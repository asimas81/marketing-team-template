# Agent Readiness Report

Estado atual: Lead e sete especialistas descobertos pelo template, com gates legados de Notion/Resend e chat web. Product/Domain Specialist e Creative Producer retornam texto revisável; Marketing OS API, AgentRun persistido, contexto Client, artifacts canônicos, Audience/Paid/Performance e observabilidade cross-plane não estão conectados.

| Gate | Estado |
| --- | --- |
| Skills/instruções e descoberta Eve atuais | PARTIAL: validar em CI antes de release |
| Contexto Agency/Client versionado | BLOCKED: Control Plane/API ausente |
| Permission envelope e tools OS | BLOCKED: contrato lógico apenas |
| Aprovação de negócio + gate Eve | PARTIAL: gate Eve legado existe; OS approval não |
| Evals cross-client e prompt injection | BLOCKED: política definida, suite futura |
| OTel/custo por AgentRun | BLOCKED: instrumentação futura |

`AGENT_RUNTIME_READY_FOR_OS = false`. O runtime atual pode servir como baseline para SPECs, não como prova de Marketing OS operacional. Próximo gate: contrato API/contexto e testes de isolamento em ambiente seguro, sem alterar agentes nesta execução.

Atualização Engagement: o agente `email` existente continua com Resend e gates Eve, mas não possui Campaign/Sequence/Consent/Lead/Thread do OS. Lead Qualification Agent não existe. WhatsApp, SMS, Instagram DM, Facebook Messenger, Web Chat e CRM connectors não foram configurados. Evals e permissions futuros estão documentados; `AGENTIC_EMAIL_OS_READY = false` e `LEAD_QUALIFICATION_READY = false`. Próximo gate para o primeiro: Client ownership, consent/suppression, approval SEND, adapter e idempotência. Para o segundo: Lead model, contexto mínimo, evidência de qualificação, política de contato e handoff CRM autorizado.
