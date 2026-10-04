# HARNESS_ENGINEERING_MARKETING_MANAGEMENT_OS.md

# Marketing Management OS — Harness Engineering Specification

**Versão:** 1.2 — Agency Multi-Tenant, Client Workspaces & Client-Scoped Integrations  
**Status:** READY_FOR_HARNESS_EXECUTION  
**Escopo:** Marketing Management OS + Marketing Agents  
**Arquitetura:** Control Plane + Execution Plane  
**Cloud principal:** Vercel  
**Agent runtime:** Eve  
**System of Record:** Supabase/PostgreSQL  
**Identity:** Supabase Auth  
**Observabilidade:** OpenTelemetry + Vercel Observability  
**Model Access:** Vercel AI Gateway  
**IDE principal:** Zed  
**Coordenação experimental:** Delta  
**Processo de desenvolvimento:** Spec Kit + Git + PR + CI/CD  
**Objetivo:** transformar a arquitetura do Marketing Management OS em um Harness de engenharia e de comportamento agentic seguro, rastreável, observável e independente de segmento.

---

# 1. MISSÃO

Atue como **Harness Architect / Harness Engineer** responsável por estruturar o ambiente completo de engenharia e execução do Marketing Management OS.

O sistema possui dois planos arquiteturais independentes:

```text
MARKETING MANAGEMENT OS
= CONTROL PLANE
= SYSTEM OF RECORD
= BUSINESS ORCHESTRATION

MARKETING AGENTS
= EXECUTION PLANE
= EVE RUNTIME
= COGNITIVE ORCHESTRATION
```

Sua missão é definir como esses dois planos:

- são desenvolvidos;
- se comunicam;
- são testados;
- são versionados;
- são observados;
- são protegidos;
- são implantados;
- executam agentes;
- controlam contexto;
- controlam permissões;
- controlam aprovações;
- preservam isolamento entre Workspaces;
- preservam rastreabilidade entre campanha, agente, artefato, decisão e resultado.

O Harness deve permitir que o produto evolua para diferentes segmentos sem reescrever o time de agentes.

---

# 2. REGRA ARQUITETURAL FUNDAMENTAL

A seguinte regra é obrigatória:

```text
AGENTS NEVER OWN BUSINESS STATE.

MARKETING OS ALWAYS OWNS BUSINESS STATE.
```

Marketing Agents podem:

```text
READ
ANALYZE
RECOMMEND
DRAFT
PREPARE
GENERATE
```

conforme permissões.

Marketing Agents NÃO devem utilizar memória de sessão como fonte oficial de:

- Workspace;
- Product;
- Campaign;
- Product Context;
- Domain Pack;
- Artifact;
- Approval;
- Budget;
- Metrics;
- Integration State;
- Billing;
- Permission;
- Business Decision.

O Marketing Management OS é sempre a fonte oficial desses estados.

---

# 3. PRINCÍPIO DO HARNESS

O Harness não é um prompt.

O Harness é:

```text
RULES
+
CONTEXT
+
TOOLS
+
PERMISSIONS
+
CONTRACTS
+
STATE BOUNDARIES
+
TESTS
+
EVALS
+
OBSERVABILITY
+
SECURITY
+
APPROVALS
+
FEEDBACK
+
GOVERNANCE
+
HUMAN CONTROL
```

O objetivo do Harness é permitir que:

- humanos;
- agentes de desenvolvimento;
- agentes Eve;
- modelos diferentes;
- integrações externas;

operem o sistema sem perder:

- coerência;
- segurança;
- qualidade;
- previsibilidade;
- privacidade;
- isolamento;
- auditabilidade;
- controle humano.

---

# 4. PRINCÍPIO — O SISTEMA DEFINE OS LIMITES

Arquitetura de decisão:

```text
DETERMINISTIC RULES
→ invariantes e regras obrigatórias

JEV
→ decisão estruturada entre opções permitidas, quando aplicável

EVE
→ runtime agentic, tools, workflows, subagents, schedules e execução

RAG / DOMAIN KNOWLEDGE
→ conhecimento recuperado e autorizado

LLM
→ compreensão, análise, linguagem e geração

CREATIVE MODELS
→ imagem, vídeo, voz e outras mídias

HUMAN
→ decisões críticas e aprovações
```

Nenhum LLM deve possuir autoridade para:

- alterar autorização;
- alterar saldo;
- movimentar budget;
- alterar Product Context aprovado;
- alterar Domain Pack aprovado;
- ignorar Approval Policy;
- publicar quando publicação exige aprovação;
- enviar campanha sem permissão;
- modificar credencial;
- bypassar RLS;
- alterar política de segurança.

---

# 5. REPOSITÓRIOS

A arquitetura alvo deve considerar dois repositórios principais.

---

## 5.1 Repositório 1 — `marketing-management-os`

Responsável pelo Control Plane.

Deve possuir:

```text
apps/
domain/
application/
database/
contracts/
integrations/
observability/
docs/
```

Responsabilidades:

- Workspace;
- User;
- Membership;
- Product;
- Product Context Pack;
- Domain Pack;
- Campaign;
- Campaign Task;
- Artifact;
- Creative Asset metadata;
- Creative Brief;
- Creative Set;
- Creative Variant;
- Approval;
- Agent Run;
- Metrics;
- Experiment;
- Integration;
- Business Events;
- Audit;
- Business Orchestration;
- Marketing Management UI.

---

## 5.2 Repositório 2 — `marketing-agents`

Baseado no repositório atual de Marketing Team com Eve.

Responsável pelo Execution Plane.

Deve possuir:

```text
agent/
skills/
tools/
connections/
subagents/
evals/
policies/
docs/
```

Responsabilidades:

- Marketing Lead;
- Product Marketer;
- Product & Domain Specialist;
- Content Marketer;
- Creative Producer;
- Social Media Coordinator;
- SEO;
- Email;
- futuros Paid Media;
- futuros Performance;
- futuros Optimization Agents;
- agent instructions;
- skills;
- agent-specific tools;
- evals;
- execution policies.

---

# 6. NÃO CRIAR TERCEIRO REPOSITÓRIO AGORA

Não criar inicialmente um terceiro repositório apenas para contratos.

Preferir:

```text
marketing-management-os/contracts/
```

como fonte canônica dos contratos.

O `marketing-agents` deve consumir:

- OpenAPI;
- JSON Schema;
- generated TypeScript client;
- package versionado;
- ou outro mecanismo explícito.

A estratégia final deve minimizar drift entre os repositórios.

Um terceiro repositório poderá ser criado no futuro somente se:

- contratos tiverem lifecycle independente;
- múltiplos consumidores externos surgirem;
- versionamento independente gerar valor comprovado.

---

# 7. STACK LOCKED / PREFERRED

Considere inicialmente:

## LOCKED

```text
Vercel
Eve
Vercel AI Gateway
Supabase PostgreSQL
Supabase Auth
OpenTelemetry
Git
GitHub
Zed
Spec Kit
```

## PREFERRED

```text
Next.js
TypeScript
Vercel Sandbox
Vercel Blob para compatibilidade/handoff quando necessário
Supabase Realtime quando houver valor comprovado
Playwright
```

## TO_VALIDATE

```text
Vercel Blob vs Supabase Storage para Creative Assets
Supabase Realtime para Agent Run streaming
queue/event implementation
JEV integration point
creative model providers
video providers
domain-pack retrieval strategy
RAG storage strategy
```

Não transforme item `TO_VALIDATE` em decisão silenciosamente.

---

# 8. VERCEL — PAPEL NA ARQUITETURA

Vercel deverá atuar como plataforma principal de aplicação e agent runtime.

Utilizar quando aplicável:

- Next.js hosting;
- Preview Deployments;
- Vercel Functions;
- AI Gateway;
- Vercel Sandbox;
- Vercel Observability;
- OpenTelemetry collector/integration;
- Vercel OIDC;
- Vercel Connect quando útil;
- deployment do Eve;
- deployment do Marketing OS.

Nunca acoplar regra de negócio a uma capacidade específica da Vercel sem adapter/abstração quando essa dependência for crítica.

---

# 9. VERCEL AI GATEWAY

Vercel AI Gateway é a camada padrão de acesso a modelos.

Objetivos:

- desacoplar modelos de regras de negócio;
- permitir múltiplos provedores;
- permitir fallback;
- permitir observabilidade;
- controlar custo;
- trocar modelo por capability;
- aplicar política de routing.

Definir:

```text
MODEL POLICY
```

por capability.

Exemplos:

```text
marketing-lead
product-marketer
domain-specialist
content
seo
email
creative-text
creative-image
creative-video
performance-analysis
```

Não fixar toda a solução em um único modelo.

---

# 10. VERCEL SANDBOX

Vercel Sandbox deverá ser considerado para execução isolada quando agentes precisarem:

- manipular arquivos;
- processar documentos;
- executar scripts;
- renderizar conteúdo;
- gerar build temporário;
- executar código não confiável;
- validar outputs.

Sandbox não deve receber automaticamente:

- production database credentials;
- service-role keys;
- billing credentials;
- secrets globais.

Use:

```text
LEAST PRIVILEGE
+
EGRESS CONTROL
+
SHORT-LIVED EXECUTION
```

quando aplicável.

---

# 11. SUPABASE — SYSTEM OF RECORD

Supabase PostgreSQL será o System of Record do Marketing Management OS.

Responsável por persistir:

- workspaces;
- memberships;
- products;
- product context versions;
- domain packs;
- campaigns;
- campaign tasks;
- artifacts;
- artifact versions;
- creative briefs;
- creative sets;
- creative assets metadata;
- creative variants;
- approvals;
- agent runs;
- agent events;
- advisories;
- metrics;
- experiments;
- integrations metadata;
- audit events.

