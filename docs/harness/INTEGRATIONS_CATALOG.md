# Integrations Catalog

| Integração | Estado | Escopo/owner | Contrato/gate |
| --- | --- | --- | --- |
| Eve + Vercel AI Gateway | Existente no template | Execution Plane | Model/cost policy, AgentRun e trace alvo |
| Vercel Blob | Existente, store legado | Template; ownership OS alvo | Compatibilidade/handoff; storage privado final TO_VALIDATE |
| Notion via Vercel Connect | Existente | Usuário; Client mapping futuro | Import/export opcional, sem SoR |
| Resend via Vercel Connect | Existente | Usuário; Client mapping futuro | Send com gate Eve; business approval OS alvo |
| Slack | Existente | Canal/principal | Vincular principal a Agency/Client antes de mutação OS |
| Supabase Auth/PostgreSQL | Alvo, sem conexão | Control Plane | Auth + RLS + backup/testes |
| OpenTelemetry/Vercel Observability | Alvo, sem instrumentação completa | Ambos os planos | Context propagation, redaction e alertas |
| Meta/Google/TikTok Ads | Alvo, sem conexão | Client Workspace/ExternalAccount | OAuth/vault, capabilities, approval, idempotência |
| CRM/Analytics/Brevo | Alvo, sem conexão | Client Workspace | Consentimento, minimização, import mapping |
| Creative image/video/voice/render | Alvo, provider aberto | Client/Campaign | Cap, direitos, versão e QA |

Toda integração operacional exige registro no ClientIntegration Model, health, reauth/revogação, scope e audit. API e capabilities reais por provider são `TO_VALIDATE`; catálogo não autoriza conectar contas.
