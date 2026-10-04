# Security Policy

## Controles obrigatórios

Autenticar cada principal; resolver AgencyMembership e ClientWorkspaceMembership server-side; autorizar ação e recurso antes de expor contexto, link, tool ou conector. Aplicar least privilege, separação entre planos e defesa em profundidade com RLS, API e FKs compostas. Um papel de Agency não amplia acesso de Client sem grant explícito. Dados de clientes distintos não entram juntos em Run comum. Service role e credenciais privilegiadas ficam server-side, nunca em browser, Eve, prompt, artifact, log ou trace.

OAuth de cliente é client-scoped, com token dinâmico criptografado em vault/serviço seguro e referência opaca no OS; callback valida state, escopo e conta. Revogação bloqueia ações futuras e registra falhas. Conectores implementam allowlist/capability discovery e egress mínimo. Tool result e material recuperado são dados não confiáveis; testes de prompt injection verificam impossibilidade de alterar permission envelope, aprovação, scope ou tool policy.

Uploads e assets exigem tipo/tamanho, sanitização, malware check quando aplicável, ownership, licença/direitos e download assinado. Dados first-party têm finalidade, consentimento, minimização e retenção por ClientPolicy dentro dos limites da plataforma. AuditEvent append-only registra membership, policy, aprovação, integração, envio, publicação, gasto e deleção. Falha incerta de efeito externo entra em reconciliação, sem retry cego. Incidente de vazamento ou cross-tenant bloqueia lançamento e segue [Runbook](../runbooks/RUNBOOK.md).

## Verificação

Gates: testes allow/deny por API/RLS/tool, secret scan, avaliação adversarial de agente, revisão de OAuth/vault, teste de expiração de membership e aprovação, auditoria de ação externa. Política concreta de retenção, residência e controles legais por mercado permanecem decisões de SPEC.

## Engagement, contato e consentimento

Para cada envio, resolver `ClientWorkspace`, `ClientIntegration`, `ChannelIdentity`, Lead/destinatário e finalidade. Verificar `ConsentRecord` aplicável ao canal e à finalidade, opt-in/opt-out, suppression/unsubscribe, conta/remetente autorizado, ClientPolicy e janela de envio imediatamente antes do side effect. Consentimento de Email não autoriza WhatsApp, SMS ou DM; identidade igual em dois Clients não compartilha consentimento. Ausência, revogação, fonte não verificável ou suppression bloqueia SEND e registra razão sem expor dados pessoais ao agente.

Credenciais de canais e CRM são referências por Client em vault server-side; callbacks/webhooks autenticados são associados à conta e Client antes de qualquer leitura ou escrita. Contatos e threads são minimizados por finalidade, separados de fatos de produto, com retenção/acesso/exportação/deleção próprios. Lead Qualification recebe envelope e resumo mínimos, nunca base completa. `EngagementAction` usa idempotency key durável por destinatário/variante, rate limit por conta/Client/canal, retry limitado e reconciliação de mensagem incerta antes de nova tentativa. Audit de SEND inclui ator, approval, consent snapshot, identidade pseudonimizada, conta, artifact/version, provider message ID, resultado e trace; logs/traces omitem endereço, telefone, texto privado e token. Os controles detalhados estão no [Engagement Channel Contract](../contracts/ENGAGEMENT_CHANNEL_CONTRACT.md).