---

# 12. SUPABASE AUTH

Supabase Auth será a identidade padrão do Marketing OS.

Definir suporte conforme necessidade para:

- email/password;
- magic link;
- OTP;
- OAuth;
- SSO futuro.

O Auth ID nunca deve ser usado sozinho como autorização de negócio.

Authorization depende de:

```text
authenticated user
+
workspace membership
+
role
+
resource ownership/policy
```

---

# 13. SUPABASE RLS

Row Level Security é obrigatória para tabelas expostas à aplicação.

Todo recurso tenant-aware deve possuir:

```text
workspace_id
```

quando aplicável.

RLS deve garantir:

```text
USER A
cannot access
WORKSPACE B
```

mesmo que:

- altere ID na URL;
- altere payload;
- tente acesso direto à Data API.

Criar testes de RLS.

Não considerar RLS correto apenas porque a policy existe.

Testar casos:

```text
ALLOW
DENY
cross-workspace
cross-product
cross-campaign
admin
viewer
editor
```

---

# 14. SERVICE ROLE

Credenciais com poder de bypass de RLS devem ser consideradas de alto risco.

Regras:

- nunca expor no browser;
- nunca passar ao LLM;
- nunca passar a subagent;
- nunca logar;
- nunca inserir em prompt;
- nunca armazenar em Artifact.

Uso permitido apenas em componentes server-side explicitamente autorizados.

Toda operação privilegiada deve possuir:

- policy;
- audit;
- reason;
- caller identity;
- scope.

---

# 15. MODELO MULTI-TENANT

A unidade principal de isolamento é:

```text
Workspace
```

Estrutura:

```text
Workspace
├── Members
├── Products
│   ├── Product Context
│   ├── Domain Pack links
│   └── Campaigns
└── Integrations
```

Nenhum agente decide autorização entre Workspaces.

Regra:

```text
MODEL INPUT
≠
AUTHORIZATION SOURCE
```

Authorization é resolvida no Marketing OS.

---

# 16. MODELO DE DADOS CONCEITUAL

Avaliar pelo menos as entidades:

```text
User
Workspace
WorkspaceMembership
Product
ProductContextVersion
DomainPack
DomainPackVersion
ProductDomainLink
Campaign
CampaignTask
CampaignBrief
Artifact
ArtifactVersion
ApprovalRequest
ApprovalDecision
AgentRun
AgentRunEvent
DomainAdvisory
ProductContextChangeProposal
DomainPackChangeProposal
CreativeBrief
CreativeSet
CreativeAsset
CreativeVariant
CreativeExperiment
CampaignMetric
MetricSnapshot
Integration
IntegrationConnection
AuditEvent
BusinessEvent
```

Não criar schema final antes de validar dependências.

---

# 17. BUSINESS STATE

Marketing OS é dono de:

```text
Campaign Status
Task Status
Artifact Status
Approval Status
Budget
Metrics
Product Context
Domain Context
Integration State
Agent Run State
```

Eve não pode substituir o banco como fonte de verdade.

---

# 18. AGENT RUN

Toda execução agentic iniciada pelo Marketing OS deve possuir:

```text
agent_run_id
```

Fluxo:

```text
Marketing OS
↓
Create AgentRun = QUEUED
↓
invoke Eve
↓
AgentRun = RUNNING
↓
events
↓
artifacts / advisory
↓
AgentRun = SUCCEEDED | FAILED | NEEDS_REVIEW
```

AgentRun deve ser persistido antes da execução externa.

---

# 19. IDEMPOTÊNCIA

Operações que possam ser repetidas devem possuir idempotency key.

Especialmente:

- Agent Run invocation;
- external publishing;
- email send;
- campaign launch;
- budget change;
- webhook processing;
- asset generation;
- payment/billing futuro;
- metric imports.

---

# 20. OUTBOX / BUSINESS EVENTS

Avaliar adoção de Outbox Pattern para eventos de negócio.

Exemplo:

```text
Campaign Approved
↓
DB transaction
├── campaign.status = APPROVED
└── outbox event = CAMPAIGN_APPROVED
↓
processor
↓
agent / integration / workflow
```

Objetivo:

- evitar estado salvo sem side effect;
- evitar side effect sem estado salvo;
- permitir retry;
- permitir audit.

Implementação concreta é `TO_VALIDATE`.

---

# 21. EVE — PAPEL

Eve é o runtime do Execution Plane.

Responsabilidades:

- Marketing Lead;
- subagents;
- tools;
- skills;
- sessions;
- schedules quando aprovados;
- human-in-the-loop operacional;
- execution orchestration;
- tool calling.

Eve não é:

- banco principal;
- authorization source;
- campaign state store;
- metrics store;
- approval system of record.

---

# 22. MARKETING LEAD

Marketing Lead é o orquestrador cognitivo.

Marketing OS decide:

```text
WHAT NEEDS TO HAPPEN
```

Marketing Lead decide:

```text
WHICH SPECIALIST
+
WHAT CONTEXT
+
WHAT EXECUTION SEQUENCE
```

O Lead deve receber preferencialmente:

```text
workspace_id
product_id
campaign_id
agent_run_id
task_type
artifact_id
permission envelope
```

e carregar contexto via tools.

---

# 23. TEAM INITIAL

Arquitetura inicial do Execution Plane:

```text
Marketing Lead
├── Product Marketer
├── Product & Domain Specialist
├── Audience Intelligence / Persona Research
├── Content Marketer
├── Creative Producer
├── Social Media Coordinator
├── SEO
└── Email
```

Segunda wave, após Control Plane, Campaign, Metrics e Experimentation estarem prontos:

```text
├── Paid Media Strategist
└── Performance Optimizer
```

Terceira wave, somente após guardrails, histórico e evals suficientes:

```text
└── Budget / Optimization capability
```

Meta, Google e TikTok devem começar como **connectors/tools de canal**, não como agentes separados. Um agente por canal só deve surgir se houver ganho claro de segurança, especialização, credenciais ou ciclo de release independente.

Audience Intelligence deve entrar antes de Paid Media porque melhora segmentação, criativos, conteúdo, targeting e experimentação em todos os canais.

---

# 24. PRODUCT & DOMAIN SPECIALIST

O Harness deve reconhecer o contrato consolidado do Product & Domain Specialist.

Função:

```text
PRODUCT TRUTH
+
DOMAIN KNOWLEDGE
+
DOMAIN CONSTRAINTS
↓
ADVISORY
```

Não pode:

- publicar;
- enviar;
- gastar;
- alterar Product Context diretamente;
- alterar Domain Pack diretamente;
- escrever no banco diretamente.

Pode:

- ler contexto;
- produzir advisory;
- propor alteração;
- levantar risk flag.

---

# 25. CREATIVE PRODUCER

O Harness deve reconhecer o Creative Producer.

Responsável por transformar:

```text
STRATEGY
+
CONTENT
+
PRODUCT CONTEXT
+
DOMAIN GUIDANCE
+
BRAND
+
CHANNEL REQUIREMENTS
```

em:

```text
VERSIONED CREATIVE ARTIFACTS
```

Tipos:

- images;
- carousels;
- ads;
- banners;
- product books;
- catalogs;
- e-books;
- decks;
- landing pages;
- videos;
- reels;
- shorts;
- creative kits;
- variants.

---

# 26. CREATIVE TOOLS

Creative Producer deve trabalhar por capabilities.

Evitar um agente por formato.

Preferir:

```text
Creative Producer
+
Image Generation Tool
+
Video Generation Tool
+
Document Renderer
+
Landing Page Renderer
+
Asset Manager
```

Provider deve ser abstraído.

---

# 27. PRODUCT CONTEXT PACK

Product Context Pack pertence ao Marketing OS.

Deve ser:

- versionado;
- auditável;
- aprovável;
- recuperável por API;
- referenciado por Agent Run.

Nenhum agente pode manter uma versão paralela escondida como fonte oficial.

---

# 28. DOMAIN PACK

Domain Pack pertence ao Marketing OS.

Deve ser:

- versionado;
- associado a Product;
- opcional por padrão;
- obrigatório quando Workspace Policy exigir;
- auditável;
- aprovável.

---

# 29. CONTEXT ENGINEERING

Nunca enviar o Workspace inteiro para um agente.

Contrato de contexto:

```text
TASK
+
PRODUCT CONTEXT
+
CAMPAIGN CONTEXT
+
DOMAIN GUIDANCE IF NEEDED
+
RELEVANT ARTIFACTS
+
USER INSTRUCTION
+
PERMISSION ENVELOPE
```

Cada agente deve receber apenas o contexto necessário.

---

# 30. CONTEXT CONTRACT

Criar documento formal:

```text
AGENT_CONTEXT_CONTRACT.md
```

Definir:

- required ids;
- optional ids;
- context loading order;
- max sizes;
- allowed sources;
- version refs;
- redaction;
- sensitive fields;
- stale-context rules;
- failure behavior.

---

# 31. MARKETING OS API

Marketing Agents nunca acessam Supabase diretamente.

Fluxo obrigatório:

```text
marketing-agents
↓
Marketing OS API / SDK
↓
authentication
↓
authorization
↓
application/domain layer
↓
Supabase
```

Objetivos:

- centralizar policy;
- centralizar audit;
- evitar service-role leakage;
- reduzir coupling;
- permitir evolução independente.

---

# 32. TOOLS DO MARKETING OS

Planejar tools equivalentes a:

