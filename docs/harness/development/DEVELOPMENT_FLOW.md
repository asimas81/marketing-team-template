# Development Flow

Fluxo padrão: Constituição → SPECIFY → CLARIFY → protótipo/validação UX quando necessário → PLAN → TASKS → IMPLEMENT → testes/evals → revisão → CI → preview → aprovação humana de release. Esta execução encerra-se antes de IMPLEMENT. Toda SPEC informa owner (Control Plane/runtime), mudança de contrato, autorização/RLS, modelo de dados, UI, observabilidade, migração compatível, rollback, limites de custo e critérios de aceite.

Feature cross-repo usa ID comum e contrato-first: contrato canônico no OS → mock/client versionado → implementação do OS → integração Eve → contract tests → E2E. Mudança breaking tem versionamento e janela de compatibilidade. Não há terceiro repositório de contratos por padrão. UX de dashboards, Campaign, Creative Studio, Approval Inbox, Product Context, Agent Runs e métricas exige protótipo e validação antes de código.

Revisor técnico verifica invariantes e `pnpm validate` no template Eve; Security Reviewer cobre RBAC/RLS/segredos; AI Behavior Reviewer cobre contexto/evals; owner humano aprova mudanças estruturais e produção. [Definition of Done](../definition-of-done/DEFINITION_OF_DONE.md) e [Spec Readiness Map](../SPEC_READINESS_MAP.md) guiam cada etapa.

Protótipos de Engagement e Approval Inbox devem demonstrar Agency/Client/Product ativo, identidade do canal, destinatário/segmento, consentimento, suppression, versão, custo, horário e consequência de `SCHEDULE` versus `SEND`. Chat permanece utility surface, não homepage. Aplicar [Design System](../MARKETING_OS_DESIGN_SYSTEM.md) e validar os fluxos do [Prototype Inspiration](../MARKETING_OS_PROTOTYPE_INSPIRATION.md), inclusive revisão pelo cliente no Portal, antes de SPEC de UI implementável.
