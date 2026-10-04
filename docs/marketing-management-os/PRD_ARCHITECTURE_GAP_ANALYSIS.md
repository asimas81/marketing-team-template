# PRD_ARCHITECTURE_GAP_ANALYSIS

## Escopo e evidência

Comparação entre [PRD v2](./PRD.md), o [delta de agência](./AGENCY_MULTI_TENANT_ARCHITECTURE_UPDATE.md), o [harness v1.2](./HARNESS_ENGINEERING_MARKETING_MANAGEMENT_OS.md) e a arquitetura anterior deste diretório. O arquivo pedido como `MARKETING_OS_SPECIALISTS.md` não existe no repositório nem no pacote localizado; a referência disponível e lida foi `C:/Users/simas/Downloads/MARKETING_OS_PRODUCT_DOMAIN_AND_CREATIVE_SPECIALISTS.md`. O delta de Audience/Paid Media foi lido em `C:/Users/simas/Downloads/MARKETING_OS_AUDIENCE_PAID_MEDIA_ARCHITECTURE_UPDATE.md`. Os arquivos em Downloads são fontes de entrada, não entregáveis copiados. Esta análise descreve arquitetura alvo; o código permanece no estado atual.

| Tema do PRD v2 | Baseline antes desta atualização | Cobertura documental v2 | Lacuna de implementação/decisão |
| --- | --- | --- | --- |
| Agency Tenant e Client Workspace | Workspace era tenant único | [Tenancy](./AGENCY_MULTI_TENANCY.md), [Client](./CLIENT_WORKSPACE_MODEL.md), [Domain Model](./DOMAIN_MODEL.md) | Auth/RLS, IDs/FKs e migração do estado global inexistentes |
| RBAC em dois níveis e Client Portal | Chat sem papéis de negócio | [Matriz](./TENANT_RBAC_MATRIX.md), [Portal](./CLIENT_PORTAL_MODEL.md) | Grants, policy efetiva e escopo MVP do portal a fechar |
| Advisor por cliente/produto | Subagente consultivo genérico, sem perfil persistido | [Advisor Profile](./CLIENT_ADVISOR_PROFILE_SPEC.md), [Topology](./AGENT_TOPOLOGY.md) | Schema, UI, API e binding remoto futuro |
| Product Context e Domain Packs | Specs por Workspace/Product | [Product Context](./PRODUCT_CONTEXT_SPEC.md), [Domain Pack](./DOMAIN_PACK_SPEC.md) | Persistência/versionamento e governança de packs privados |
| Requests, Agent Runs e Control/Eve boundary | Eve e chat, sem OS de negócio | [Runtime Contract](./AGENT_RUNTIME_CONTRACT.md), [Target](./TARGET_ARCHITECTURE.md) | Transporte, identidade delegada, eventos e custo por Run |
| Creative Studio, Content, Campaigns | Especialista criativo textual; Notion/Blob como saídas | [Creative](./CREATIVE_STUDIO_SPEC.md), [Campaign](./CAMPAIGN_MODEL.md) | Asset store e provider adapters; rich text interno |
| Audience Intelligence e personas | Não modelados | [Audience](./AUDIENCE_INTELLIGENCE_SPEC.md), [Domain Model](./DOMAIN_MODEL.md) | Fontes first-party, consentimento, thresholds de validação |
| Experiments, Paid Media e conectores | Sem campanhas ou integrações de ads no OS | [Experiment](./EXPERIMENTATION_MODEL.md), [Paid Media](./PAID_MEDIA_ARCHITECTURE.md), [Connectors](./CHANNEL_CONNECTORS_SPEC.md) | OAuth/vault, APIs por conta, canal piloto e ambiente de teste |
| Métricas, performance e verba | UTMs/Resend, sem ingestão normalizada | [Performance](./PERFORMANCE_OPTIMIZATION_MODEL.md), [Learning Loop](./MARKETING_LEARNING_LOOP.md) | Atribuição MVP, mappings e limites de budget |
| Aprovações e ações externas | Gates Eve/Resend sem trilha de negócio própria | [Approval](./APPROVAL_MODEL.md), [Integrations](./INTEGRATION_MODEL.md) | Workflow, dual approval, idempotência e reconciliação |
| Agency/Client UI, dashboards, Reports/Publications | Web app de chat | [UI IA](./AGENCY_UI_INFORMATION_ARCHITECTURE.md), [Portal](./CLIENT_PORTAL_MODEL.md) | Protótipos, queries e modelos de relatório |
| Notion opcional e offboarding | Conteúdo longo ainda usa Notion | [Migração](./MIGRATION_FROM_NOTION.md), [Offboarding](./CLIENT_OFFBOARDING_MODEL.md) | Importador, retenção, export format e revogação |
| Observabilidade e harness | Sem Control Plane distribuído | [Integration Model](./INTEGRATION_MODEL.md), [Harness Readiness](./HARNESS_READINESS_REPORT.md) | OTel end-to-end, CI/RLS/evals e ambientes |