```text
get_workspace_policy
get_product_context
get_domain_pack
get_campaign
get_campaign_brief
get_campaign_metrics
get_artifact
list_relevant_artifacts
create_artifact
create_domain_advisory
create_creative_artifact
create_creative_variant
submit_for_review
raise_risk_flag
propose_product_context_change
propose_domain_pack_change
update_agent_run_event
```

Tools devem encapsular a API.

---

# 33. PERMISSION ENVELOPE

Toda execução agentic deve receber autorização explícita.

Exemplo conceitual:

```yaml
permissions:
  read:
    product_context: true
    campaign: true
    artifacts: true
    metrics: false

  write:
    artifacts: true
    advisories: true
    campaign: false

  external:
    publish: false
    send: false
    spend: false
    delete: false
```

Agente não pode auto-elevar permissão.

---

# 34. APPROVAL MODEL

Marketing OS é a fonte da verdade das aprovações de negócio.

Eve aplica enforcement operacional quando aplicável.

Separar:

```text
READ
DRAFT
RECOMMEND
PREPARE
EXECUTE
PUBLISH
SEND
SPEND
DELETE
```

Padrão inicial:

```text
READ
DRAFT
RECOMMEND
PREPARE
→ may be automatic

PUBLISH
SEND
SPEND
DELETE
→ human approval
```

---

# 35. DUAL APPROVAL MODEL

Pode haver duas camadas:

```text
Marketing OS Approval
= business authorization

Eve Approval
= runtime enforcement
```

A segunda não substitui a primeira.

---

# 36. NOTION

Notion deve ser tratado como:

```text
OPTIONAL INTEGRATION
```

Nunca:

```text
SYSTEM OF RECORD
```

Nenhum agente deve depender de Notion para acessar:

- Product Context;
- Campaign State;
- Artifact State;
- Approval State.

---

# 37. ARTIFACT MODEL

Todo output relevante deve virar Artifact.

Tipos possíveis:

```text
strategy
brief
content
social_post
seo_audit
email
domain_advisory
creative_brief
creative_asset
landing_page
product_book
video
performance_report
```

Artifact deve ser:

- versionado;
- atribuído a Agent Run;
- relacionado a Campaign;
- revisável;
- aprovável.

---

# 38. CREATIVE ASSET STORAGE

Decisão inicial:

```text
Structured metadata
→ Supabase

Binary assets
→ TO_VALIDATE
```

Avaliar:

```text
Vercel Blob
vs
Supabase Storage
```

Critérios:

- segurança;
- acesso privado;
- signed access;
- integração com Vercel;
- integração com RLS;
- custo;
- tamanho;
- CDN;
- lifecycle;
- versionamento;
- migração do template existente.

Não utilizar dois storages sem motivo claro.

---

# 39. RAG E KNOWLEDGE

Caso Domain Pack ou outros materiais cresçam:

avaliar RAG.

Supabase possui PostgreSQL e pode suportar `pgvector`.

Mas:

```text
RAG IS NOT DEFAULT
```

Só usar quando:

- volume justificar;
- recuperação lexical/estruturada for insuficiente;
- evals comprovarem valor.

---

# 40. JEV

JEV permanece camada opcional para decisões estreitas.

Exemplo futuro de Performance:

```text
INCREASE_BUDGET
KEEP
REDUCE
PAUSE
INVESTIGATE
```

Antes do JEV:

```text
DETERMINISTIC PRECONDITIONS
```

Depois do JEV:

```text
DETERMINISTIC POSTCONDITIONS
```

JEV nunca pode alterar budget sem Policy + Approval.

---

# 41. OBSERVABILIDADE — OPEN TELEMETRY

OpenTelemetry é o padrão de instrumentação.

Criar observabilidade distribuída entre:

```text
marketing-management-os
marketing-agents
Eve
AI Gateway
Supabase calls
external integrations
creative providers
```

Usar propagação de contexto quando possível.

---

# 42. SERVICE NAMES

Definir nomes consistentes.

Sugestão:

```text
marketing-os-web
marketing-os-api
marketing-agents
marketing-agents-creative
marketing-integrations
```

Evitar cardinalidade excessiva.

Não criar service name por usuário/campaign.

---

# 43. TRACE CORRELATION

Toda operação importante deve permitir correlação com:

```text
trace_id
agent_run_id
workspace_id
product_id
campaign_id
artifact_id
approval_id
```

Não registrar dado pessoal sensível como atributo indiscriminadamente.

---

# 44. SPANS IMPORTANTES

Criar spans para:

```text
HTTP request
auth resolution
workspace authorization
database query
agent run
lead routing
subagent delegation
tool call
marketing-os-api call
AI Gateway call
JEV decision
RAG retrieval
creative generation
external integration call
approval check
artifact persistence
publish/send/spend action
```

---

# 45. AI TELEMETRY

Registrar quando aplicável:

```text
model
provider
prompt/instruction version
agent id
agent version
tokens
latency
tool calls
retry
fallback
cost
finish reason
```

Não registrar prompt completo por padrão quando puder conter informação sensível.

Preferir:

- hashes;
- versions;
- ids;
- sampled/redacted content.

---

# 46. CREATIVE TELEMETRY

Para imagens/vídeos/documentos:

```text
provider
model
brief_id
variant_id
duration
cost
size
generation status
review result
approval status
```

---

# 47. OBSERVABILITY REDACTION

Nunca enviar para trace/log:

- password;
- access token;
- refresh token;
- service role key;
- API secret;
- full auth headers;
- private user content sem necessidade;
- payment secrets.

Criar redaction policy.

---

# 48. VERCEL OBSERVABILITY

OpenTelemetry deve integrar com Vercel Observability.

Quando necessário, utilizar Vercel OTEL collector / Drains para encaminhar traces.

Não tornar a arquitetura dependente de dashboard específico.

O padrão de instrumentação deve continuar sendo OpenTelemetry.

---

# 49. ALERTING

Definir alertas para:

- agent failure rate;
- external integration failure;
- database errors;
- authorization failures;
- RLS deny spikes;
- publish/send failures;
- AI Gateway failures;
- cost anomaly;
- creative generation failure;
- queue backlog;
- agent run timeout.

---

# 50. SECURITY PRINCIPLE

Aplicar:

```text
LEAST PRIVILEGE
ZERO TRUST BETWEEN PLANES
DEFENSE IN DEPTH
```

O Execution Plane deve ser tratado como sistema externo ao banco.

---

# 51. SECRETS

Nunca colocar secret em:

- prompt;
- Artifact;
- Git;
- markdown;
- trace;
- log;
- eval fixture.

Segredos devem existir apenas em:

- Vercel Environment;
- Vercel Connect;
- Supabase secure configuration;
- secret manager apropriado.

---

# 52. PROMPT INJECTION

Tudo que tools retornam é:

```text
DATA
```

não:

```text
SYSTEM INSTRUCTION
```

Product Context, Domain Pack, Campaign Brief, Artifact e conteúdo importado podem conter texto malicioso.

O agente não pode permitir que conteúdo externo altere:

- system prompt;
- permission envelope;
- approval model;
- tool allowlist;
- authorization.

---

# 53. NETWORK POLICY

Tools com acesso de rede devem ser explicitamente catalogadas.

Para cada:

- destination;
- purpose;
- auth;
- data sent;
- data returned;
- approval;
- retry;
- rate limit.

Vercel Sandbox deve aplicar egress control quando necessário.

---

# 54. AGENT ROLES — HARNESS DE ENGENHARIA

Definir pelo menos:

## Harness Architect

Responsável por:

- arquitetura;
- contracts;
- governance;
- cross-repo boundaries;
- security policies;
- CI/CD policy;
- observability policy.

## Marketing OS Developer

Responsável por:

- Control Plane;
- domain;
- UI;
- Supabase;
- APIs;
- integrations.

## Agent Runtime Developer

Responsável por:

- Eve;
- subagents;
- skills;
- tools;
- agent evals.

## Reviewer

Responsável por:

- code review;
- spec compliance;
- tests;
- integration.

## Security Reviewer

Responsável por:

- RLS;
- secrets;
- permissions;
- auth;
- data exposure.

## AI Behavior Reviewer

Responsável por:

- agent behavior;
- tool use;
- context handling;
- prompt injection;
- evals.

---

# 55. HUMAN ORCHESTRATOR

No início:

```text
ORCHESTRATOR = HUMAN
```

Humano controla:

- quando iniciar feature;
- quando aprovar architecture decision;
- quando abrir PR;
- quando mergear;
- quando publicar;
- quando autorizar ação crítica.

Automação aumenta apenas depois de evidência.

---

# 56. CONTEXT POLICY PARA DEV AGENTS

Harness Architect:

```text
full architecture
cross-repo contracts
ADRs
security
harness
```

Marketing OS Developer:

```text
spec
domain
relevant schema
API contract
UI requirement
DoD
```

Agent Runtime Developer:

```text
spec
agent contract
relevant skills/tools
API client contract
eval requirements
DoD
```

Reviewer:

```text
spec
diff
tests
CI
relevant ADRs
```

---

# 57. SPEC KIT

Spec Kit é o fluxo padrão.

```text
CONSTITUTION
↓
SPECIFY
↓
CLARIFY
↓
PROTOTYPE when UX
↓
PLAN
↓
TASKS
↓
IMPLEMENT
```

Toda feature cross-repo deve explicitar:

- repo ownership;
- contract changes;
- migration order;
- compatibility window.

---

# 58. UX GATE

Toda SPEC com impacto relevante em UX exige:

```text
PROTOTYPE_SPEC
+
VALIDATION
```

antes de implementação.

Especialmente:

- Dashboard;
- Campaign Management;
- Creative Workspace;
- Approval Inbox;
- Product Context editor;
- Domain Pack editor;
- Agent Runs;
- Metrics Dashboard.

