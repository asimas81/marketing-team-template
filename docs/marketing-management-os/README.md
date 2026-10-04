# Artefatos do Marketing Management OS

Este diretório descreve o produto alvo. [PRD](./PRD.md) é a entrada para escopo, requisitos e critérios de aceite. Os documentos de arquitetura e contratos detalham como entregar as capacidades. O código atual contém o lead Eve, sete subagentes e o app de chat; o Marketing OS como system of record e o Creative Studio de geração ainda são alvo de implementação.

| Artefato | Decisão que sustenta |
| --- | --- |
| [AS-IS](./AS-IS.md) | Baseline anterior aos dois novos subagentes e lacunas da aplicação |
| [TARGET_ARCHITECTURE](./TARGET_ARCHITECTURE.md) | Separação control plane / execution plane e stores |
| [DOMAIN_MODEL](./DOMAIN_MODEL.md) | Entidades, versões, ownership e isolamento |
| [AGENT_TOPOLOGY](./AGENT_TOPOLOGY.md) | Lead e sete especialistas; handoffs sequenciais |
| [PRODUCT_CONTEXT_SPEC](./PRODUCT_CONTEXT_SPEC.md) | Verdade do Product, claims e publicação por versão |
| [DOMAIN_PACK_SPEC](./DOMAIN_PACK_SPEC.md) | Conhecimento reutilizável e ativação opcional por Product |
| [DOMAIN_ADVISORY_SPEC](./DOMAIN_ADVISORY_SPEC.md) | Acionamento, estados, evidência e handoff do consultor |
| [CREATIVE_STUDIO_SPEC](./CREATIVE_STUDIO_SPEC.md) | Briefs, sets, assets, variantes, revisão e formatos |
| [CAMPAIGN_MODEL](./CAMPAIGN_MODEL.md) | Objetivos, WorkItems, entregas, tracking e métricas |
| [APPROVAL_MODEL](./APPROVAL_MODEL.md) | Revisão editorial e autorização de execução |
| [AGENT_RUNTIME_CONTRACT](./AGENT_RUNTIME_CONTRACT.md) | API futura entre Marketing OS e Eve |
| [EVAL_PLAN](./EVAL_PLAN.md) | Cenários de fidelidade, segurança e qualidade |
| [MIGRATION_FROM_NOTION](./MIGRATION_FROM_NOTION.md) | Importação e corte da dependência operacional |
| [ROADMAP](./ROADMAP.md) | Ordem de implementação e gates de saída |

Os contratos aqui são propostas para revisão. IDs, estados e campos canônicos devem ser fechados antes de criar APIs persistentes; os subagentes Eve atuais não devem ser usados como prova de que essas APIs já existem.

## Atualização v2 — agência multi-tenant

O [PRD v2](./PRD.md) introduz `AgencyTenant → ClientWorkspace → Product/Brand → Campaign`. Documentos legados usam `Workspace` para a unidade que agora se chama `ClientWorkspace`; as extensões v2 de cada contrato são a referência para novas SPECs. [PRD_ARCHITECTURE_GAP_ANALYSIS](./PRD_ARCHITECTURE_GAP_ANALYSIS.md) compara o PRD com o baseline e [HARNESS_READINESS_REPORT](./HARNESS_READINESS_REPORT.md) distingue prontidão documental de produto operacional.

| Grupo | Artefatos v2 |
| --- | --- |
| Tenancy e papéis | [Agency Multi-Tenancy](./AGENCY_MULTI_TENANCY.md), [Client Workspace](./CLIENT_WORKSPACE_MODEL.md), [RBAC Matrix](./TENANT_RBAC_MATRIX.md), [Offboarding](./CLIENT_OFFBOARDING_MODEL.md) |
| Advisor e integrações | [Client Advisor Profile](./CLIENT_ADVISOR_PROFILE_SPEC.md), [Client Integration](./CLIENT_INTEGRATION_MODEL.md), [Integration Model](./INTEGRATION_MODEL.md), [Channel Connectors](./CHANNEL_CONNECTORS_SPEC.md) |
| UI | [Agency UI Information Architecture](./AGENCY_UI_INFORMATION_ARCHITECTURE.md), [Client Portal](./CLIENT_PORTAL_MODEL.md) |
| Growth loop | [Audience Intelligence](./AUDIENCE_INTELLIGENCE_SPEC.md), [Experimentation](./EXPERIMENTATION_MODEL.md), [Paid Media](./PAID_MEDIA_ARCHITECTURE.md), [Performance](./PERFORMANCE_OPTIMIZATION_MODEL.md), [Learning Loop](./MARKETING_LEARNING_LOOP.md) |

Os arquivos [AGENCY_MULTI_TENANT_ARCHITECTURE_UPDATE](./AGENCY_MULTI_TENANT_ARCHITECTURE_UPDATE.md), [HARNESS_ENGINEERING_MARKETING_MANAGEMENT_OS](./HARNESS_ENGINEERING_MARKETING_MANAGEMENT_OS.md) e [REPOSITORY_UPDATE_INSTRUCTIONS](./REPOSITORY_UPDATE_INSTRUCTIONS.md) são entradas de referência. A implementação continua pendente; o app existente permanece um chat com Eve e sete especialistas.
