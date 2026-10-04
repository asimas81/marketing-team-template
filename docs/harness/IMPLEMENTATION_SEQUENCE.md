# Implementation Sequence

1. Aprovar Constituição, ADRs e decisões A01/A02; definir ambientes seguros e contratos de tenancy.
2. Implementar Auth, Agency/Client membership, RLS e testes cross-tenant antes de expor dados. ClientPolicy e AuditEvent entram junto.
3. Criar Product Context, Domain Pack, Campaign, Request, Artifact e Approval com versões e ownership. Garantir fluxo sem Notion.
4. Fechar API/Context Contract, AgentRun persistido, identity delegation e OTel; integrar Eve por contrato, mantendo especialistas atuais.
5. Prototipar/validar Agency/Client UI e Portal; adicionar Audience/Persona evidenciada, Creative Core e Experimentation.
6. Definir vault/OAuth, account mappings e conectores client-scoped em modo read-only/teste. Importar métricas nativas e normalizadas com atribuição declarada.
7. Habilitar Paid Media planning e, só depois dos gates, execução real aprovada/idempotente com limite de budget e reconciliação.
8. Ligar Performance Recommendation e feedback a Audience/Creative; considerar JEV/autoexecução somente com histórico, evals, policy e override humano.

Cada etapa tem SPEC, PR, testes, security review, evidência OTel e rollout seguro. A ordem preserva Agency/Client isolation antes de mídia real. Migração Notion e offboarding evoluem por Client após catálogo e integração. A ausência de qualquer pré-condição bloqueia a etapa dependente, não a decomposição da SPEC.
