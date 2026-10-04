# REPOSITORY_UPDATE_INSTRUCTIONS.md

# Pacote de Atualização — Marketing Management OS v2.0

Use este arquivo como prompt no Arquiteto/Codex do repositório.

---

# MISSÃO

Aplicar ao repositório apenas as atualizações de arquitetura e documentação necessárias para evoluir o Marketing Management OS para:

```text
MULTI-TENANT AGENCY OPERATING SYSTEM
```

com:

- Agency Tenants;
- Client Workspaces;
- Advisor por cliente/produto;
- integrações de mídia por cliente;
- interface Web de gestão;
- Audience Intelligence;
- Creative Studio;
- Paid Media;
- Experiments;
- Performance;
- approvals;
- Agent Runs;
- client portal.

---

# ARQUIVOS DE REFERÊNCIA

Leia integralmente:

1. `PRD_MARKETING_MANAGEMENT_OS_AGENCY_MULTI_TENANT.md`
2. `HARNESS_ENGINEERING_MARKETING_MANAGEMENT_OS.md`
3. `AGENCY_MULTI_TENANT_ARCHITECTURE_UPDATE.md`
4. `MARKETING_OS_PRODUCT_DOMAIN_AND_CREATIVE_SPECIALISTS.md`
5. `MARKETING_OS_AUDIENCE_PAID_MEDIA_ARCHITECTURE_UPDATE.md`

Também leia toda a documentação atual em:

`docs/marketing-management-os/`

---

# O QUE FAZER

1. Comparar o PRD v2.0 com a arquitetura atual.
2. Produzir gap analysis.
3. Atualizar documentos existentes sem apagar decisões válidas.
4. Criar os novos documentos exigidos por `AGENCY_MULTI_TENANT_ARCHITECTURE_UPDATE.md`.
5. Atualizar roadmap.
6. Atualizar Domain Model.
7. Atualizar Agent Topology.
8. Atualizar Approval Model.
9. Atualizar Integration Model.
10. Atualizar UI Information Architecture.
11. Atualizar Harness Readiness.

---

# O QUE NÃO FAZER

Não:

- implementar código;
- criar migrations;
- conectar Supabase;
- conectar Meta;
- conectar Google;
- conectar TikTok;
- alterar agentes Eve;
- criar secrets;
- fazer deploy;
- fazer commit;
- fazer push.

Esta tarefa é somente de arquitetura e documentação.

---

# VALIDAÇÕES OBRIGATÓRIAS

Confirme explicitamente que a arquitetura final contempla:

- isolamento entre Agencies;
- isolamento entre Clients;
- RBAC em dois níveis;
- Advisor Profile por cliente/produto;
- integrações client-scoped;
- Agency Dashboard;
- Client Dashboard;
- Client Portal;
- Requests;
- Agent Runs;
- Creative Studio;
- Audience Intelligence;
- Campaign Management;
- Paid Media;
- Experimentation;
- Performance;
- Approval Inbox;
- Publications;
- Reports;
- Metrics normalization;
- Budget policies;
- OpenTelemetry;
- Supabase Auth/RLS;
- Eve execution plane.

---

# SAÍDA

Criar:

`docs/marketing-management-os/PRD_ARCHITECTURE_GAP_ANALYSIS.md`

e finalizar com:

```text
REPOSITORY_ARCHITECTURE_UPDATE_COMPLETED

Updated:
- ...

Created:
- ...

Critical blockers:
- ...

Implementation-ready capabilities:
- ...

Capabilities still requiring decisions:
- ...

REPOSITORY_READY_FOR_SPEC_DECOMPOSITION = true | false
```