---

# 59. GIT STRATEGY

Cada repositório possui:

```text
main
```

protegida.

Fluxo:

```text
spec
↓
branch
↓
worktree when useful
↓
implementation
↓
commit
↓
PR
↓
CI
↓
review
↓
approval
↓
merge
```

---

# 60. CROSS-REPO FEATURE STRATEGY

Feature que afeta os dois repositórios deve ter:

```text
FEATURE ID
```

comum.

Exemplo:

```text
MMOS-007-agent-context-api
```

Branches podem ser:

```text
feature/MMOS-007-agent-context-api
```

em ambos.

---

# 61. CONTRACT-FIRST

Para features cross-repo:

```text
CONTRACT
↓
CONTROL PLANE IMPLEMENTATION
↓
CLIENT / MOCK
↓
EXECUTION PLANE IMPLEMENTATION
↓
CONTRACT TEST
↓
E2E
```

Não desenvolver ambos com suposições diferentes.

---

# 62. API VERSIONING

Marketing OS API deve possuir estratégia de versionamento.

Mudança breaking deve:

- ser explicitamente identificada;
- possuir migration plan;
- atualizar generated client;
- executar contract tests.

---

# 63. CI — MARKETING MANAGEMENT OS

Pipeline mínimo:

```text
install
lint
typecheck
unit tests
domain tests
build
Supabase migration validation
RLS tests
integration tests
Playwright critical flows
security scan
secret scan
```

---

# 64. SUPABASE CI

CI deve validar:

- migrations;
- schema;
- RLS;
- grants;
- seed safety;
- function permissions.

Quando possível:

```text
supabase test db
```

ou mecanismo equivalente.

Não aplicar migration de produção a partir de ambiente não autorizado.

---

# 65. CI — MARKETING AGENTS

Pipeline mínimo:

```text
install
lint
typecheck
eve discovery
pnpm validate
agent contract tests
tool tests
evals
security checks
build
```

Confirmar que:

- agentes esperados são descobertos;
- tools esperadas são descobertas;
- connection surface não aumentou acidentalmente;
- destructive tools continuam gated.

---

# 66. CONTRACT TESTS

Criar testes entre:

```text
Marketing OS API
↔
Marketing Agents Client
```

Cobrir:

- auth;
- workspace isolation;
- Product Context version;
- Domain Pack version;
- Artifact creation;
- Agent Run events;
- approval behavior.

---

# 67. E2E CROSS-REPO

Fluxo mínimo:

```text
User
↓
creates Campaign
↓
requests strategy
↓
AgentRun created
↓
Eve invoked
↓
Product Marketer executes
↓
Artifact persisted
↓
UI shows result
↓
Human approves
```

Outro:

```text
Approved content
↓
Creative Producer
↓
Creative Asset
↓
Review
↓
Approval
```

---

# 68. EVALS — AGENTS

Cada agente deve possuir dataset mínimo.

Product Marketer:
- positioning;
- messaging;
- claim discipline.

Domain Specialist:
- product truth;
- domain rule;
- uncertainty;
- claims.

Content:
- brief adherence;
- factuality;
- brand.

Creative:
- brief adherence;
- brand;
- format;
- safety.

Social:
- platform fit.

SEO:
- grounded recommendations.

Email:
- compliance;
- deliverability prep;
- content fidelity.

---

# 69. REGRESSION EVALS

Toda mudança em:

- model;
- instructions;
- skills;
- tools;
- Product Context schema;
- Domain Pack schema;
- permission policy;
- approval policy;

deve executar regressão.

---

# 70. PERFORMANCE / PAID MEDIA FUTURO

Não implementar agora.

Quando chegar:

```text
Marketing OS Metrics
↓
Performance Agent
↓
Rules
↓
JEV if appropriate
↓
Recommendation
↓
Approval
↓
Paid Media Connector
```

Budget continua sendo estado determinístico do Control Plane.

---

# 71. DEPLOYMENT TOPOLOGY

Inicialmente:

```text
Vercel Project A
marketing-management-os

Vercel Project B
marketing-agents
```

Separação recomendada para:

- lifecycle independente;
- credentials;
- blast radius;
- deployments;
- cost visibility.

---

# 72. SUPABASE PROJECT

Supabase deve possuir ambientes separados quando viável.

Pelo menos:

```text
development
production
```

Preferível:

```text
development
staging
production
```

Nunca usar dados de produção indiscriminadamente em dev.

---

# 73. VERCEL ENVIRONMENTS

Utilizar:

```text
Development
Preview
Production
```

Preview deve apontar para ambiente seguro.

Não permitir Preview usar service role de produção.

---

# 74. ENVIRONMENT MATRIX

Criar:

```text
ENVIRONMENT_MATRIX.md
```

Para cada ambiente:

- Vercel Project;
- Supabase Project/branch;
- AI Gateway access;
- Eve endpoint;
- integrations;
- email behavior;
- publishing behavior;
- secrets;
- observability;
- allowed destructive actions.

---

# 75. PREVIEW POLICY

Preview Deployments:

- nunca publicam campanha real por padrão;
- nunca enviam email real por padrão;
- nunca movimentam budget real;
- usam sandbox/test integrations;
- usam mock quando necessário.

---

# 76. CD

Deploy para Preview pode ser automático.

Deploy para Production exige:

```text
CI GREEN
+
SECURITY GREEN
+
MIGRATION SAFE
+
EVALS GREEN
+
HUMAN APPROVAL
```

quando aplicável.

---

# 77. MIGRATION POLICY

Database migration deve possuir:

- forward plan;
- rollback/mitigation;
- compatibility period;
- data migration test;
- RLS validation.

Evitar migration destrutiva imediata.

---

# 78. OBSERVABILITY SMOKE TEST

Após deploy validar:

- trace chegando;
- service name correto;
- trace correlation;
- DB span;
- agent span;
- AI span;
- tool span;
- no secret leakage.

---

# 79. AUDIT LOG

Audit Event deve registrar:

```text
actor
workspace
action
resource
resource_id
timestamp
result
reason
trace_id
```

Ações de alto impacto obrigatórias:

- approval;
- publish;
- send;
- spend;
- delete;
- Product Context approval;
- Domain Pack approval;
- permission change;
- integration connect/disconnect.

---

# 80. BUSINESS METRICS

Separar:

```text
Operational Metrics
AI Metrics
Marketing Metrics
Business Metrics
```

Não misturar campaign KPIs com runtime observability.

---

# 81. FAILURE MODEL

Criar política para:

- Supabase unavailable;
- Eve unavailable;
- AI Gateway unavailable;
- model timeout;
- tool failure;
- asset generation failure;
- Vercel deployment issue;
- Resend failure;
- Brevo failure;
- external channel failure.

Cada falha precisa definir:

```text
detect
timeout
retry
fallback
user message
audit
alert
recovery
```

---

# 82. CIRCUIT BREAKER / RETRY

Retries devem ser limitados.

Não repetir automaticamente:

- spend;
- publish;
- send;
- delete;

sem idempotência garantida.

---

# 83. COST GOVERNANCE

Rastrear custo por:

```text
Workspace
Product
Campaign
AgentRun
Agent
Model
Creative Generation
```

Criar budget guardrails para IA/creative generation.

---

# 84. CREATIVE COST

Creative models podem gerar custo alto.

Definir:

- per-run budget;
- variant limit;
- video limit;
- approval before expensive render, quando necessário.

---

# 85. DATA RETENTION

Definir retenção para:

- Agent Runs;
- Traces;
- Logs;
- Artifacts;
- Creative Assets;
- Metrics;
- Audit;
- User Content.

Retention deve respeitar:

- necessidade operacional;
- privacidade;
- requisitos legais;
- custo.

---

# 86. DELETE POLICY

Deletion deve diferenciar:

```text
soft archive
hard delete
legal retention
audit preservation
```

Não usar hard delete indiscriminado.

---

# 87. BACKUP / RECOVERY

Definir:

- Supabase backup strategy;
- restoration procedure;
- migration rollback;
- asset recovery strategy;
- RTO/RPO alvo.

---

# 88. TOOLS CATALOG

Criar catálogo com:

```text
Tool
Owner
Plane
Purpose
Read
Write
External Side Effect
Approval
Credentials
Environment
Fallback
Audit
```

---

# 89. INTEGRATIONS CATALOG

Catalogar:

- Vercel;
- Supabase;
- Eve;
- AI Gateway;
- OpenTelemetry;
- Resend;
- Brevo;
- Notion optional;
- creative providers;
- social/ad networks future.

---

# 90. PERMISSIONS MATRIX

Criar matriz explícita por agente e role.

Exemplo:

```text
Marketing Lead
read product: yes
write artifact: conditional
publish: no
spend: no

Creative Producer
read campaign: yes
write creative: yes
publish: no

Domain Specialist
read context: yes
write advisory: yes
modify context: no
```

---

# 91. DEFINITION OF DONE

Feature só está concluída quando aplicável:

```text
SPEC PASS
+
CONTRACT PASS
+
UNIT TESTS PASS
+
INTEGRATION TESTS PASS
+
TYPECHECK PASS
+
LINT PASS
+
BUILD PASS
+
RLS TEST PASS
+
SECURITY PASS
+
EVALS PASS
+
OTEL PRESENT
+
DOCS UPDATED
+
REVIEW PASS
+
CI GREEN
+
PREVIEW VALIDATED
```

---

# 92. ARCHITECTURE DECISIONS

Criar ADR para decisões estruturais.

Pelo menos avaliar ADRs para:

