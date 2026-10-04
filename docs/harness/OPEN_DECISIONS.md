# Open Decisions

Decisões abaixo precisam de owner e ADR/SPEC antes da implementação afetada. `TO_VALIDATE` significa que a arquitetura não fixa comportamento de provider sem teste/documentação específica.

| Tema | Opções/questão | Gate |
| --- | --- | --- |
| Nome e mercado | `AgencyTenant` versus Organization; agência apenas ou marca direta | SPEC-A01 |
| Login e RBAC | Fluxo Auth inicial, revogação de membership, papéis/grants e aprovação dupla | SPEC-A01/A02 |
| Client Portal | MVP ou fase posterior; visibilidade padrão e publicação de relatórios | SPEC-A09 |
| Advisor/Domain | Perfil Client com override Product, packs piloto, remoto e RAG | SPEC-A05/Domain |
| Storage | Vercel Blob privado versus Supabase Storage; rich text e export | Artifact/Creative |
| Eventos | Outbox/queue, retries, streaming/Realtime de AgentRun | AgentRun API |
| Contratos | OpenAPI/JSON Schema/package, generated client, autenticação Eve e trace context | API/Agent Context |
| Ambiente | Staging isolado, vault dinâmico, credenciais OAuth e contas de teste | Client Integration |
| Criativo | Imagem/vídeo/voz/render providers, licença, custo e limite por Run | Creative |
| Audiência | Fontes first-party, consentimento, confidence e validação de Persona | Audience |
| Mídia | Canal piloto, capabilities reais por conta, identidade de campaign/ad/adset e stop rules | Paid Media |
| Métricas | Atribuição MVP, normalização, janela mínima e freshness | Metrics/Performance |
| Verba/JEV | Limites por Agency/Client/Campaign, autoapproval, início de JEV e autoexecução | Budget/Optimization |
| Operação | Retenção, RTO/RPO, custo, observabilidade, alertas e offboarding | Foundation/Operations |
| Engagement Email | Adapter inicial, relação com Resend legado, campaigns/sequences, métricas e identidade de remetente | Engagement Email SPEC |
| Consent e contato | Finalidades, prova de opt-in, expiração, opt-out/suppression, região e retenção por canal | Consent/Engagement SPEC |
| Identidade e threads | Deduplicação do Lead, ChannelIdentity, união entre canais, inbound e permissões de ConversationThread | Lead/Conversation SPEC |
| Envio | Regra de SCHEDULE externo como SEND, volume/frequency cap, idempotency key por destinatário e reconciliação | Engagement Execution SPEC |
| Canais futuros | Ordem e capabilities reais de WhatsApp, SMS, Instagram DM, Messenger e Web Chat; provider/test account | SPEC por canal |
| CRM/qualification | Critérios de qualificação, evidência, campos mínimos de handoff, papel aprovador e mapping CRM | Lead Qualification/CRM SPEC |

Decisões já fixadas: Control Plane separado de execução Eve; Supabase PostgreSQL/Auth/RLS como alvo; OpenTelemetry como padrão; Marketing OS API como fronteira; Product Context/Domain Pack versionados; humano como orquestrador de releases e aprovação inicial de ações externas. Essas decisões não significam que serviços foram conectados.
