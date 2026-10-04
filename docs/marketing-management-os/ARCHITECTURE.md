# AGENCY_MULTI_TENANT_ARCHITECTURE_UPDATE.md

# Marketing Management OS — Atualização Arquitetural para Agência Multi-Tenant

**Versão:** 1.0  
**Status:** READY_FOR_ARCHITECTURE_UPDATE

---

# MISSÃO

Atualize a arquitetura existente do Marketing Management OS para refletir o modelo de produto descrito no PRD v2.0:

```text
Agency Tenant
↓
Client Workspace
↓
Product / Brand
↓
Campaign
```

O produto deve operar como plataforma para agência gerenciar múltiplos clientes com isolamento completo.

Não implemente código nesta tarefa.

---

# 1. DOCUMENTOS DE ENTRADA

Leia:

- `PRD_MARKETING_MANAGEMENT_OS_AGENCY_MULTI_TENANT.md`;
- `HARNESS_ENGINEERING_MARKETING_MANAGEMENT_OS.md`;
- `MARKETING_OS_PRODUCT_DOMAIN_AND_CREATIVE_SPECIALISTS.md`;
- `MARKETING_OS_AUDIENCE_PAID_MEDIA_ARCHITECTURE_UPDATE.md`;
- tudo em `docs/marketing-management-os/`.

---

# 2. DOCUMENTOS EXISTENTES A ATUALIZAR

Atualize quando existirem:

- `TARGET_ARCHITECTURE.md`;
- `DOMAIN_MODEL.md`;
- `AGENT_TOPOLOGY.md`;
- `PRODUCT_CONTEXT_SPEC.md`;
- `DOMAIN_PACK_SPEC.md`;
- `CAMPAIGN_MODEL.md`;
- `APPROVAL_MODEL.md`;
- `INTEGRATION_MODEL.md`;
- `MIGRATION_FROM_NOTION.md`;
- `ROADMAP.md`;
- `AUDIENCE_INTELLIGENCE_SPEC.md`;
- `PAID_MEDIA_ARCHITECTURE.md`;
- `EXPERIMENTATION_MODEL.md`;
- `PERFORMANCE_OPTIMIZATION_MODEL.md`;
- `CHANNEL_CONNECTORS_SPEC.md`;
- `MARKETING_LEARNING_LOOP.md`.

Não alterar `AS-IS.md` para fingir que o novo modelo já existe. Se necessário, apenas adicionar nota de que representa a arquitetura anterior.

---

# 3. NOVOS DOCUMENTOS A CRIAR

Crie:

- `AGENCY_MULTI_TENANCY.md`;
- `CLIENT_WORKSPACE_MODEL.md`;
- `CLIENT_ADVISOR_PROFILE_SPEC.md`;
- `CLIENT_INTEGRATION_MODEL.md`;
- `TENANT_RBAC_MATRIX.md`;
- `AGENCY_UI_INFORMATION_ARCHITECTURE.md`;
- `CLIENT_PORTAL_MODEL.md`;
- `CLIENT_OFFBOARDING_MODEL.md`.

---

# 4. DOMAIN MODEL

Adicionar:

```text
AgencyTenant
AgencyMembership
ClientWorkspace
ClientWorkspaceMembership
ClientPolicy
AdvisorProfile
ClientIntegration
ExternalAccount
```

Relacionar com:

```text
Product
ProductContext
DomainPack
Campaign
Artifact
Approval
AgentRun
Audience
Persona
Experiment
Metric
```

---

# 5. CLIENT ADVISOR

Cada Client Workspace pode possuir Advisor Profile.

O Advisor Profile usa o agente genérico `product-domain-specialist`.

Não criar código de agente por cliente.

Permitir futuramente Remote Agent específico.

---

# 6. INTEGRATIONS

Meta, Google, TikTok, CRM, Resend, Brevo e Analytics devem ser escopados ao Client Workspace.

Documentar:

- OAuth;
- token reference;
- external account mapping;
- permissions;
- revocation;
- health;
- reauth;
- audit.

---

# 7. WEB UI

Atualizar arquitetura para possuir duas perspectivas:

## Agency View
- dashboard consolidado;
- clients;
- approvals;
- agent runs;
- performance;
- alerts.

## Client Workspace View
- dashboard;
- requests;
- products;
- audiences;
- campaigns;
- content;
- creatives;
- experiments;
- paid media;
- performance;
- approvals;
- agents;
- integrations;
- reports.

---

# 8. CLIENT PORTAL

Planejar Client Portal com roles:

```text
Client Admin
Client Approver
Client Reviewer
Client Viewer
```

O portal não é outro banco/sistema.

É outra surface sobre o mesmo Control Plane.

---

# 9. PAID MEDIA

Todas as contas e external IDs devem ter ownership de Client Workspace.

Nenhum campaign external mapping pode existir sem client owner.

---

# 10. CROSS-CLIENT ANALYTICS

Agency Dashboard pode agregar clientes autorizados.

Preferir SQL/analytics para agregação.

LLM apenas explica ou interpreta agregados.

---

# 11. ROADMAP

Atualizar roadmap para garantir que tenancy e client isolation aconteçam antes de paid media real.

Sequência mínima:

```text
Agency Tenant
↓
Membership / RBAC
↓
Client Workspace
↓
Client Policy
↓
Product Context / Domain
↓
Campaign / Artifact / Approval
↓
Agent Run
↓
Audience / Creative
↓
Client Integrations
↓
Paid Media
↓
Metrics / Performance
↓
Optimization
```

---

# 12. CRITÉRIO DE SAÍDA

Ao concluir:

```text
AGENCY_MULTI_TENANT_ARCHITECTURE_READY = true | false
```

Liste blockers.

Não implemente código.
