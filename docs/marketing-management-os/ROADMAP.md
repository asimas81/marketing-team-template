# ROADMAP

## Sequência anterior (baseline Workspace)

| Fase | Entrega | Dependência e gate de saída |
| --- | --- | --- |
| 0. Decisões e baseline | Revisar [PRD](./PRD.md), contratos especializados, perfis de usuário, escopo MVP, provedor de identidade/banco e retenção; registrar cenários Eve e Notion atuais | Aceitar hierarquia Workspace → Product → Campaign e responsabilidades dos sete especialistas |
| 1. Fundação multi-tenant | Login web, User/Membership, Workspace, RBAC servidor, banco, auditoria, assets privados e vínculo de sessão Eve | Testes de isolamento entre Workspaces e autenticação web de ponta a ponta |
| 2. Products e contexto | Cadastro Product, Product Context Pack versionado, fontes/claims, editor/diff e aprovação; gateway de contexto para lead e especialistas | Dois Products no mesmo Workspace geram briefings isolados e reprodutíveis |
| 3. Campanhas e entregáveis | Campaign/Brief, WorkItems, catálogo e versões de Deliverable, UI de planejamento/revisão, ferramentas Eve para persistir entregas | Newsletter e peça SEO percorrem especialistas em sequência, com IDs e versões corretos |
| 4. Aprovação e execução | Fila de decisões, RBAC por ação, snapshot/hash, idempotência e reconciliação; integrar gates Eve e Resend | Mudança no conteúdo/público invalida aprovação; tentativa repetida não duplica envio |
| 5. Domain Packs | Manifesto, instalação/binding por Product, ferramentas de leitura/persistência do product/domain specialist e [evals](./EVAL_PLAN.md) | Pack ligado altera somente o Product selecionado; desligá-lo restaura comportamento genérico |
| 6. Creative Studio inicial | CreativeBrief, Sets/Artifacts/Variants, geração de imagem por adapter, asset store, custo e aprovação | Um kit com variantes é revisável por versão, sem publicação automática |
| 7. Migração Notion | Inventário, importador com preview e relatório, corte de escrita, exportação opcional | Fluxo completo funciona sem Notion e conteúdo importado tem rastreabilidade |
| 8. Operação e medição | Métricas com origem, dashboards, monitoramento de execução, retenção e documentação de extensão | Estados externos reconciliados e KPIs distinguem observado de estimado |
| 9. Creative Studio ampliado | Landing pages e books com preview/render; depois vídeo/voz por adapters; performance e variantes | Direitos, custos, revisão visual e publicação por versão passam gates próprios |

## MVP anterior (baseline Workspace)

Fases 0 a 4 formam o primeiro produto utilizável: Workspace, Product, contexto aprovado, Campaign, entregáveis internos e envio Resend controlado. A fase 5 conecta o novo especialista consultivo ao OS e valida um pack piloto contra outro Product sem pack. A fase 6 conecta o Creative Producer a geração, assets e aprovação. A fase 7 elimina a dependência operacional do Notion. Se o objetivo comercial exigir Notion opcional desde o primeiro lançamento, antecipar o corte de escrita e um importador mínimo após a fase 3, mantendo a migração completa na fase 7.

## Decisões que não devem ficar implícitas

- Identidade: provedor de login e mapeamento de principal Slack/TUI para usuário e Workspace.
- Permissões: papéis iniciais, quem publica Product Context e quem pode autorizar envio, inclusive autoaprovação.
- Armazenamento: provedor PostgreSQL, retenção, residência de dados, backup e política de assets privados.
- Documento interno: formato canônico de rich text e regras de exportação/importação.
- Packs: governança de mantenedores, revisão de fonte e política para packs de terceiros.
- Email: consentimento, segmentos e jurisdições continuam sob responsabilidade operacional do Workspace, com declaração registrada no fluxo.

## Validação por cenário

Executar ensaios com dois Workspaces, dois Products no mesmo Workspace, uma campanha multproduto, mudança de contexto após aprovação, claim sem prova, Domain Pack fora de escopo, criativo com claim alterado, asset sem licença, importação Notion parcial, falha incerta no Resend e retomada de sessão Eve. Medir se cada resposta e entrega aponta para a versão certa, se aprovações mostram o payload exato e se nenhum dado cruza a fronteira de Workspace. Seguir as verificações estáticas do repositório (`pnpm validate`) e exercitar o TUI quando houver credenciais de modelo disponíveis.

