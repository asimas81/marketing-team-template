# Marketing Management OS

**Agentic Marketing Operations Platform for Agencies** em evolução a partir de um time de agentes de marketing construído com [Eve](https://eve.dev). Este repositório reúne o runtime e o web chat existentes com a arquitetura de produto e o Harness que orientarão a implementação do sistema de gestão.

> **Estado atual:** o código executa um Marketing Lead, sete especialistas Eve e uma interface Next.js de chat. O Marketing Management OS descrito em `docs/` ainda é arquitetura alvo: a interface de gestão, o banco como system of record, o Client Portal e as integrações por Client Workspace não estão implementados neste repositório.

## O que existe hoje

O Marketing Lead recebe a solicitação, consulta o contexto de marca compartilhado e encaminha o trabalho ao especialista adequado. Quando uma entrega depende de outra, ele encadeia os especialistas e transmite o resultado anterior no briefing. Os agentes atuais usam Vercel Blob para contexto e artefatos, Notion para parte dos documentos e Resend para operações de email. O web app atual é uma interface de chat; também há TUI local e canal Slack configurável.

| Especialista | Responsabilidade atual |
| --- | --- |
| `product-marketer` | Posicionamento, mensagens e documento de brand context compartilhado |
| `content-marketer` | Planejamento e redação de conteúdo longo, com entregas no Notion |
| `social-media-coordinator` | Posts e threads para redes sociais |
| `seo` | Auditorias e recomendações de busca orgânica |
| `email` | Adaptação de conteúdo existente, campanhas e envios via Resend com aprovação |
| `product-domain-specialist` | Advisory sobre fatos de produto, domínio, claims, restrições e riscos |
| `creative-producer` | Briefs, especificações, storyboards e variantes criativas para revisão |

O `product-domain-specialist` e o `creative-producer` produzem orientação e especificações revisáveis. As APIs de Product Context, Campaign, Asset e Approval do futuro OS ainda não estão conectadas; o Creative Producer não renderiza imagens ou vídeos atualmente. A [arquitetura do runtime existente](./docs/ARCHITECTURE.md) detalha ferramentas, limites e fluxo de dados.

## Produto planejado

O Marketing OS terá uma **interface Web de gestão como superfície principal**. O chat com o Marketing Lead será uma utilidade contextual. O Control Plane será o system of record para operações de marketing, separado da execução cognitiva no Eve. A hierarquia de isolamento é `Agency Tenant → Client Workspace → Product/Brand → Campaign`; cada Product terá contexto versionado, e conhecimento de segmento entrará por Domain Pack e Advisor Profile, sem especializar os agentes genéricos por mercado. O Notion passará a ser uma opção de importação/exportação, não a fonte canônica dos dados.

O MVP definido na documentação inclui Agency e Client Workspaces, Products e contexto, campanhas e aprovações, Audience Intelligence, Creative Studio inicial, métricas básicas, Agentic Email e **Client Portal**. O portal terá `Overview`, `Campaigns`, `Creatives`, `Approvals`, `Performance`, `Reports` e `Requests`, com acesso restrito ao cliente e sem configurações internas ou dados de outros clientes.

Engagement modela `EMAIL`, `WHATSAPP`, `SMS`, `INSTAGRAM_DM`, `FACEBOOK_MESSENGER` e `WEB_CHAT`. Email é o primeiro canal planejado. WhatsApp, os demais canais, Lead Qualification e conectores CRM continuam no roadmap. O Marketing OS cuidará de aquisição, engajamento, qualificação futura, medição e otimização; oportunidade, pipeline e vendas permanecem no CRM. Integrações, envio real e mídia paga dependem de políticas de consentimento, permissão, aprovação, isolamento e auditoria antes de serem habilitados.

Esses itens descrevem **escopo e sequência planejados**, não funcionalidades disponíveis no web app atual. Consulte o [PRD](./docs/marketing-management-os/PRD.md), a [arquitetura funcional](./docs/marketing-management-os/ARCHITECTURE.md) e o [roadmap](./docs/marketing-management-os/ROADMAP.md) para os gates de entrega.

## Estrutura do repositório

| Caminho | Conteúdo |
| --- | --- |
| [`agent/`](./agent/) | Marketing Lead, sete subagentes, ferramentas, skills, canais e conexões Eve |
| [`apps/web/`](./apps/web/) | Web chat Next.js existente |
| [`docs/marketing-management-os/`](./docs/marketing-management-os/) | PRD, modelos de domínio, arquitetura funcional, capacidades e roadmap do produto |
| [`docs/harness/`](./docs/harness/) | Contratos, políticas, segurança, observabilidade, execução e governança para a futura implementação |
| [`docs/ARCHITECTURE.md`](./docs/ARCHITECTURE.md) | Mapa técnico do runtime atual |

O [índice de artefatos do produto](./docs/marketing-management-os/README.md) e o [índice do Harness](./docs/harness/README.md) são os pontos de entrada para a documentação detalhada. O [Product Update Plan](./docs/harness/MARKETING_OS_PRODUCT_UPDATE_PLAN.md) registra as decisões recentes; o [Design System](./docs/harness/MARKETING_OS_DESIGN_SYSTEM.md) é a referência de UX/UI, e [Prototype Inspiration](./docs/harness/MARKETING_OS_PROTOTYPE_INSPIRATION.md) orienta a prototipação.

## Desenvolvimento local

Requisitos: Node.js **24.x** e pnpm **11.22.0**. O `packageManager` em `package.json` fixa a versão do pnpm.

```bash
corepack enable
pnpm install --frozen-lockfile
pnpm validate
pnpm dev
```

`pnpm dev` abre o TUI do Eve. Para rodar Eve e o web chat juntos, use `pnpm dev:all` após vincular um projeto Vercel e configurar os recursos necessários. O arquivo [`.env.example`](./.env.example) documenta os identificadores de conectores, sem credenciais válidas. Cada usuário autoriza Notion e Resend pelo fluxo da conexão.

| Comando | Finalidade |
| --- | --- |
| `pnpm dev` | TUI local do Eve |
| `pnpm dev:all` | Eve e Next.js pelo roteador local da Vercel |
| `pnpm dev:web` | Frontend isolado; use `dev:all` para chat conectado |
| `pnpm validate` | Lint, TypeScript e descoberta do Eve |
| `pnpm exec eve info` | Agentes, ferramentas e diagnósticos descobertos |
| `pnpm build` / `pnpm build:web` | Builds do Eve e do web app |

Para configurar uma instância própria, execute `pnpm exec eve link`, associe os recursos Vercel e os conectores usados e carregue o ambiente local com `pnpm exec vercel env pull .env.local`. A implantação do runtime existente usa `pnpm exec eve deploy`. Vincular ou implantar o template não implementa o Control Plane ou o login do futuro Marketing OS.

## Origem e licença

O runtime começou a partir do [marketing-team-eve-template da Vercel Labs](https://github.com/vercel-labs/marketing-team-eve-template). O pacote ainda se chama `marketing-team-eve-template` e está na versão `0.1.0`; a evolução para Marketing Management OS está documentada separadamente. Licenciado sob [MIT](./LICENSE).
