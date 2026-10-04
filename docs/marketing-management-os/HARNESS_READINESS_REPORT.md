# HARNESS_READINESS_REPORT

## Avaliação em 2026-10-04

Este relatório separa prontidão documental para decompor SPECs de prontidão do produto/harness para implementação ou produção. A atualização é somente arquitetural. Nenhum código, schema, conector, agente ou ambiente foi criado aqui.

| Dimensão | Estado | Evidência e próximo gate |
| --- | --- | --- |
| Architecture boundary | PARTIAL | Control Plane/Eve e Agency/Client descritos; aprovar contratos canônicos e decisões abertas |
| Agency tenancy / client isolation / client RBAC | PARTIAL | Modelos e matriz definidos; Supabase Auth/RLS, API e testes de cross-tenant pendentes |
| Client Advisor | PARTIAL | Perfil e binding genérico especificados; schema/API/evals de isolamento pendentes |
| Client integrations / offboarding | PARTIAL | Ownership e ciclo de vida descritos; vault, OAuth, revogação e runbook executável pendentes |
| Agency/Client UI e Client Portal | PARTIAL | IA e papéis descritos; protótipos/validação e endpoints pendentes |
| Cross-client analytics | PARTIAL | Regra de agregado autorizado definida; queries/definições/testes pendentes |
| Supabase / RLS | BLOCKED | Escolha alvo no PRD; sem conexão, migrations ou policies implementadas nesta tarefa |
| API / Agent context / Eve | PARTIAL | Envelope v2 documentado; transporte, autenticação delegada e contract tests pendentes |
| Audience / Creative / Experiment | PARTIAL | Modelos definidos; sources/providers, storage, UX e evals pendentes |
| Paid Media / Metrics / Performance | PARTIAL | Conectores client-scoped e guardrails definidos; atribuição, capabilities por provider e imports pendentes |
| Approvals / budget | PARTIAL | Snapshot/dual gate/policy definidos; matrizes finais, limites e execução pendentes |
| OpenTelemetry / audit / cost | PARTIAL | Correlação/redação/custos definidos; instrumentação, alertas e retenção pendentes |
| CI/CD / security / environments | BLOCKED | Harness de referência requer políticas e testes específicos; não produzidos como implementação nesta tarefa |

`HARNESS_READY = false`. `PAID_MEDIA_AUTOMATION_READY = false`. Falhas críticas de isolamento entre Agency ou Client impedem qualquer operação real. Nenhuma seção deste diretório constitui evidência de integração ativa com Supabase ou plataforma de anúncios.

## Readiness para SPEC decomposition

`REPOSITORY_READY_FOR_SPEC_DECOMPOSITION = true`: hierarquia, ownership, fronteiras, contratos conceituais, UX surface, sequência e gates estão definidos o suficiente para criar SPECs A01–A10 e as SPECs de Audience, Creative, Experiment, Paid Media, Metrics, Performance, OTel e migração. Cada SPEC deve fechar decisões locais, produzir critérios verificáveis, separar Control Plane/runtime, prever ambiente seguro e testes de autorização/RLS/evals. A primeira SPEC recomendada é Agency Tenant + memberships/RBAC, seguida de Client Workspace/Policy, antes de conectar qualquer mídia real.

O detalhamento documental do Harness está em [docs/harness/HARNESS_READINESS_REPORT](../harness/HARNESS_READINESS_REPORT.md). Ele mantém `HARNESS_READY = false` e avalia o programa completo como `SPEC_READINESS = PARTIAL`: SPECs de fundação podem começar, enquanto integrações e otimização exigem decisões e gates adicionais.
