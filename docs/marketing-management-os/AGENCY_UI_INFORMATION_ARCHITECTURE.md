# AGENCY_UI_INFORMATION_ARCHITECTURE

## Navegação e escopo

A Web UI é a superfície principal de operação, com Marketing Lead/chat como utility surface contextual em drawer, command palette e páginas de Client/Campaign, não homepage. O [Design System](../harness/MARKETING_OS_DESIGN_SYSTEM.md) é referência canônica de UX/UI; a [Prototype Inspiration](../harness/MARKETING_OS_PROTOTYPE_INSPIRATION.md) orienta prototipação sem copiar concorrentes.

O app Next.js atual fornece chat e retomada de sessão. O alvo adiciona interface de gestão sobre o mesmo Control Plane e mantém o chat contextual. O seletor de Agency é global; o seletor de Client aparece antes de qualquer operação específica. Breadcrumb e cabeçalho mostram `Agency / Client / Product / Campaign`; mudança de escopo descarta drafts locais e caches de outro Client após aviso de perda de trabalho não salvo. Rotas e IDs não substituem autorização da API/RLS.

| Perspective | Navegação | Informação principal |
| --- | --- | --- |
| Agency | Dashboard, Clients, Approvals, Agent Runs, Performance, Alerts, Costs, Settings | Agregado SQL dos Clients autorizados; filtros por Client, Product, canal, período e owner; alertas de integração, budget e run |
| Client Workspace | Dashboard, Requests, Products, Audiences, Campaigns, Content, Creative Studio, Engagement, Experiments, Paid Media, Performance, Approvals, Publications, Agents, Integrations, Reports, Settings | Recursos e métricas apenas daquele Client; Product/Campaign como filtros persistentes; Engagement começa por Email |
| Client Portal | Overview, Campaigns, Creatives/Content, Approvals, Performance, Reports, Activity | Visão e ações permitidas ao cliente no mesmo backend, com navegação reduzida |

## Fluxos principais

`Request → AgentRun → Artifact/Advisory → Review → Approval Inbox → Publication/ExternalAction → Metrics → Report`. Request exige Client e objetivo; Product/Campaign são escolhidos quando aplicáveis. A tela de Agent Runs mostra status, etapas, custo, outputs, erros e retry permitido; toda abertura valida Client. Content e Creative Studio são bibliotecas canônicas com versões, fontes, preview e diff. Campaign detalha brief, audiência, WorkItems, budget, canais, entregas, experimentos e performance. Publications mostra versão publicada, destino, conta externa, horário, estado reconciliado e métricas.

Approval Inbox filtra por `assigned_to_me`, Client, tipo, prazo e risco. Cada decisão mostra conteúdo/payload exatos, policy, claim/evidência e efeito externo, incluindo gasto. Integrations exibe OAuth/contas/health/reauth/revogação. Performance mostra métrica nativa e normalizada, definição, janela, freshness e advertência de comparação. Reports exportam snapshots autorizados, nunca um link externo como única cópia canônica.

Agency Dashboard não envia dados brutos de vários clientes a Eve. Consultas do Control Plane agregam escopo autorizado e preservam supressão de dimensões sensíveis. Estados vazios explicam falta de integração, ausência de dados ou falta de permissão de forma distinta. Fluxos de UX com impacto relevante exigem protótipo e validação antes da SPEC de implementação.

Engagement abre inicialmente Campaigns, Broadcasts, Sequences, Segments, Templates, Experiments e Performance de Email. Outros canais só aparecem com estado futuro/indisponível até integração e policy real. A futura visão de Lead/Conversation e Handoff pertence ao mesmo Client e respeita permissões específicas. A tela de Approval distingue `DRAFT`, `PREPARE`, `SCHEDULE`, `SEND` e `PUBLISH` e mostra o efeito concreto da ação.
