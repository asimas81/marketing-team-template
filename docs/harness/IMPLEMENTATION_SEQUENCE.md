# Implementation Sequence

1. Aprovar Constituição, ADRs e decisões A01/A02; definir ambientes seguros e contratos de tenancy.
2. Implementar Auth, Agency/Client membership, RLS e testes cross-tenant antes de expor dados. ClientPolicy e AuditEvent entram junto.
3. Criar Product Context, Domain Pack, Campaign, Request, Artifact e Approval com versões e ownership. Garantir fluxo sem Notion.
4. Fechar API/Context Contract, AgentRun persistido, identity delegation e OTel; integrar Eve por contrato, mantendo especialistas atuais.
5. Prototipar/validar a Web UI principal de Agency/Client, Client Portal e Metrics Foundation; adicionar Audience/Persona evidenciada e Creative Core.
6. Especificar `EngagementChannel`, identidade de contato, consentimento e supressão mínimos por Client/canal/finalidade. Definir vault/conta/remetente client-scoped e adapter piloto Resend ou Brevo; habilitar Agentic Email somente após approval de SEND, idempotência, reconciliação, métricas e testes de isolamento. O Lead model completo vem depois.
7. Adicionar Experimentation Core, account mappings e conectores de mídia client-scoped em modo read-only/teste; importar métricas com atribuição declarada e habilitar Paid Media planning.
8. Especificar WhatsApp, Lead Qualification e modelo de CRM Handoff em gates próprios; executar handoff externo somente após conector CRM autorizado. SMS, Instagram DM, Facebook Messenger e Web Chat seguem SPECs posteriores por canal.
9. Habilitar Paid Media controlada somente após approval, budget policy, idempotência e reconciliação; ligar Performance Recommendation e feedback a Audience/Creative. Considerar JEV/autoexecução somente com histórico, evals, policy e override humano.

Cada etapa tem SPEC, PR, testes, security review, evidência OTel e rollout seguro. A ordem preserva Agency/Client isolation antes de mídia real. Migração Notion e offboarding evoluem por Client após catálogo e integração. A ausência de qualquer pré-condição bloqueia a etapa dependente, não a decomposição da SPEC.

O conector Resend atual serve apenas como baseline de migração; não prova Client ownership, consentimento ou SEND do OS. A ordem de construção da UI pode antecipar protótipos de Engagement, mas não antecipa envio real. O [Product Update Plan](./MARKETING_OS_PRODUCT_UPDATE_PLAN.md) informa o escopo e o [Roadmap canônico](../marketing-management-os/ROADMAP.md) fixa as ondas de produto; esta sequência explicita os gates de Harness correspondentes.
