# INTEGRATION_MODEL

## Fronteiras de integração

O Marketing OS é system of record; Eve é execution plane; Supabase PostgreSQL/Auth/RLS são escolhas alvo do Control Plane. O app usa API/BFF para identidade, business state, autorização e auditoria. Eve chama apenas API/SDK do OS com permission envelope verificável, jamais Supabase diretamente. Vercel Blob atual pode suportar compatibilidade de arquivos; escolha final entre Blob e Supabase Storage para assets privados permanece aberta. Notion é import/export opcional. Resend, Brevo, CRM, Analytics e mídia são conectados por Client Workspace conforme [CLIENT_INTEGRATION_MODEL](./CLIENT_INTEGRATION_MODEL.md).

Contratos cross-plane carregam `contract_version`, `agency_id`, `client_workspace_id`, `product_id?`, `campaign_id?`, `agent_run_id`, `requested_by`, recursos/ações permitidos, versões de contexto e `trace_id`. O Control Plane cria AgentRun antes de invocar Eve, recebe eventos e persiste artifacts/advisories mediante API com idempotência. Aprovação de negócio vive no OS; gate Eve protege o commit operacional quando aplicável. Publicação e gasto usam ExternalAction com snapshot/hash e reconciliação. Contratos canônicos futuros pertencem ao Control Plane, publicados em formato versionado para o runtime; formato de cliente gerado permanece decisão aberta.

Instrumentação OpenTelemetry correlaciona UI, API, AgentRun, tool call, AI Gateway, storage e conector. Eventos de negócio/outbox, transporte assíncrono, vault dinâmico, propagação de identidade Eve, ambiente staging e contratos de webhook são `TO_VALIDATE` antes das SPECs respectivas. A API deve negar cross-agency/client, inclusive por service account, e nunca expor credenciais ao modelo.
