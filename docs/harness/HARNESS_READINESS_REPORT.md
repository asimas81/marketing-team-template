# Harness Readiness Report

## Escopo e estado

Esta avaliação executa documentalmente o [Harness Engineering v1.2](../marketing-management-os/HARNESS_ENGINEERING_MARKETING_MANAGEMENT_OS.md). `docs/marketing-management-os/HARNESS_ENGINEERING.md` não existe; foi usada a especificação com sufixo, localizada no mesmo diretório. O repositório ainda é o template Eve com web chat e sete especialistas. O Marketing OS multi-tenant, Supabase, conectores de mídia, AgentRun API e OTel cross-plane são alvo, não funcionalidades existentes. Artefatos do Control Plane e do runtime estão temporariamente neste repositório; não houve split físico.

| Dimensão requerida | Estado | Evidência documental / bloqueio |
| --- | --- | --- |
| Architecture / control-execution boundary | PARTIAL | Constitution e contratos escritos; ADRs aguardam aprovação |
| Control Plane / business state | BLOCKED | Entidades e ownership documentados; aplicação/banco não implementados |
| Execution Plane / Eve / agentes | PARTIAL | Sete especialistas atuais; integração OS e Audience/Paid Media/Performance/Lead Qualification futuros pendentes |
| Agency tenancy / Client isolation / RBAC | BLOCKED | Políticas e matriz definidas; nenhuma prova API/RLS cross-tenant |
| Supabase / Auth / RLS | BLOCKED | Escolha alvo e política; sem projeto, schema, grants ou testes |
| API contract / Agent context | PARTIAL | Contrato lógico v2; formato, transporte, autenticação delegada e versão pendentes |
| Client Advisor | PARTIAL | Profile e boundary genérico; API/evals pendentes |
| Client integrations / portal / offboarding | PARTIAL | Modelos e runbook; vault/OAuth/UX e revogação real pendentes |
| Cross-client analytics | PARTIAL | Regra de agregado autorizado; query/testes pendentes |
| Approval / Artifact / Creative | PARTIAL | Specs e gates; persistência e asset privado pendentes |
| Audience / Experiment / Paid Media / Metrics / Performance | PARTIAL | Modelos; fontes, conta piloto, atribuição e execução não definidas |
| Security / privacy | PARTIAL | Policy, RLS, prompt injection; testes, retenção e vault pendentes |
| OpenTelemetry / audit / cost | PARTIAL | Política e correlação; instrumentação/smoke test pendentes |
| Tools / evals | PARTIAL | Catálogo e políticas; suíte cross-client/contract tests pendente |
| CI/CD / environments | PARTIAL | Políticas e matriz; pipelines/projetos isolados não configurados |
| Engagement Channel / Agentic Email | PARTIAL | Contrato de canal, consentimento e SEND documentados; módulo OS, adapter, listas e testes ausentes |
| Lead model / qualification / CRM handoff | BLOCKED | Entidades e envelope mínimo planejados; agente, CRM, política e evals não existem |
| WhatsApp/SMS/Instagram DM/Messenger/Web Chat | BLOCKED | Capabilities futuras; nenhum provider/credencial/consent policy de canal validado |

## Blockers e próximo passo

Bloqueadores críticos para `HARNESS_READY`: aprovação formal dos ADRs de fronteira e autorização; contrato de identidade delegada/permission envelope; política RLS e testes efetivos entre duas Agencies e dois Clients; vault/integrações client-scoped antes de mídia; ambiente staging seguro; CI/evals de autorização e OTel smoke test. Nenhum desses controles pode ser presumido a partir de texto. `PAID_MEDIA_AUTOMATION_READY = false`.

As SPECs A01/A02 (Agency Tenant, Auth, memberships e RLS) têm escopo e critérios suficientes para começar. SPECs posteriores dependem de decisões em [Open Decisions](./OPEN_DECISIONS.md), contratos fechados e gates do [Spec Readiness Map](./SPEC_READINESS_MAP.md). `SPEC_READINESS = PARTIAL` para o programa completo: fundação pronta para especificação, mídia/otimização ainda dependentes de escolhas e evidências. Próxima ação recomendada: revisar/aceitar Constituição e ADRs 001–003, abrir SPEC-A01/A02 e prototipar autorização com testes cross-tenant antes de qualquer integração real.

`HARNESS_READY = false`

`SPEC_READINESS = PARTIAL`

## Atualização incremental após Product Update Plan

O [Product Update Plan](./MARKETING_OS_PRODUCT_UPDATE_PLAN.md), o [Design System](./MARKETING_OS_DESIGN_SYSTEM.md) e a [direção de protótipo](./MARKETING_OS_PROTOTYPE_INSPIRATION.md) colocam Client Portal e métricas básicas no MVP, Engagement na visão de Client e Agentic Email após o core, antes de Paid Media real. Os demais canais, Lead Qualification e CRM seguem fases posteriores. O [Engagement Channel Contract](./contracts/ENGAGEMENT_CHANNEL_CONTRACT.md) exige ChannelIdentity/ConsentRecord/SuppressionEntry mínimos para Email, sem depender do Lead model completo; define ownership por Client, capabilities e separação `DRAFT/PREPARE/SCHEDULE/SEND/PUBLISH`. Lead/LeadIdentity, ConversationThread e CRM Handoff são futuros. Policies de segurança, aprovação, contexto, OTel, tools, testes e ambiente permanecem válidas.

### NEW_BLOCKERS

- Para Agentic Email no OS: modelo persistente de consentimento e suppression por canal/finalidade, ClientIntegration/identidade de remetente, aprovação de SEND, idempotência por destinatário, reconciliação, limites de taxa, audit e teste cross-client. O Resend legado com gate Eve não satisfaz esses requisitos sozinho.
- Para Lead Qualification/CRM: Lead model, identidade de canal, contexto minimizado, critérios de avaliação evidenciada, permissão de handoff, mapping de campos, consentimento/finalidade e conector testado.
- Para qualquer novo canal: capability e provider reais, política de opt-in/opt-out, inbound/receipt quando aplicável, credenciais por Client, rate limits, ambiente de teste e contrato de segurança revisado.

### FUTURE_GATES

1. SPEC de Engagement Channel + ChannelIdentity/Consent/Suppression mínimos, com decisão de identidade, retenção e finalidade; protótipo de Engagement/Approval conforme Design System. Lead completo é gate futuro separado.
2. SPEC de Agentic Email e adapter piloto client-scoped, com suite de ausência/revogação de consentimento, duplicate-send prevention, retry e webhook deduplicado antes de SEND real.
3. Somente depois, SPEC própria para WhatsApp e Lead Qualification; avaliar CRM handoff com campos mínimos e sync idempotente.
4. SMS, Instagram DM, Facebook Messenger e Web Chat permanecem futuros, cada qual com capability/consent/opt-out/limites validados antes de habilitar.

`HARNESS_READY = false`: os blockers estruturais anteriores e os gates de Engagement continuam sem implementação/validação. `SPEC_READINESS = PARTIAL`: fundação e contrato de canal podem ser especificados; WhatsApp, CRM e Lead Qualification não estão `READY`.
