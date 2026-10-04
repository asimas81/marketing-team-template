# Spec Readiness Map

| Onda | SPEC sugerida | Pré-condição | Questão a fechar |
| --- | --- | --- | --- |
| 1 | A01 Agency Tenant Foundation | PRD/Constitution | Nome técnico, owner e política |
| 1 | A02 Agency + Client Membership RBAC/Auth/RLS | A01 | Login, grants, revogação, matriz RLS |
| 1 | A03 Client Workspace + A04 Client Policy | A02 | Ciclo de vida, limites e defaults |
| 1 | Product Context + Domain Pack | A03/A04 | Schema, publicação e packs privados |
| 1 | Campaign/Request/Artifact/Approval | Context | Estados, rich text, approval policy |
| 1 | A05 Client Advisor Profile | Context/Domain/API | Override Product e Remote Agent futuro |
| 2 | AgentRun API + Eve Context Integration + OTel | RBAC/Artifact/Approval | Transporte, token delegado, traces |
| 2 | A07 Agency Dashboard + A08 Client Dashboard + A09 Portal | RBAC/Metrics básicas | UX protótipo e grants do portal |
| 2 | Audience, Creative Core e Experimentation | Context/Campaign/Artifact | Evidência, provider/storage, stop rules |
| 3 | A06 Client Integration Vault/References | RBAC/Approval/Audit | Vault, OAuth, mapping, health |
| 3 | Paid Media abstraction + conectores read-only | A06/Audience/Experiment | Canal piloto, capabilities |
| 3 | Metrics normalization + attribution | Conectores e Campaign | Definições e janela MVP |
| 3 | Controlled Paid Media execution | A06/Metrics/Approval/Budget | Test account, idempotência, reconciliação |
| 4 | Performance Optimizer + recommendation/approval | Metrics/Experiment | Thresholds e evals |
| 4 | A10 Offboarding | A03/A06/Retention | Export, revogação, audit |
| 5 | JEV bounded optimization + autoexecution | Histórico/guardrails/evals | Limits, override, rollback |

Sequência é por dependência, não compromisso de calendário. Cada SPEC exige critérios de aceitação, owner, UX gate quando aplicável, API/schema, RLS/isolamento, observabilidade, migração e rollback. Produzir SPEC não autoriza implementação automática. [Implementation Sequence](./IMPLEMENTATION_SEQUENCE.md) detalha os gates.
