# ARCHITECTURE — Marketing Management OS

## Posicionamento e fontes

O produto é uma **Agentic Marketing Operations Platform for Agencies**. O [PRD](./PRD.md) define escopo e critérios de produto. O [Product Update Plan](../harness/MARKETING_OS_PRODUCT_UPDATE_PLAN.md) registra as decisões recentes e sua prioridade; o [Design System](../harness/MARKETING_OS_DESIGN_SYSTEM.md) é a referência canônica de UX/UI; a [Prototype Inspiration](../harness/MARKETING_OS_PROTOTYPE_INSPIRATION.md) é a referência oficial de prototipação, sem copiar concorrentes. Esta página é o mapa funcional canônico; as especificações vinculadas detalham cada domínio. Regras de segurança, contexto, execução, observabilidade e governança ficam em [docs/harness](../harness/README.md).

## Mapa do produto alvo

```text
Web UI principal: Agency View / Client Workspace View / Client Portal
  └─ Marketing OS Control Plane: identidade, tenancy, produto, campanha,
     engagement, entregáveis, aprovação, métricas, aprendizado e auditoria
      ├─ System of record: dados estruturados + assets privados versionados
      ├─ Context Gateway → Eve / Marketing Lead → especialistas
      └─ Client Integrations → Email primeiro; mídia e outros canais por fase
```

`AgencyTenant → ClientWorkspace → Product/Brand → Campaign` é a hierarquia de ownership. Toda operação de cliente, incluindo Campaign, AgentRun, Engagement, Lead futuro, Artifact, Approval e ExternalAction, resolve escopo e permissão no Control Plane. O OS detém estado de negócio, versões e decisões. Eve executa trabalho cognitivo e retorna propostas/artefatos; provedores externos executam ações autorizadas. Notion é interoperabilidade opcional, nunca system of record. O [Target Architecture](./TARGET_ARCHITECTURE.md), [Domain Model](./DOMAIN_MODEL.md) e [Integration Model](./INTEGRATION_MODEL.md) detalham essas fronteiras.

## Superfícies e capacidades

A Web UI concentra trabalho diário da agência e dos clientes. Agency View agrega somente clientes autorizados; Client Workspace View organiza Requests, Products, Audiences, Campaigns, Content, Creative Studio, Engagement, Experiments, Performance, Approvals e Integrations; Client Portal expõe ações e resultados permitidos. Chat/Marketing Lead aparece como utilidade contextual na tela, não como homepage. A [arquitetura da informação](./AGENCY_UI_INFORMATION_ARCHITECTURE.md) organiza as vistas.

O ciclo operacional é `research → plan → create → review → publish/execute → measure → optimize → learn`. [Campaign](./CAMPAIGN_MODEL.md) une objetivo, público, trabalho, entregas e resultados. [Engagement](./ENGAGEMENT_ARCHITECTURE.md) introduz `EMAIL`, `WHATSAPP`, `SMS`, `INSTAGRAM_DM`, `FACEBOOK_MESSENGER` e `WEB_CHAT` como contrato de canal; somente Email é a primeira implementação planejada. [Agentic Email](./AGENTIC_EMAIL_MARKETING_SPEC.md) cobre broadcasts, sequences, segments, templates, experiments, automations, performance e recomendações. [Lead Qualification](./LEAD_QUALIFICATION_MODEL.md) é evolução futura, com handoff para CRM externo; o OS não assume pipeline de vendas.

## Sequência e disponibilidade

A base multi-tenant, versões, aprovações e UI precede execução externa. Client Portal e métricas entram cedo; Email segue o core e é o primeiro canal de Engagement. WhatsApp, Lead Qualification, demais canais e conectores CRM ficam em roadmap, com gates próprios. Meta/Google/TikTok começam por leitura/planejamento e só depois execução controlada. O [Roadmap](./ROADMAP.md) define dependências. Esta documentação descreve alvo, não disponibilidade no código atual: o repositório ainda contém o app web de chat e o time Eve existente.