```text
Control Plane / Execution Plane split
Supabase as System of Record
Supabase Auth + RLS
Marketing OS API boundary
Eve runtime boundary
Agent Context Contract
Artifact model
Creative asset storage
OpenTelemetry observability
AI Gateway model routing
Approval model
Product Context / Domain Pack versioning
```

---

# 93. HARNESS STRUCTURE — CONTROL PLANE

No `marketing-management-os` criar:

```text
docs/harness/
  constitution/
  architecture/
  context/
  contracts/
  development/
  git/
  ci/
  cd/
  security/
  observability/
  permissions/
  runbooks/
  definition-of-done/
  readiness/
```

---

# 94. HARNESS STRUCTURE — EXECUTION PLANE

No `marketing-agents` criar:

```text
docs/harness/
  agent-behavior/
  context/
  tools/
  permissions/
  evals/
  observability/
  security/
  runbooks/
  readiness/
```

---

# 95. DELIVERABLES — CROSS-SYSTEM

Produzir no Control Plane:

```text
docs/harness/HARNESS_CONSTITUTION.md
docs/harness/architecture/SYSTEM_ARCHITECTURE.md
docs/harness/architecture/CONTROL_EXECUTION_BOUNDARY.md
docs/harness/architecture/AGENT_RUNTIME_TOPOLOGY.md
docs/harness/contracts/AGENT_CONTEXT_CONTRACT.md
docs/harness/contracts/MARKETING_OS_AGENT_API.md
docs/harness/context/CONTEXT_POLICY.md
docs/harness/security/SECURITY_POLICY.md
docs/harness/security/SUPABASE_RLS_POLICY.md
docs/harness/observability/OTEL_POLICY.md
docs/harness/permissions/PERMISSIONS_MATRIX.md
docs/harness/development/DEVELOPMENT_FLOW.md
docs/harness/git/GIT_STRATEGY.md
docs/harness/git/WORKTREE_POLICY.md
docs/harness/ci/CI_POLICY.md
docs/harness/cd/CD_POLICY.md
docs/harness/definition-of-done/DEFINITION_OF_DONE.md
docs/harness/runbooks/RUNBOOK.md
docs/harness/ENVIRONMENT_MATRIX.md
docs/harness/TOOLS_CATALOG.md
docs/harness/INTEGRATIONS_CATALOG.md
docs/harness/OPEN_DECISIONS.md
docs/harness/HARNESS_READINESS_REPORT.md
```

---

# 96. DELIVERABLES — AGENT RUNTIME

Produzir no repositório `marketing-agents`:

```text
docs/harness/AGENT_BEHAVIOR_POLICY.md
docs/harness/AGENT_CONTEXT_POLICY.md
docs/harness/AGENT_PERMISSIONS.md
docs/harness/TOOL_POLICY.md
docs/harness/APPROVAL_ENFORCEMENT_POLICY.md
docs/harness/AGENT_OBSERVABILITY_POLICY.md
docs/harness/EVALS_POLICY.md
docs/harness/PROMPT_INJECTION_POLICY.md
docs/harness/AGENT_RUNBOOK.md
docs/harness/AGENT_READINESS_REPORT.md
```

---

# 97. SPEC READINESS MAP

Criar:

```text
docs/harness/SPEC_READINESS_MAP.md
```

Mapear futuras specs.

Primeira wave sugerida:

```text
SPEC-001 Marketing OS Foundation
SPEC-002 Supabase Auth + Workspace RLS
SPEC-003 Product Context
SPEC-004 Domain Pack
SPEC-005 Campaign Core
SPEC-006 Artifact + Approval
SPEC-007 Creative Core
SPEC-008 Marketing Management UI
SPEC-009 Agent Run API
SPEC-010 Eve Context Integration
SPEC-011 Product & Domain Specialist
SPEC-012 Creative Producer
SPEC-013 OpenTelemetry End-to-End
SPEC-014 Audience Intelligence Core
SPEC-015 Persona / Segment Evidence Model
SPEC-016 Experimentation Core
```

Segunda wave sugerida:

```text
SPEC-017 Paid Media Abstraction
SPEC-018 Meta Ads Connector
SPEC-019 Google Ads Connector
SPEC-020 TikTok Ads Connector
SPEC-021 Campaign Metrics Normalization
SPEC-022 Performance Optimizer
SPEC-023 Recommendations + Approval
```

Terceira wave, somente após histórico e guardrails:

```text
SPEC-024 Budget Optimization Policy
SPEC-025 JEV Bounded Optimization
SPEC-026 Controlled Auto-Execution
```

Não aceitar essa decomposição cegamente.

Revisar dependências reais.

---

# 98. IMPLEMENTATION SEQUENCE

Criar:

```text
docs/harness/IMPLEMENTATION_SEQUENCE.md
```

Derivar sequência por dependências.

Não começar agents integration antes de:

- Workspace isolation;
- Product Context;
- Campaign;
- Artifact;
- AgentRun;
- API contract.

---

# 99. READINESS STATUS

Avaliar:

```text
ARCHITECTURE
CONTROL_PLANE
EXECUTION_PLANE
SUPABASE
AUTH
RLS
API_CONTRACT
EVE
AGENTS
CONTEXT
APPROVALS
ARTIFACTS
CREATIVE
CI
CD
SECURITY
OTEL
EVALS
TOOLS
INTEGRATIONS
ENVIRONMENTS
COST
PRIVACY
```

Status:

```text
READY
PARTIAL
BLOCKED
```

---

# 100. HARNESS READY

Use:

```text
HARNESS_READY = true
```

somente quando:

- architecture boundary está aprovada;
- Supabase strategy está definida;
- RLS strategy está definida;
- API boundary está definida;
- Agent Context Contract está definido;
- permissions estão definidas;
- approval model está definido;
- CI/CD policies estão definidas;
- OpenTelemetry policy está definida;
- agent eval policy está definida;
- no critical security blocker remains.

Caso contrário:

```text
HARNESS_READY = false
```

Isso não é falha.

É readiness real.

---

# 101. NÃO IMPLEMENTAR NESTA EXECUÇÃO

Nesta execução:

NÃO:

- criar aplicação;
- criar tabela;
- executar migration;
- instalar pacote;
- conectar Supabase;
- modificar agentes Eve;
- criar integração externa;
- configurar produção;
- fazer deploy;
- criar secrets;
- publicar;
- enviar emails.

Esta execução produz o Harness e readiness.

Implementação virá por Specs.

---

# 102. NÃO FAZER GIT AUTOMÁTICO

Não executar:

- commit;
- push;
- merge;
- rebase;
- branch delete.

Produzir arquivos e relatório.

---

# 103. VALIDAR DOCUMENTAÇÃO ATUAL

Antes de afirmar capacidade específica de:

- Vercel;
- Eve;
- Supabase;
- OpenTelemetry;

consultar documentação oficial disponível.

Não inventar APIs.

Quando comportamento depender de versão:

registrar versão.

Quando não confirmado:

marcar:

```text
TO_VALIDATE
```

---

# 104. REVISAR ARQUITETURA EXISTENTE

Antes de produzir o Harness, ler integralmente:

```text
docs/marketing-management-os/
```

e qualquer arquivo equivalente a:

```text
TARGET_ARCHITECTURE.md
DOMAIN_MODEL.md
AGENT_TOPOLOGY.md
PRODUCT_CONTEXT_SPEC.md
DOMAIN_PACK_SPEC.md
CAMPAIGN_MODEL.md
APPROVAL_MODEL.md
MIGRATION_FROM_NOTION.md
ROADMAP.md
```

Também ler o documento consolidado:

```text
MARKETING_OS_PRODUCT_DOMAIN_AND_CREATIVE_SPECIALISTS.md
```

se existir.

---

# 105. REVISAR REPOSITÓRIO ATUAL DE AGENTES

Ler:

```text
README.md
AGENTS.md
docs/ARCHITECTURE.md
agent/
apps/web/
package.json
```

Preservar:

- Eve;
- Marketing Lead;
- especialistas existentes;
- approval gates;
- web channel;
- compatibility quando útil.

Não reescrever o template sem necessidade.

---

# 106. MIGRAÇÃO GRADUAL

Notion e Blob atuais podem permanecer temporariamente.

Migração deve ser gradual.

Exemplo:

```text
Current Brand Context
↓
Product Context adapter
↓
new Product Context API
```

Não realizar big-bang migration.

---

# 107. OPEN DECISIONS OBRIGATÓRIAS

No mínimo avaliar:

1. Vercel Blob ou Supabase Storage para Creative Assets?
2. Supabase Realtime é necessário para UI de Agent Runs?
3. Qual mecanismo de Business Events/Outbox?
4. Qual auth flow inicial?
5. Qual contract format entre repos?
6. Como versionar generated client?
7. Como Eve recebe identity/permission envelope?
8. Como propagar trace context até Eve?
9. Como rastrear AI Gateway calls?
10. Como mapear Supabase RLS para Workspace roles?
11. Como limitar AgentRun cost?
12. Como implementar staging isolado?
13. Como realizar creative provider abstraction?
14. Quando JEV entra?
15. Quando Domain Pack exige RAG?
16. Qual é o modelo canônico de Audience Segment vs Persona?
17. Quais fontes de pesquisa podem criar evidência de persona?
18. Como calcular e versionar confidence sem transformá-la em verdade?
19. Como conectar CRM/customer data com consentimento e minimização?
20. Como normalizar métricas entre Meta, Google e TikTok?
21. Qual modelo de atribuição será usado no MVP?
22. Qual identidade canônica de campaign/ad/adset/asset entre canais?
23. Como modelar A/B tests cross-channel vs experimentos nativos da plataforma?
24. Quais stop rules são determinísticas?
25. Qual janela mínima de dados permite recomendação de performance?
26. Qual limite máximo de alteração de budget por execução?
27. Quando uma recomendação pode ser autoexecutada?
28. Como lidar com APIs de ads quando uma capability não estiver disponível para a conta?
29. Como armazenar tokens OAuth das plataformas com least privilege e rotação?
30. Quando Paid Media deve ser um agente único e quando um canal merece agente separado?