## Sequência canônica 2.1 para decomposição em SPECs

A tabela anterior registra o baseline pré-agência. A sequência abaixo reconcilia o [Product Update Plan](../harness/MARKETING_OS_PRODUCT_UPDATE_PLAN.md) com dependências arquiteturais: contrato de canal é especificado antes do primeiro envio, mesmo que Email seja o primeiro release. Toda onda exige contrato, testes de isolamento e trilha OTel/audit adequados; documentação não representa implementação.

| Onda | Capacidade | Gate antes da próxima |
| --- | --- | --- |
| A1 | Agency Tenant, Supabase Auth, AgencyMembership/RBAC e AgencyPolicy | Cross-agency deny por API/RLS e resolução de principal |
| A2 | Client Workspace, ClientWorkspaceMembership/RBAC, ClientPolicy e offboarding básico | Cross-client deny inclusive por service role delegada, UI, tool e asset |
| A3 | Product/Brand, Product Context, Domain Pack binding e Advisor Profile | Versões publicadas, claim/evidência e escopo por Client |
| A4 | Campaign, WorkRequest, Artifact/version, Approval Inbox e Publications internas | Snapshot aprovado e ownership de ponta a ponta |
| A5 | AgentRun API, Context Gateway, Eve integration e OTel distribuído | Um Client por run, custo/trace, handoff e erro/retry visíveis |
| A6 | Web Management UI, Agency/Client Dashboards, Client Portal, Reports e Metrics Foundation | Agregados só de Clients autorizados, roles do portal, métrica com definição/fonte e UX validada pelo Design System |
| A7 | Audience Intelligence e Creative Studio inicial | Persona evidenciada, Creative Brief/variant com direitos e revisão por versão |
| A8 | Engagement Channel Contract e Agentic Email: Campaigns, Broadcasts, Sequences, Segments, Templates, experimentos de Email, Automations delimitadas, Performance e AI Recommendations | Email é o primeiro canal; Client Integration Resend/Brevo, consentimento, supressão, aprovação de `SEND`, idempotência, reconciliação e métricas demonstradas |
| A9 | Experimentation Core, Client Integrations read-only e Paid Media Read/Plan | Hipótese e métrica pré-definidas; vault/reauth/revogação, account mapping e capacidades verificadas por Client |
| A10 | WhatsApp, Lead/LeadIdentity/Consent, Lead Qualification Agent e modelo de CRM Handoff | Gates separados por capacidade: identidade, opt-in, contexto mínimo, revisão da qualificação e isolamento; handoff externo aguarda conector da A12 |
| A11 | Paid Media Controlled Execution, normalização ampliada e Performance Optimizer | Policy de budget, aprovação humana, idempotência, reconciliação, test account, definição e freshness de métricas |
| A12 | Instagram DM, Facebook Messenger, SMS, Web Chat, CRM connectors/handoff, inbox gradual e atribuição avançada | Gate por canal/conector, finalidade, consentimento, receive/reply, retenção e revisão de produto; HighLevel, HubSpot, RD Station, Pipedrive e Salesforce são futuros |
| A13 | JEV limitado e autoexecução controlada | Histórico, evals, caps, override, compensação e aprovação explícita |

O recorte de MVP da decisão de produto inclui A1–A8: Agency/Client, Product/Advisor, Request/Agents, Campaign/Artifact/Approval, UI/Portal, Audience/Creative, métricas básicas e Agentic Email. A8 depende do contrato Engagement, mas não habilita os outros cinco canais. WhatsApp e Lead Qualification (A10), CRM (A12) e mídia paga com execução real (A11) continuam futuras e possuem gates próprios. Creative Studio amplia landing pages/books/vídeo por adapters após A7. Migração Notion pode ocorrer por Client após A4, com corte de escrita quando o fluxo interno estiver completo. Em cada SPEC, separar owner do Control Plane e do runtime Eve, contrato versionado, UI prototipada quando necessário, migração compatível, RLS/tests/evals e rollback. O [gap analysis](./PRD_ARCHITECTURE_GAP_ANALYSIS.md) e o [harness readiness](../harness/HARNESS_READINESS_REPORT.md) registram dependências abertas.
