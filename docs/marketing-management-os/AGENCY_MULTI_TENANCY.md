# AGENCY_MULTI_TENANCY

## Fronteiras e ownership

`AgencyTenant` é a fronteira superior de isolamento. `ClientWorkspace` pertence a uma única Agency e é a fronteira operacional entre clientes. Product/Brand, Campaign, WorkRequest, Artifact, Audience, Experiment, Metric, Approval, AgentRun, custos e integrações carregam `agency_id` e `client_workspace_id` ou uma relação verificável que fixe ambos. O termo `workspace_id` nos contratos anteriores passa a significar `client_workspace_id`; contratos novos usam o nome explícito. IDs vindos de URL, prompt ou callback nunca concedem autorização.

```text
Platform → AgencyTenant → ClientWorkspace → Product/Brand → Campaign → trabalho e resultados
```

O Control Plane resolve identidade, AgencyMembership e ClientWorkspaceMembership antes de qualquer consulta, mutação, delegação ou agregação. Um usuário pode integrar mais de uma Agency e ter papéis diferentes em cada Client. A sessão seleciona Agency e Client explicitamente; troca de escopo limpa contexto de UI e invalida cache de autorização. Usuário do cliente acessa apenas seu Client Workspace. Papel na agência não concede acesso indiscriminado a todos os clientes: acesso operacional depende da atribuição explícita ou de papel administrativo definido na [matriz](./TENANT_RBAC_MATRIX.md).

## Persistência e defesa em profundidade

Supabase Auth é a identidade alvo e Supabase PostgreSQL o system of record. RLS deve filtrar linhas por `agency_id` e `client_workspace_id` em tabelas expostas; a API aplica a mesma política e valida relações compostas para Product, Campaign, Artifact e contas externas. Recursos apenas de Agency, como billing, não têm Client owner, mas exigem AgencyMembership. Credenciais de service role ficam server-side, fora de prompts e browser, com operações privilegiadas explicitamente autorizadas e auditadas. Dados binários usam metadados de ownership no banco e acesso assinado; a chave do objeto não é autorização.

Testes de contrato e RLS devem cobrir negação cross-agency e cross-client, adulteração de IDs, cliente sem membership, troca de Agency na mesma sessão, role read-only, vínculo entre Product/Campaign de clientes diferentes e acesso por ferramenta Eve. O dashboard da agência agrega em SQL apenas os clientes autorizados, com definições de métricas compatíveis; LLM recebe agregado autorizado para explicar, não dados crus combinados de vários clientes.

## Política, auditoria e observabilidade

Policy efetiva segue `platform hard limits → AgencyPolicy → ClientPolicy → Product/Campaign constraints`. Uma política inferior pode restringir, nunca ampliar. Alterações de membership, policy, Advisor Profile, integração, aprovação e execução externa geram AuditEvent append-only com ator, escopo, resultado, motivo e `trace_id`. OpenTelemetry propaga correlação entre UI, API, Eve e conectores; `agency_id` e `client_workspace_id` ficam em traces protegidos, não em labels agregadas de alta cardinalidade. Logs removem tokens e dados sensíveis.

## Gate

Nenhuma integração real de mídia é habilitada antes de testes de isolamento, RBAC, ownership de conta, auditoria e aprovação passarem em ambiente seguro. Esta é arquitetura alvo, não capacidade implementada.
