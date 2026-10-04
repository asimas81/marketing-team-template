# System Architecture

## Planos e dados

```text
Agency/Client Web + Client Portal + canais autorizados
                 ↓
Marketing OS API / BFF → Supabase Auth + PostgreSQL/RLS (business state)
          │           → object storage privado (binários, metadata no OS)
          │           → Client Integration executors (Resend, mídia, CRM, analytics)
          ↓
AgentRun + Context Gateway → Eve Lead → especialistas locais/futuros
                                     ↓
                              propostas/artifacts via OS API
```

O Control Plane possui Tenant, Client, membership, policies, Product Context, Domain Pack, Campaign, Request, Artifact, Approval, AgentRun, Audience, Experiment, integrações, Metric, custo, publicação e audit. Eve possui instruções, skills, tools, sessões e execução; recebe apenas um Client por Run. Supabase PostgreSQL e Auth são escolhas alvo do PRD, não serviços conectados neste repositório. RLS complementa a autorização da API para tabelas expostas. Object storage, vault e fila/outbox concretos são decisões abertas.

Agency Dashboard agrega em SQL apenas Clients autorizados. Client Dashboard e Portal consultam o mesmo Control Plane com papéis distintos. Notion é import/export opcional; Resend atual permanece integração operacional legada até que ownership por Client seja reconciliado. Meta/Google/TikTok são conectores planejados, sem contas conectadas. [Arquitetura alvo](../../marketing-management-os/TARGET_ARCHITECTURE.md) e [modelo de domínio](../../marketing-management-os/DOMAIN_MODEL.md) detalham entidades.

OpenTelemetry propaga correlação UI → API → AgentRun/Eve → tool/API → conector. A API reconcilia falhas externas e audita transições. Preview/staging não executa efeitos externos reais por padrão.

Engagement futuro é módulo do Control Plane com `EngagementChannel`, Lead, ChannelIdentity, ConsentRecord, SuppressionEntry, ConversationThread, EngagementEvent e EngagementAction. Email entra primeiro após o core; WhatsApp, SMS, Instagram DM, Facebook Messenger, Web Chat, CRM e Lead Qualification permanecem roadmap. Conectores resolvem capacidade e identidade por Client, enquanto OS verifica consentimento, approval, limite e idempotência antes de cada envio. [Contrato de canal](../contracts/ENGAGEMENT_CHANNEL_CONTRACT.md) detalha a fronteira sem transformar o OS em CRM completo.
