# CLIENT_WORKSPACE_MODEL

## Unidade operacional

`ClientWorkspace(id, agency_id, name, slug, status, owner, locale, timezone, created_at)` pertence a uma única Agency. Slug é único dentro da Agency. Estados sugeridos: `ONBOARDING`, `ACTIVE`, `SUSPENDED`, `OFFBOARDING`, `ARCHIVED`. Suspensão impede novas execuções externas; leitura para auditoria e exportação depende de papel e política. Reativação exige verificação de memberships, integrações e aprovações vencidas.

`ClientWorkspaceMembership` vincula usuário, Client, papel, origem agência/cliente, status e janela de validade. `ClientPolicy` versionada define canais permitidos, revisões de domínio/claims, aprovação editorial e de execução, horários, limites de custo e verba, provedores criativos e retenção. Cada ação fixa a versão de policy efetiva usada. Exceções têm owner, prazo e auditoria; não são instruções em prompt.

O Client contém Products/Brands, Product Context Pack por Product, bindings de Domain Pack, Advisor Profile, Campaigns, WorkRequests, AgentRuns, Audience, Creative Studio, Experiments, Publications, Metrics, Reports, Approvals, Assets e ClientIntegrations. Entidades derivadas carregam owner do Client; referências externas mantêm mesmo escopo. Um Product não muda de Client por simples edição de FK: transferência requer procedimento com reautorização, revisão de integrações e auditoria.

## Onboarding e operação

Criar Client exige AgencyMembership com `client:create`, nome, owner e policy inicial. O onboarding atribui equipe, convida usuários, registra Products, aprova contextos, escolhe Domain Packs e Advisor, define integrações e mede readiness. Requests e chat iniciam dentro de Client selecionado; o Marketing OS cria `AgentRun` antes de chamar Eve e passa apenas contexto desse Client. A UI mostra escopo ativo persistentemente e exige nova seleção para operar outro cliente.

O Client Dashboard apresenta campanhas, aprovações, runs, conteúdos, criativos, experimentos, mídia, métricas e saúde de integrações daquele Client. O [portal](./CLIENT_PORTAL_MODEL.md) é outra superfície do mesmo Control Plane. Offboarding segue [runbook](./CLIENT_OFFBOARDING_MODEL.md).
