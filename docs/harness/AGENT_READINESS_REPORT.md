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
