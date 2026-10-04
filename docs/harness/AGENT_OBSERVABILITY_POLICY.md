# Agent Observability Policy

Todo AgentRun registra `agency_id`, `client_workspace_id`, `agent_run_id`, task, especialista, versões de contexto/prompt/modelo, início/fim, status, tokens, custo, tool calls, artifacts, blockers e `trace_id`. Spans cobrem Lead routing, delegação, model call, tool/API e provider; propagar contexto OTel do OS ao Eve e de volta quando o transporte suportar. A forma concreta de propagação é `TO_VALIDATE`.

Não registrar prompt integral, documento privado, token, header ou PII por padrão. Métricas agregadas usam agent/model/status/environment, evitando Agency/Client como label de alta cardinalidade. Run deve aparecer na UI com custo e erro reconciliados; traces protegidos permitem investigação por IDs. Alarmes incluem falha, timeout, custo e tool negada. Ver [OTEL Policy](./observability/OTEL_POLICY.md).

Quando Agentic Email ou Lead Qualification existirem, registrar fase `DRAFT/PREPARE/SCHEDULE/SEND/PUBLISH`, `engagement_action_id`, canal, status de consent/suppression check (sem dados de contato), approval/version, tentativa, provider message ID protegido e resultado reconciliado. `lead_qualification` e `qualification_handoff` correlacionam Run/assessment/CRM handoff sem incluir thread completa ou PII em span. Os nomes de spans futuros seguem [OTEL Policy](./observability/OTEL_POLICY.md); não declarar instrumentação ativa antecipadamente.