---

# 108. OUTPUT FINAL

Ao concluir, responder:

```text
HARNESS ENGINEERING EXECUTION COMPLETED

Architecture:
READY | PARTIAL | BLOCKED

Control Plane:
READY | PARTIAL | BLOCKED

Execution Plane:
READY | PARTIAL | BLOCKED

Supabase:
READY | PARTIAL | BLOCKED

RLS:
READY | PARTIAL | BLOCKED

Eve:
READY | PARTIAL | BLOCKED

OpenTelemetry:
READY | PARTIAL | BLOCKED

Agent Contracts:
READY | PARTIAL | BLOCKED

Artifacts created:
- ...

ADRs proposed:
- ...

Critical decisions:
- ...

Open decisions:
- ...

Security blockers:
- ...

Cross-repo blockers:
- ...

SPEC_READINESS:
READY | PARTIAL | BLOCKED

HARNESS_READY = true | false

NEXT RECOMMENDED ACTION:
- ...
```

---

# 109. REGRA FINAL

O sistema final deve permitir:

```text
Marketing Management OS
↓
owns business truth
↓
requests work
↓
Marketing Agents / Eve
↓
produce advice, content and creatives
↓
Marketing OS
↓
persists, reviews, approves and measures
↓
performance feedback
↓
next decision
```

A arquitetura deve continuar funcionando mesmo se:

- o modelo mudar;
- o agente mudar;
- Eve evoluir;
- o provider de imagem mudar;
- Notion for removido;
- um novo segmento for adicionado.

O Harness está correto quando:

```text
PRODUCT CONTEXT
+
DOMAIN PACK
```

podem mudar sem exigir reescrever o Marketing Team genérico.

---

# 110. INÍCIO DA EXECUÇÃO

Comece agora por:

1. ler toda a arquitetura existente em `docs/marketing-management-os/`;
2. ler `MARKETING_OS_PRODUCT_DOMAIN_AND_CREATIVE_SPECIALISTS.md`;
3. ler `README.md`, `AGENTS.md` e `docs/ARCHITECTURE.md`;
4. mapear o estado atual do repositório;
5. identificar decisões já aprovadas e decisões ainda abertas;
6. validar capacidades atuais de Vercel, Eve, Supabase e OpenTelemetry na documentação oficial;
7. produzir todos os artefatos do Harness;
8. finalizar com `HARNESS_READINESS_REPORT.md`.

Não implemente código nesta execução.

---

# 111. AUDIENCE INTELLIGENCE / PERSONA RESEARCH

O Harness passa a reconhecer **Audience Intelligence** como capability central e como subagente Eve recomendado antes da expansão para Paid Media.

Objetivo:

```text
PRODUCT CONTEXT
+
DOMAIN PACK
+
MARKET RESEARCH
+
CUSTOMER RESEARCH
+
SEARCH / SOCIAL SIGNALS
+
HISTORICAL CAMPAIGNS
+
CRM / FIRST-PARTY DATA WHEN AUTHORIZED
↓
AUDIENCE INTELLIGENCE
↓
SEGMENTS
+
PERSONAS
+
TARGETING HYPOTHESES
+
EVIDENCE
```

O agente NÃO deve "inventar persona".

Toda conclusão relevante deve carregar:

```text
source
evidence_type
confidence
status
last_validated_at
```

---

# 112. AUDIENCE INTELLIGENCE ROLE

Responsabilidades:

- pesquisar mercado;
- identificar padrões de audiência;
- propor segmentos;
- propor personas;
- distinguir fato de hipótese;
- mapear dores, objetivos, objeções e canais;
- identificar linguagem utilizada pelo mercado;
- propor targeting hypotheses;
- comparar persona com performance real;
- revisar persona após novos dados.

Não pode:

- criar targeting discriminatório proibido;
- tratar inferência como fato;
- publicar campanha;
- alterar budget;
- modificar Product Context sem approval;
- usar dados pessoais sem autorização.

---

# 113. AUDIENCE DATA MODEL

Adicionar ao Domain Model:

```text
AudienceResearch
AudienceResearchSource
AudienceSegment
AudienceSegmentVersion
Persona
PersonaVersion
PersonaEvidence
TargetingHypothesis
MarketingHypothesis
AudienceExperiment
```

Persona deve ser um artefato versionado e evidenciado.

Exemplo conceitual:

```yaml
persona:
  id:
  version:
  product_id:
  segment_id:
  name:
  context:
  goals:
  barriers:
  objections:
  media_behavior:
  triggers:
  status:

  evidence:
    - source:
      type:
      confidence:
      observed_at:
```

---

# 114. EVIDENCE POLICY

Classificar evidência como:

```text
FIRST_PARTY_DECLARED
FIRST_PARTY_BEHAVIORAL
CRM_DATA
CAMPAIGN_PERFORMANCE
CUSTOMER_INTERVIEW
SURVEY
SEARCH_SIGNAL
SOCIAL_SIGNAL
PUBLIC_RESEARCH
EXTERNAL_REPORT
AGENT_INFERENCE
```

Hierarquia deve favorecer first-party e dados observados.

`AGENT_INFERENCE` nunca pode ser promovida automaticamente a fato.

---

# 115. PERSONA STATUS

Estados sugeridos:

```text
DRAFT
HYPOTHESIS
TESTING
VALIDATED
NEEDS_REVIEW
DEPRECATED
```

`VALIDATED` exige evidência definida por policy.

Não existe "persona validada" apenas porque um LLM a escreveu.

---

# 116. MARKETING HYPOTHESIS

Criar entidade:

```text
MarketingHypothesis
```

Exemplo:

```yaml
type: audience
statement: "Segmento X responde melhor a autonomia do que romance."
evidence:
  - interview
  - search signal
confidence: 0.67
status: TESTING
```

Fluxo:

```text
HYPOTHESIS
↓
EXPERIMENT
↓
RESULT
↓
VALIDATED | REJECTED | INCONCLUSIVE
```

---

# 117. PAID MEDIA STRATEGIST

Adicionar após Audience Intelligence e Experimentation Core.

Responsabilidades:

- recomendar channel mix;
- estruturar campanhas;
- recomendar objective;
- propor audience;
- propor budget allocation;
- desenhar experimentos;
- solicitar criativos;
- preparar campaign execution plan.

Não deve possuir liberdade irrestrita de spend.

---

# 118. CHANNEL CONNECTORS

Meta, Google e TikTok começam como connectors/tools.

Arquitetura:

```text
Paid Media Strategist
        │
        ├── Meta Ads Connector
        ├── Google Ads Connector
        └── TikTok Ads Connector
```

Connectors devem encapsular:

- authentication;
- account discovery;
- campaign read/write;
- audience/targeting operations quando permitidas;
- creative upload;
- experiment operations quando suportadas;
- metrics read;
- status read;
- budget update;
- pause/resume;
- rate limits;
- retry;
- audit.

Capability deve ser detectada por conta/plataforma e nunca presumida.

---

# 119. CONNECTOR PRINCIPLE

Não codificar lógica estratégica dentro do connector.

Connector responde:

```text
HOW TO EXECUTE ON CHANNEL
```

Paid Media Strategist responde:

```text
WHAT SHOULD BE PREPARED
```

Performance Optimizer responde:

```text
WHAT SHOULD CHANGE
```

Policy Engine responde:

```text
WHAT IS ALLOWED
```

Marketing OS responde:

```text
WHAT IS AUTHORIZED
```

---

# 120. EXPERIMENTATION CORE

Experiment é entidade do Marketing OS, mesmo quando executado por ferramenta nativa de canal.

Adicionar:

```text
Experiment
ExperimentArm
ExperimentMetric
ExperimentObservation
ExperimentDecision
```

Campos:

```text
hypothesis
channel
control
treatment
primary_metric
secondary_metrics
minimum_sample
minimum_duration
start_rule
stop_rule
status
result
confidence
```

---

# 121. EXPERIMENT TYPES

Suportar:

```text
CREATIVE
AUDIENCE
MESSAGE
OFFER
LANDING_PAGE
CHANNEL
BUDGET
BIDDING
```

Não permitir experimento de budget/bidding autoexecutado sem policy explícita.

---

# 122. NATIVE VS CROSS-CHANNEL EXPERIMENTS

Distinguir:

```text
NATIVE_PLATFORM_EXPERIMENT
```

de:

```text
MARKETING_OS_EXPERIMENT
```

Marketing OS mantém hipótese, governança e resultado canônico.

Plataforma pode executar o mecanismo específico.

---

# 123. PERFORMANCE OPTIMIZER

Adicionar somente após metrics normalization.

Responsabilidades:

- analisar performance;
- comparar campanha vs target;
- analisar persona × creative × channel × offer;
- identificar anomalias;
- recomendar ação;
- pedir investigação quando dados insuficientes;
- produzir Performance Recommendation.

Não executar spend diretamente.

---

# 124. PERFORMANCE ACTION SPACE

Espaço inicial de decisão:

```text
INCREASE
KEEP
REDUCE
PAUSE
INVESTIGATE
CREATE_VARIANT
```

Ações devem ser tipadas.

---

# 125. DETERMINISTIC PERFORMANCE GUARDRAILS

