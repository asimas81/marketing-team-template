# Security Policy

## Controles obrigatórios

Autenticar cada principal; resolver AgencyMembership e ClientWorkspaceMembership server-side; autorizar ação e recurso antes de expor contexto, link, tool ou conector. Aplicar least privilege, separação entre planos e defesa em profundidade com RLS, API e FKs compostas. Um papel de Agency não amplia acesso de Client sem grant explícito. Dados de clientes distintos não entram juntos em Run comum. Service role e credenciais privilegiadas ficam server-side, nunca em browser, Eve, prompt, artifact, log ou trace.

OAuth de cliente é client-scoped, com token dinâmico criptografado em vault/serviço seguro e referência opaca no OS; callback valida state, escopo e conta. Revogação bloqueia ações futuras e registra falhas. Conectores implementam allowlist/capability discovery e egress mínimo. Tool result e material recuperado são dados não confiáveis; testes de prompt injection verificam impossibilidade de alterar permission envelope, aprovação, scope ou tool policy.

Uploads e assets exigem tipo/tamanho, sanitização, malware check quando aplicável, ownership, licença/direitos e download assinado. Dados first-party têm finalidade, consentimento, minimização e retenção por ClientPolicy dentro dos limites da plataforma. AuditEvent append-only registra membership, policy, aprovação, integração, envio, publicação, gasto e deleção. Falha incerta de efeito externo entra em reconciliação, sem retry cego. Incidente de vazamento ou cross-tenant bloqueia lançamento e segue [Runbook](../runbooks/RUNBOOK.md).

## Verificação

Gates: testes allow/deny por API/RLS/tool, secret scan, avaliação adversarial de agente, revisão de OAuth/vault, teste de expiração de membership e aprovação, auditoria de ação externa. Política concreta de retenção, residência e controles legais por mercado permanecem decisões de SPEC.