## Invariantes aceitos para decomposição

O OS possui business state; Eve executa trabalho cognitivo. Agência e Client são fronteiras distintas, com membership e checagem server-side; o modelo nunca autoriza recursos. Integração e conta externa têm Client owner; nenhuma ação de mídia real antes de isolamento, aprovação, audit, budget e reconciliação. Product Context e Domain Pack são versionados, Advisor é perfil sobre agente genérico, especialistas de craft permanecem genéricos. Notion é opcional. Métricas mantêm valor nativo/normalizado e proveniência; LLM recomenda ou explica, não gasta. OpenTelemetry correlaciona os planos sem vazar segredos.

## Checklist obrigatório de cobertura arquitetural

| Requisito | Documento de referência | Coberto como alvo? |
| --- | --- | --- |
| Isolamento entre Agencies e entre Clients; RBAC em dois níveis; Supabase Auth/RLS | [Agency Multi-Tenancy](./AGENCY_MULTI_TENANCY.md), [RBAC Matrix](./TENANT_RBAC_MATRIX.md) | Sim |
| Advisor Profile por Client/Product e integrações client-scoped | [Advisor](./CLIENT_ADVISOR_PROFILE_SPEC.md), [Client Integration](./CLIENT_INTEGRATION_MODEL.md) | Sim |
| Agency Dashboard, Client Dashboard e Client Portal | [UI IA](./AGENCY_UI_INFORMATION_ARCHITECTURE.md), [Portal](./CLIENT_PORTAL_MODEL.md) | Sim |
| Requests, Agent Runs e Eve execution plane | [Agent Runtime Contract](./AGENT_RUNTIME_CONTRACT.md), [Agent Topology](./AGENT_TOPOLOGY.md) | Sim |
| Creative Studio e Audience Intelligence | [Creative](./CREATIVE_STUDIO_SPEC.md), [Audience](./AUDIENCE_INTELLIGENCE_SPEC.md) | Sim |
| Campaign Management, Paid Media e Experimentation | [Campaign](./CAMPAIGN_MODEL.md), [Paid Media](./PAID_MEDIA_ARCHITECTURE.md), [Experimentation](./EXPERIMENTATION_MODEL.md) | Sim |
| Performance, métricas normalizadas e budget policies | [Performance](./PERFORMANCE_OPTIMIZATION_MODEL.md), [Domain Model](./DOMAIN_MODEL.md) | Sim |
| Approval Inbox, Publications e Reports | [Approval](./APPROVAL_MODEL.md), [UI IA](./AGENCY_UI_INFORMATION_ARCHITECTURE.md) | Sim |
| OpenTelemetry | [Integration Model](./INTEGRATION_MODEL.md), [Harness Readiness](./HARNESS_READINESS_REPORT.md) | Sim |

“Sim” significa contrato/arquitetura documentado, não funcionalidade implementada.

## Decisões ainda abertas

1. Nome técnico `AgencyTenant` ou `Organization` e suporte a marca direta no MVP.
2. Escopo inicial do Client Portal e grants exatos de cada papel, inclusive dupla aprovação e autoaprovação.
3. Advisor Profile padrão por Client com override por Product (proposto) versus outro arranjo; Remote Agent e packs piloto.
4. Fluxo de Supabase Auth, identidade delegada para Eve, contrato/versionamento entre repos e propagação de trace.
5. Storage privado de assets (Vercel Blob ou Supabase Storage), formato canônico de documento e retenção/exportação por Client.
6. Vault de credenciais dinâmicas, OAuth por provider, canal de mídia piloto, capabilities reais e ambiente de teste.
7. Modelo de atribuição MVP, definições normalizadas, thresholds de persona/experimento/performance, stop rules e limites de budget.
8. Outbox/queue, streaming de AgentRun, providers criativos e momento de adoção de JEV/RAG.

Essas decisões cabem nas SPECs correspondentes e são blockers de implementação das capacidades afetadas, não impedem decompor o trabalho por dependências. [ROADMAP](./ROADMAP.md) ordena tenancy e isolamento antes de mídia real. `REPOSITORY_READY_FOR_SPEC_DECOMPOSITION = true`; `HARNESS_READY = false` até contratos, políticas detalhadas e controles implementados/validados.