Antes de qualquer JEV/LLM recommendation validar:

```text
minimum_conversions
minimum_spend
minimum_duration
maximum_budget_change_percent
maximum_daily_budget
campaign_status
account_status
experiment_lock
human_override
data_freshness
attribution_window
```

Depois validar postconditions.

---

# 126. JEV FOR PERFORMANCE

JEV pode ser usado quando:

- input está estruturado;
- opções são limitadas;
- regras determinísticas já passaram;
- dados mínimos existem.

Exemplo:

```text
STATE
+
TARGET
+
METRICS
+
ALLOWED ACTIONS
↓
JEV
↓
ACTION + CONFIDENCE
```

JEV não define livremente valor de spend.

Valor permitido deve ser calculado/limitado por policy determinística.

---

# 127. BUDGET OPTIMIZATION POLICY

Budget é estado crítico.

Regras iniciais:

```text
LLM cannot change budget directly
JEV cannot bypass budget limits
every budget change is audited
every budget change has reason
every budget change has source metrics
```

Padrão inicial:

```text
RECOMMENDATION
↓
HUMAN APPROVAL
↓
EXECUTION
```

Autoexecution só depois de histórico, evals e policy aprovada.

---

# 128. CONTROLLED AUTO-EXECUTION

Somente permitir quando todos verdadeiros:

```text
high confidence
data fresh
minimum sample reached
inside max delta
inside campaign limit
inside workspace limit
no active experiment conflict
no human hold
connector healthy
policy allows autoexecute
```

Mesmo assim, manter:

- audit;
- rollback/compensation;
- notification;
- trace.

---

# 129. METRICS NORMALIZATION

Criar camada canônica de métricas.

Entidades sugeridas:

```text
CampaignMetricDefinition
ChannelMetricMapping
MetricSnapshot
AttributionSnapshot
PerformanceTarget
```

Separar métrica nativa da plataforma da métrica normalizada.

Exemplo:

```text
meta.spend
google.cost_micros
tiktok.spend
↓
normalized.spend
```

---

# 130. ATTRIBUTION

MVP deve declarar explicitamente modelo de atribuição.

Não misturar resultados de canais com janelas diferentes como se fossem comparáveis.

Registrar:

```text
source
platform_attribution_window
marketing_os_attribution_model
observed_at
```

---

# 131. LEARNING LOOP

Arquitetura alvo:

```text
Product Context
+
Domain Pack
↓
Audience Intelligence
↓
Segments / Personas
↓
Product Marketer
↓
Campaign Strategy
↓
Content / Creative
↓
Paid Media
↓
Meta / Google / TikTok
↓
Metrics
↓
Performance Optimizer
↓
Rules + JEV
↓
Recommendation
↓
Approval / Execution
↓
New Evidence
↓
Audience Intelligence
```

Esse loop é uma capability central do Marketing OS.

---

# 132. PERSONA × CREATIVE × CHANNEL LEARNING

Persistir capacidade de analisar:

```text
Persona
×
Creative
×
Channel
×
Offer
×
Landing Page
```

Evitar conclusões sem volume suficiente.

---

# 133. FIRST-PARTY DATA

Quando CRM/customer data for conectado:

- consentimento;
- purpose limitation;
- minimização;
- hashing/pseudonymization quando apropriado;
- workspace isolation;
- retention;
- deletion;
- access logging.

Agentes nunca recebem dataset bruto se um resumo/aggregate resolve.

---

# 134. UI — AUDIENCE INTELLIGENCE

Adicionar ao Marketing Management OS:

```text
Audiences
├── Research
├── Segments
├── Personas
├── Evidence
├── Hypotheses
└── Experiments
```

Usuário deve conseguir:

- revisar;
- editar;
- aprovar;
- rejeitar;
- versionar;
- ver evidência;
- ver performance associada.

---

# 135. UI — PAID MEDIA

Adicionar:

```text
Paid Media
├── Accounts
├── Campaigns
├── Ad Groups / Ad Sets
├── Ads
├── Creatives
├── Experiments
├── Budgets
├── Recommendations
└── Approvals
```

A UI nunca deve esconder que uma ação alterará spend real.

---

# 136. UI — PERFORMANCE

Adicionar:

```text
Performance
├── Executive Dashboard
├── Channel Performance
├── Campaign Performance
├── Audience Performance
├── Creative Performance
├── Experiment Results
├── Recommendations
└── Change History
```

---

# 137. PAID MEDIA APPROVALS

Novas actions:

```text
CREATE_CAMPAIGN
CREATE_AD
START_EXPERIMENT
PUBLISH_AD
INCREASE_BUDGET
REDUCE_BUDGET
PAUSE_CAMPAIGN
RESUME_CAMPAIGN
```

Policy inicial:

```text
CREATE DRAFT
→ automatic

PUBLISH / SPEND / BUDGET CHANGE
→ human approval
```

---

# 138. PAID MEDIA PERMISSIONS

Paid Media Strategist:

```text
read metrics: yes
draft campaign: yes
draft targeting: yes
draft budget: yes
publish: no
spend: no
```

Performance Optimizer:

```text
read metrics: yes
recommend: yes
create experiment proposal: yes
change budget: no
pause: no
```

Channel Connector:

```text
execute only with valid authorization token
+
approved action
+
idempotency key
```

---

# 139. ADS CREDENTIAL SECURITY

OAuth/token material:

- encrypted;
- server-side only;
- scoped;
- rotated;
- never sent to model;
- never traced;
- never stored in Artifact.

Prefer token exchange/managed connector patterns quando disponíveis.

---

# 140. ADS AUDIT LOG

Toda ação externa deve registrar:

```text
workspace
platform
account
campaign
action
before
after
requested_by
recommended_by
approved_by
executed_by
reason
source_metrics
trace_id
timestamp
```

---

# 141. OBSERVABILITY — PAID MEDIA

Adicionar spans:

```text
audience_research
persona_generation
persona_review
experiment_create
experiment_observation
paid_media_plan
connector_call
metrics_import
performance_analysis
performance_recommendation
budget_policy_check
budget_change
```

Adicionar métricas:

```text
connector_error_rate
metrics_freshness
recommendation_acceptance_rate
budget_change_reversal_rate
experiment_completion_rate
persona_validation_rate
```

---

# 142. EVALS — AUDIENCE INTELLIGENCE

Avaliar:

- evidence grounding;
- source quality;
- no fabricated persona facts;
- confidence calibration;
- segmentation usefulness;
- bias/sensitive targeting;
- actionable output;
- revision with new evidence.

---

# 143. EVALS — PAID MEDIA

Avaliar:

- campaign structure validity;
- objective alignment;
- targeting coherence;
- budget policy compliance;
- channel capability awareness;
- no unsupported execution claims.

---

# 144. EVALS — PERFORMANCE

Avaliar:

- metric interpretation;
- insufficient-data handling;
- action selection;
- guardrail adherence;
- confidence calibration;
- rollback recommendation;
- no direct spend bypass.

---

# 145. UPDATED EXECUTION ORDER

Nova sequência recomendada:

```text
FOUNDATION
↓
AUTH + WORKSPACE RLS
↓
PRODUCT CONTEXT
↓
DOMAIN PACK
↓
CAMPAIGN CORE
↓
ARTIFACT + APPROVAL
↓
CREATIVE CORE
↓
AUDIENCE INTELLIGENCE
↓
EXPERIMENTATION CORE
↓
MARKETING MANAGEMENT UI
↓
AGENT RUN API
↓
EVE CONTEXT INTEGRATION
↓
DOMAIN SPECIALIST
↓
CREATIVE PRODUCER
↓
OTEL END-TO-END
↓
PAID MEDIA ABSTRACTION
↓
CHANNEL CONNECTORS
↓
METRICS NORMALIZATION
↓
PERFORMANCE OPTIMIZER
↓
RECOMMENDATION + APPROVAL
↓
BOUNDED JEV OPTIMIZATION
↓
CONTROLLED AUTO-EXECUTION
```

Não pular diretamente para budget automation.

---

# 146. UPDATED HARNESS READINESS

Além dos critérios existentes, `HARNESS_READY` para Paid Media requer:

- Audience evidence model definido;
- Experiment model definido;
- connector security policy definida;
- metrics normalization definida;
- attribution policy definida;
- spend approval policy definida;
- budget guardrails definidos;
- paid media audit definido;
- performance eval policy definida;
- OAuth/token handling definido.

Sem isso:

```text
PAID_MEDIA_AUTOMATION_READY = false
```

---

# 147. REGRA FINAL V1.1

O Marketing OS deve evoluir de:

```text
AI TEAM THAT PRODUCES MARKETING
```

para:

```text
MARKETING OPERATING SYSTEM
THAT
RESEARCHES
HYPOTHESIZES
CREATES
EXPERIMENTS
EXECUTES
MEASURES
LEARNS
AND OPTIMIZES
```

sem permitir que modelos tenham autoridade financeira ou operacional ilimitada.

---

# 148. AGENCY MULTI-TENANCY

O Harness passa a adotar uma hierarquia explícita:

```text
Agency Tenant
↓
Client Workspace
↓
Product / Brand
↓
Campaign
```

`Agency Tenant` é a fronteira superior de tenancy.

`Client Workspace` é a fronteira operacional entre clientes da mesma agência.

Nenhuma autorização pode depender apenas de `workspace_id` fornecido pelo modelo.

---

# 149. TENANT IDENTIFIERS

Contratos cross-plane devem carregar, conforme aplicável:

```text
agency_id
client_workspace_id
product_id
campaign_id
agent_run_id
```

Esses identificadores servem para contexto e auditoria.

Eles NÃO substituem authorization server-side.

---

# 150. SUPABASE RLS — TWO-LEVEL ISOLATION

RLS deve impedir:

```text
Agency A → Agency B
```

e também:

```text
Client A → Client B
```

dentro da mesma agência quando o usuário não possuir membership adequado.

Testes mínimos:

```text
cross-agency deny
cross-client deny
agency-admin allow
account-manager scoped allow
client-admin own-workspace allow
client-viewer read-only
```

---

# 151. MEMBERSHIP MODEL

Modelar separadamente:

```text
AgencyMembership
ClientWorkspaceMembership
```

Um usuário pode:

- ser Agency Admin;
- ter acesso somente a clientes específicos;
- possuir papel diferente em cada cliente.

Authorization resolve o escopo efetivo antes de tool/API execution.

---

# 152. CLIENT-SCOPED INTEGRATIONS

Toda integração pertencente a um cliente deve ser vinculada a:

```text
agency_id
+
client_workspace_id
```

Exemplos:

- Meta Business / Ad Account;
- Google Ads Customer;
- TikTok Ad Account;
- Resend;
- Brevo;
- CRM;
- Analytics.

Nunca reutilizar token de um cliente para outro sem associação e policy explícitas.

---

# 153. CLIENT INTEGRATION TOKENS

Tokens OAuth dinâmicos de clientes não devem existir como env var compartilhada por tenant.

A arquitetura deve usar armazenamento seguro de credenciais dinâmicas ou token references.

Supabase armazena apenas metadata/reference quando isso reduzir risco.

Nunca:

- enviar token ao modelo;
- registrar token em trace;
- armazenar token em Artifact;
- retornar token por tool.

---

# 154. CLIENT ADVISOR PROFILE

Adicionar entidade:

```text
AdvisorProfile
```

Escopo:

```text
Client Workspace
ou
Product
```

O Advisor Profile configura o agente genérico `product-domain-specialist`.

Campos esperados:

```text
domain packs
knowledge sources
claims policy
risk policy
review requirements
model policy
agent binding
```

O cliente pode "ter seu próprio Advisor" sem exigir código de agente exclusivo.

---

# 155. OPTIONAL REMOTE ADVISOR

Quando um cliente exigir isolamento especial, Advisor Profile poderá apontar para Remote Eve Agent.

Motivos válidos:

- regulated domain;
- proprietary knowledge;
- customer-owned deployment;
- credentials;
- independent release cycle.

Não usar Remote Agent como padrão para todos os clientes.

---

# 156. AGENCY DASHBOARD

Control Plane deve oferecer visão consolidada:

- clients;
- campaigns;
- spend;
- leads;
- CPA/CPL/ROAS;
- approvals;
- Agent Runs;
- integration health;
- cost;
- recommendations.

Queries agregadas devem respeitar memberships.

---

# 157. CLIENT DASHBOARD

Cada Client Workspace deve possuir visão própria:

- products;
- campaigns;
- content;
- creatives;
- paid media;
- experiments;
- performance;
- approvals;
- agents;
- integrations.

Client users nunca recebem cross-client aggregation.

---

# 158. CLIENT PORTAL

Harness deve considerar Client Portal como surface autorizada do mesmo Control Plane.

Policies devem distinguir:

```text
agency_user
client_user
```

A UI não pode ser a única barreira.

API/RLS deve aplicar o mesmo isolamento.

---

# 159. AGENT CONTEXT CONTRACT V2

Atualizar `AGENT_CONTEXT_CONTRACT.md`.

Inputs mínimos:

```yaml
context:
  agency_id:
  client_workspace_id:
  product_id:
  campaign_id:
  agent_run_id:
  task_type:
  permission_envelope:
```

O agent carrega dados via tools.

Não recebe contexto de outros clientes.

---

# 160. PERMISSION ENVELOPE — CLIENT SCOPE

Permission Envelope deve declarar:

```text
agency scope
client scope
product scope
campaign scope
allowed resources
allowed actions
external side effects
```

Exemplo:

```yaml
scope:
  agency_id: ag_01
  client_workspace_id: cl_22

actions:
  read_campaign: true
  create_artifact: true
  publish: false
  spend: false
```

---

# 161. CROSS-CLIENT AGENT OPERATIONS

Marketing Lead não deve receber simultaneamente contexto de vários clientes em uma execução comum.

Cross-client analysis é uma capability separada e deve receber apenas dados agregados/permitidos.

Evitar:

```text
Client A raw context
+
Client B raw context
→ same agent prompt
```

sem caso de uso explícito.

---

# 162. AGENCY ANALYTICS

Visão multi-cliente deve usar camada de analytics/control plane.

Não pedir a um LLM para agregar dados crus de todos os clientes quando SQL/analytics resolve.

LLM pode explicar agregados autorizados.

---

# 163. CLIENT-SCOPED AUDIT

Todo Audit Event relevante inclui:

```text
agency_id
client_workspace_id
actor
action
resource
result
trace_id
```

Para ações externas:

```text
external_account_id
```

quando seguro e necessário.

---

# 164. CLIENT OFFBOARDING

Criar runbook para:

- revoke integrations;
- disable agent runs;
- export data;
- archive campaigns;
- terminate client user access;
- handle retention;
- delete/anonymize according to policy;
- preserve required audit.

---

# 165. CLIENT INTEGRATION HEALTH

Cada conexão deve possuir:

```text
CONNECTED
DEGRADED
EXPIRED
REAUTH_REQUIRED
DISCONNECTED
```

Agency Dashboard deve exibir falhas sem revelar secrets.

---

# 166. MEDIA ACCOUNT OWNERSHIP

AdAccount mapping deve possuir:

```text
client_workspace_id
platform
external_account_id
display_name
status
permissions
connected_by
credential_ref
```

Campaign externa só pode ser associada ao Client Workspace dono da conexão.

---

# 167. APPROVAL SCOPES

Approval policy pode variar por cliente.

Exemplos:

```text
Agency internal approval only
Client approval required
Dual approval required
Auto-approve drafts
```

Publicação/spend continua exigindo policy válida.

---

# 168. CLIENT POLICY

Adicionar conceito:

```text
ClientPolicy
```

Pode governar:

- required approvals;
- allowed channels;
- maximum spend change;
- claims review;
- domain review;
- agent permissions;
- creative providers;
- publication hours;
- autoexecution policy.

---

# 169. MULTI-TENANT OBSERVABILITY

Traces podem carregar:

```text
agency_id
client_workspace_id
product_id
campaign_id
agent_run_id
```

Mas IDs de alta cardinalidade não devem virar labels de métricas agregadas indiscriminadamente.

Métricas operacionais agregadas devem preferir dimensões controladas:

```text
service
agent
channel
status
environment
```

Investigações por tenant usam traces/logs protegidos.

---

# 170. COST ALLOCATION BY CLIENT

Registrar custo por:

```text
agency
client
product
campaign
agent run
creative generation
```

Agency Dashboard deve permitir chargeback/showback futuro.

---

# 171. CLIENT DATA RETENTION

Retention pode variar por Client Policy dentro dos limites da plataforma.

Nunca permitir policy de cliente reduzir requisitos obrigatórios de segurança/audit definidos pela plataforma.

---

# 172. UPDATED DOMAIN ENTITIES

Adicionar ou garantir:

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

Relacionamentos:

```text
AgencyTenant
└── ClientWorkspace
    ├── Products
    ├── AdvisorProfile
    ├── Integrations
    ├── Campaigns
    └── Members
```

---

# 173. UPDATED UI SURFACES

Harness deve considerar:

```text
Agency Dashboard
Clients
Client Dashboard
Requests
Products
Audiences
Campaigns
Creative Studio
Experiments
Paid Media
Performance
Approvals
Agents
Integrations
Reports
Settings
Client Portal
```

---

# 174. UPDATED SPEC MAP — MULTI-TENANT AGENCY

Reavaliar sequência e incluir:

```text
SPEC-A01 Agency Tenant Foundation
SPEC-A02 Agency + Client Membership RBAC
SPEC-A03 Client Workspace
SPEC-A04 Client Policy
SPEC-A05 Client Advisor Profile
SPEC-A06 Client Integration Vault / References
SPEC-A07 Agency Dashboard
SPEC-A08 Client Dashboard
SPEC-A09 Client Portal
SPEC-A10 Client Offboarding
```

Essas specs devem ser encaixadas antes das integrações Paid Media reais.

---

# 175. PAID MEDIA MULTI-CLIENT GATE

Meta/Google/TikTok só podem entrar em produção quando:

- Client Workspace isolation passa;
- credential storage passa;
- account mapping passa;
- connector authorization passa;
- audit passa;
- approval passa;
- metrics import passa;
- no cross-client leakage exists.

---

# 176. AGENCY HARNESS READINESS

Adicionar dimensões ao Readiness Report:

```text
AGENCY_TENANCY
CLIENT_ISOLATION
CLIENT_RBAC
CLIENT_ADVISOR
CLIENT_INTEGRATIONS
CLIENT_PORTAL
CLIENT_OFFBOARDING
CROSS_CLIENT_ANALYTICS
```

Qualquer falha crítica de isolamento:

```text
HARNESS_READY = false
```

---

# 177. REGRA FINAL V1.2

O sistema deve conseguir operar:

```text
MANY AGENCIES
×
MANY CLIENTS
×
MANY PRODUCTS
×
MANY CAMPAIGNS
×
MANY CHANNEL ACCOUNTS
```

sem que:

- dados;
- contexto;
- credenciais;
- approvals;
- Agent Runs;
- artifacts;
- metrics;

se misturem entre tenants.

