# PRD — Marketing Management OS
## Agência Multi-Tenant com Times Agentic de Marketing

**Versão:** 2.1
**Status:** proposta consolidada para revisão de produto e arquitetura  
**Produto:** Marketing Management OS  
**Modelo operacional primário:** agência gerenciando múltiplos clientes  
**Arquitetura:** Control Plane + Execution Plane  
**Control Plane:** Marketing Management OS  
**Execution Plane:** Marketing Agents / Eve  
**Infraestrutura alvo:** Vercel + Supabase + Eve + OpenTelemetry
**Posicionamento canônico:** Agentic Marketing Operations Platform for Agencies

As decisões recentes de escopo e prioridade vêm do [Product Update Plan](../harness/MARKETING_OS_PRODUCT_UPDATE_PLAN.md). O [Design System](../harness/MARKETING_OS_DESIGN_SYSTEM.md) é a referência canônica de UX/UI e a [Prototype Inspiration](../harness/MARKETING_OS_PROTOTYPE_INSPIRATION.md) é a referência oficial de prototipação, sem copiar concorrentes. Esta versão do PRD reconcilia essas fontes com a arquitetura funcional; políticas e contratos de execução permanecem em `docs/harness/`.

---

# 1. Resumo executivo

O Marketing Management OS é uma **Agentic Marketing Operations Platform for Agencies** com aplicação Web para operar uma agência de marketing assistida por agentes de IA.

A plataforma deve permitir que uma agência:

- gerencie múltiplos clientes de forma isolada;
- mantenha produtos, marcas, contextos e regras específicas por cliente;
- conecte progressivamente contas de email, Meta, Google, TikTok, analytics e outras integrações por cliente;
- receba solicitações de trabalho;
- orquestre agentes especializados por meio do Eve;
- produza estratégia, conteúdo, criativos, landing pages, books, vídeos e outros ativos;
- gerencie revisão e aprovação;
- publique ou execute ações externas de forma controlada;
- acompanhe campanhas, publicações, experimentos e performance;
- gere recomendações de otimização;
- gerencie verba com guardrails determinísticos e aprovação;
- mantenha um ciclo contínuo de pesquisa, criação, execução, medição e aprendizado.

A interface Web é o produto principal. O chat com o Marketing Lead é uma utility surface contextual, como drawer, command palette ou assistência dentro de Client/Campaign, e não a homepage.

---

# 2. Problema

Times e agências de marketing trabalham hoje com informações fragmentadas entre:

- gerenciadores de anúncios;
- planilhas;
- chats;
- ferramentas de conteúdo;
- Notion;
- ferramentas de email;
- dashboards;
- documentos;
- ferramentas de design;
- fornecedores de IA.

Um time agentic isolado resolve parte da produção, mas não resolve a gestão operacional.

Sem um sistema central surgem problemas como:

- contexto de clientes misturado;
- claims incorretos;
- dificuldade de rastrear quem aprovou o quê;
- produção desconectada dos resultados;
- criativos sem versionamento;
- personas sem evidência;
- testes A/B presos dentro de cada canal;
- orçamento administrado manualmente;
- dificuldade para entender quais agentes estão trabalhando;
- falta de visão executiva por cliente;
- falta de visão consolidada da agência;
- dependência excessiva de ferramentas externas como Notion.

---

# 3. Visão do produto

A plataforma deve funcionar como um **Marketing Operating System para agências**.

Hierarquia conceitual:

```text
PLATFORM
↓
AGENCY TENANT
↓
CLIENT WORKSPACE
↓
PRODUCT / BRAND
↓
CAMPAIGN
↓
WORK / ARTIFACTS / EXPERIMENTS / PUBLICATIONS
↓
METRICS / LEARNING / OPTIMIZATION
```

O Marketing OS é o Control Plane e System of Record para operações de marketing. O ciclo de produto é `research → plan → create → review → publish/execute → measure → optimize → learn`. O OS cobre aquisição, engajamento, qualificação futura, medição e otimização; opportunity, pipeline, sales e customer lifecycle pertencem a CRMs externos. A [arquitetura canônica](./ARCHITECTURE.md) e o [modelo de Lead Qualification](./LEAD_QUALIFICATION_MODEL.md) fixam essa fronteira.

O Eve é o Execution Plane.

```text
Marketing OS
decide O QUE precisa acontecer
e registra a verdade do negócio

Eve / Marketing Lead
decide COMO executar cognitivamente
e QUAL especialista deve atuar
```

---

# 4. Princípios fundamentais

1. **Agents never own business state. Marketing OS always owns business state.**
2. Todo recurso pertence explicitamente a um Agency Tenant e, quando aplicável, a um Client Workspace.
3. Nenhum agente pode determinar autorização a partir de texto recebido no prompt.
4. Cada cliente deve possuir contexto e integrações próprias.
5. O sistema deve funcionar sem Notion.
6. Notion pode existir como integração opcional.
7. Os agentes de craft permanecem genéricos.
8. Especialização de segmento ocorre por contexto, Domain Pack e Advisor Profile.
9. Personas devem ser baseadas em evidência.
10. Produção e publicação são etapas diferentes.
11. Revisão editorial e autorização de execução são decisões diferentes.
12. Publicar, enviar, gastar e excluir exigem policy explícita; consentimento, opt-out e supressão são pré-condições de envio.
13. Toda alteração financeira deve ser auditável.
14. Toda saída relevante deve ser versionada e rastreável.
15. Performance deve retroalimentar audiência, criativo, estratégia e experimentação.
16. LLMs não possuem autoridade financeira ou de autorização.
17. JEV só deve atuar em decisões estreitas, tipadas e guardadas por regras determinísticas.

---

# 5. Modelo de tenancy

## 5.1 Agency Tenant

A unidade superior de tenancy é a agência.

Exemplos:

```text
Nora Inteligência Digital
Agência XPTO
Consultoria ABC
```

Cada Agency Tenant possui:

- membros;
- papéis;
- políticas;
- clientes;
- custos;
- integrações de nível agência quando aplicável;
- limites de uso;
- preferências;
- dashboards consolidados.

Nenhum Agency Tenant pode acessar recursos de outro.

---

## 5.2 Client Workspace

Cada cliente da agência recebe um Client Workspace próprio.

Exemplos:

```text
Cliente: Doce Capítulo
Cliente: Incorporadora Alfa
Cliente: Clínica Beta
```

O Client Workspace é a principal fronteira operacional de isolamento dentro da agência.

Ele possui:

- membros da agência autorizados;
- membros do cliente, quando convidados;
- Products / Brands;
- Product Context;
- Domain Packs;
- Advisor Profile;
- Campaigns;
- Audiences;
- Personas;
- Artifacts;
- Creatives;
- Experiments;
- Paid Media Accounts;
- Metrics;
- Approvals;
- Integrations;
- Costs;
- Agent Runs.

---

## 5.3 Product / Brand

Um cliente pode possuir um ou vários Products ou Brands.

Exemplo:

```text
Client Workspace
├── Brand A
│   ├── Product A1
│   └── Product A2
└── Brand B
```

Cada Product pode possuir:

- Product Context Pack;
- Domain Pack association;
- campanhas próprias;
- personas;
- assets;
- regras;
- goals;
- oferta;
- claims;
- métricas.

---

# 6. Client-Specific Advisor

Cada Client Workspace deve poder possuir um Advisor especializado.

A experiência para o usuário pode ser:

```text
Advisor do Cliente
```

mas a implementação padrão deve utilizar o agente genérico:

```text
product-domain-specialist
```

configurado por:

```text
Advisor Profile
+
Client Context
+
Product Context
+
Domain Pack
+
Client Knowledge Sources
+
Client Policies
```

Isso significa:

```text
1 cliente
→ 1 Advisor Profile lógico

não necessariamente

1 cliente
→ 1 código/agente diferente
```

O sistema deve permitir no futuro apontar um cliente para um Remote Agent específico quando houver necessidade de:

- runtime isolado;
- conhecimento proprietário;
- requisitos regulatórios;
- release independente;
- credenciais próprias.

---

# 7. Advisor Profile

Entidade sugerida:

```text
AdvisorProfile
```

Campos conceituais:

```yaml
advisor_profile:
  agency_id:
  client_workspace_id:
  product_id:
  name:
  domain_pack_ids:
  knowledge_source_ids:
  required_review_types:
  claims_policy:
  risk_policy:
  model_policy:
  agent_binding:
  status:
```

O Advisor Profile nunca é fonte autônoma da verdade.

Ele referencia fontes versionadas.

---

# 8. Usuários e papéis

## 8.1 Papéis de agência

### Agency Owner
- administração completa;
- billing da plataforma;
- criação de clientes;
- políticas globais.

### Agency Admin
- usuários;
- clientes;
- integrações;
- políticas.

### Account Director
- acesso a múltiplos clientes;
- visão executiva;
- aprovação estratégica.

### Account Manager
- operação de clientes atribuídos;
- criação de solicitações;
- campanhas;
- follow-up.

### Strategist
- estratégia;
- produto;
- audiência;
- campanhas.

### Media Buyer
- mídia paga;
- campanhas;
- experimentos;
- recomendações;
- execução autorizada.

### Creative / Content
- conteúdo;
- criativos;
- revisão.

### Analyst
- métricas;
- performance;
- relatórios.

---

## 8.2 Papéis do cliente

### Client Admin
- usuários do cliente;
- visualização ampla;
- aprovações.

### Client Approver
- aprova peças e/ou execução conforme escopo.

### Client Reviewer
- comenta;
- solicita alterações.

### Client Viewer
- somente leitura.

---

# 9. Escopo de autorização

Toda autorização deve considerar:

```text
authenticated_user
+
agency_membership
+
client_workspace_membership
+
role
+
resource_scope
+
action
```

Nunca apenas:

```text
user_id
```

ou:

```text
workspace_id vindo do prompt
```

---

# 10. Interface Web — visão geral

A aplicação deve possuir navegação primária semelhante a:

```text
Agency Dashboard
Clients
Requests
Products
Audiences
Campaigns
Content
Creative Studio
Experiments
Paid Media
Performance
Approvals
Agents
Integrations
Reports
Settings
```

Dentro de cada Client Workspace a interface muda para o contexto daquele cliente e inclui **Engagement**. As perspectivas Agency, Client e Portal seguem a [arquitetura da informação](./AGENCY_UI_INFORMATION_ARCHITECTURE.md); o [Design System](../harness/MARKETING_OS_DESIGN_SYSTEM.md) governa navegação, estados e acessibilidade.

---

# 11. Agency Dashboard

Visão consolidada para a agência.

Deve exibir:

- clientes ativos;
- campanhas ativas;
- investimento gerenciado;
- leads;
- conversões;
- CPL;
- CPA;
- ROAS quando aplicável;
- aprovações pendentes;
- tarefas atrasadas;
- Agent Runs em execução;
- falhas de integrações;
- recomendações de performance;
- alertas de orçamento;
- custo de IA;
- custo de geração criativa.

Filtros:

- Client;
- Product;
- Channel;
- Period;
- Account Manager.

---

# 12. Client Dashboard

Cada cliente possui dashboard próprio.

Exibir:

- campanhas;
- canais;
- investimento;
- resultados;
- conteúdos publicados;
- criativos;
- experimentos;
- recomendações;
- tarefas;
- aprovações;
- status das integrações.

---

# 13. Requests / Solicitações

A interface deve permitir criar solicitações estruturadas.

Exemplo:

```text
Cliente: Doce Capítulo
Produto: Doce Capítulo
Campanha: Lançamento Outubro

Solicitação:
Criar campanha de aquisição

Objetivo:
500 leads

Budget:
R$ 20.000

Canais desejados:
Meta
Google
Email
```

A solicitação cria:

```text
WorkRequest
+
AgentRun
```

e passa ao Marketing Lead.

---

# 14. Agent Run Management

A UI deve permitir acompanhar:

```text
Product Marketer       DONE
Audience Intelligence  DONE
Domain Advisor          DONE
Content                 RUNNING
Creative Producer       RUNNING
Paid Media              WAITING
```

O usuário deve ver:

- status;
- início;
- duração;
- custo;
- artefatos gerados;
- bloqueios;
- solicitações de aprovação;
- erros;
- retry quando permitido.

---

# 15. Product Context

Cada Product deve possuir Product Context versionado.

A UI deve permitir:

- visualizar versão atual;
- editar draft;
- comparar diff;
- anexar fontes;
- aprovar;
- publicar versão;
- consultar histórico.

---

# 16. Domain Packs

Domain Packs são reutilizáveis entre clientes e produtos quando apropriado.

Exemplos:

- Real Estate;
- Financial Services;
- Healthcare;
- SaaS;
- E-commerce;
- Relationship / Well-being.

Podem ser:

- privados da agência;
- privados do cliente;
- reutilizáveis;
- futuramente instaláveis.

---

# 17. Audience Intelligence

Área:

```text
Audiences
├── Research
├── Segments
├── Personas
├── Evidence
├── Hypotheses
└── Experiments
```

O sistema deve suportar:

- pesquisa de mercado;
- pesquisa de concorrentes;
- sinais de busca;
- pesquisa pública;
- entrevistas;
- surveys;
- dados de CRM autorizados;
- performance histórica;
- dados de campanha.

---

# 18. Audience Segment

Segment é uma estrutura mais objetiva.

Exemplo:

```text
Mulheres
35–50
Brasil
interesse em desenvolvimento pessoal
```

Deve possuir:

- origem;
- critérios;
- evidence;
- version;
- status.

---

# 19. Persona

Persona é interpretativa.

Deve possuir:

- version;
- evidence;
- confidence;
- status;
- goals;
- barriers;
- objections;
- media behavior;
- language;
- triggers.

Estados:

```text
DRAFT
HYPOTHESIS
TESTING
VALIDATED
NEEDS_REVIEW
DEPRECATED
```

Persona não pode ser considerada validada apenas porque um LLM a produziu.

---

# 20. Campaign Management

Campaign é entidade central.

Deve possuir:

- Client;
- Product;
- objective;
- audience;
- persona;
- offer;
- channels;
- campaign brief;
- budget;
- targets;
- status;
- tasks;
- artifacts;
- experiments;
- metrics;
- approvals;
- publications;
- engagement campaigns, broadcasts e sequences quando Email estiver habilitado.

---

# 21. Campaign UI

Exemplo:

```text
Campaign: Lançamento Doce Capítulo

Status: ACTIVE
Budget: R$ 30.000
Spend: R$ 12.340

Objective:
500 leads

Audience:
Persona A
Persona B

Channels:
Meta       ACTIVE
Google     ACTIVE
TikTok     TESTING
Email      ACTIVE

Strategy          APPROVED
Content           APPROVED
Creatives         3 IN REVIEW
Landing Page      PUBLISHED
Paid Media        RUNNING
Experiments       2 RUNNING
Performance       RECOMMENDATION AVAILABLE
```

---

# 22. Content Management

O OS deve armazenar a peça canônica.

Tipos:

- blog;
- social post;
- email;
- newsletter;
- SEO brief;
- landing copy;
- ad copy;
- sales copy;
- script.

Notion pode exportar/importar, mas não é obrigatório.

---

# 23. Creative Studio

Área:

```text
Creative Studio
├── Briefs
├── Creative Sets
├── Drafts
├── In Review
├── Approved
├── Published
├── Experiments
└── Performance
```

---

# 24. Creative Types

Suportar progressivamente:

- image;
- carousel;
- banner;
- ad;
- thumbnail;
- mockup;
- infographic;
- product book;
- catalog;
- e-book;
- presentation;
- landing page;
- video;
- Reel;
- Short;
- voice;
- campaign kit.

---

# 25. Creative Set

Exemplo:

```text
Launch Kit — Campaign 123
├── Landing Page
├── Product Book
├── Instagram Carousel
├── Reel
├── Meta Ad A
├── Meta Ad B
├── TikTok Video
└── Email Banner
```

---

# 26. Repurposing

A interface deve permitir:

```text
Source Artifact
↓
Create Derivatives
```

Exemplo:

```text
Blog Post
→ LinkedIn carousel
→ Instagram carousel
→ Reel script
→ Hero image
→ eBook chapter
```

---

# 27. Approval Inbox

Tela central de aprovações.

Tipos:

- Product Context approval;
- Domain Pack approval;
- content review;
- creative review;
- campaign approval;
- publication approval;
- email send approval;
- experiment launch approval;
- budget change approval;
- pause/resume approval.

---

# 28. Approval Snapshot

A aprovação deve registrar exatamente o que foi aprovado:

- artifact version;
- destination;
- audience;
- schedule;
- budget;
- payload/hash;
- actor;
- timestamp.

Mudança no snapshot invalida approval quando policy exigir.

---

# 29. Publications

A plataforma deve acompanhar publicações.

Exemplo:

```text
Instagram Carousel
Published
03/10 14:30
External ID: ...
Reach: ...
CTR: ...

Meta Ad A
Running
Spend: ...
Leads: ...
CPL: ...

Google Campaign
Running
Spend: ...
Conversions: ...
CPA: ...
```

---

# 30. Client Integration Center

Cada Client Workspace deve conectar suas próprias contas.

Área:

```text
Integrations
├── Meta
├── Google Ads
├── TikTok Ads
├── Resend
├── Brevo
├── Analytics
├── CRM
├── Notion
└── outras
```

A conexão deve pertencer ao Client Workspace. A lista é arquitetura alvo: CRM connectors são futuros; Resend/Brevo exigem adaptação para o OS e não estão operacionais no Control Plane atual.

## Atualização 2.1 — Engagement e Agentic Email

A área Engagement abstrai `EMAIL`, `WHATSAPP`, `SMS`, `INSTAGRAM_DM`, `FACEBOOK_MESSENGER` e `WEB_CHAT`. Apenas Email é o primeiro canal planejado; os demais permanecem em roadmap e só aparecem como operáveis após integração, identidade, consentimento e policy próprios. A [Engagement Architecture](./ENGAGEMENT_ARCHITECTURE.md) define o modelo funcional, e a [Agentic Email Marketing Spec](./AGENTIC_EMAIL_MARKETING_SPEC.md) define a primeira entrega.

Agentic Email deve oferecer campaigns, broadcasts, sequences, segments, templates, experiments, automations delimitadas, performance e AI recommendations. O fluxo canônico é `Audience → Campaign Goal → Email Strategy → Content / Creative → Sequence → Approval → Resend / Brevo → Metrics → Performance → Learning`. O agente `email` atual é uma base de adaptação de copy e operação Resend; a área completa do OS ainda é alvo. Preparar, agendar e enviar são decisões distintas, com consentimento por canal, supressão e aprovação do payload exato antes de `SEND` real.

Lead Qualification é roadmap e prepara `Lead`, `LeadIdentity`, `LeadSource`, `LeadQualification`, `ConversationThread`, `EngagementEvent`, `Consent` e `Handoff`. Um Lead Qualification Agent futuro propõe avaliações com contexto mínimo; o OS governa a decisão e entrega dados autorizados a CRM externo. Conectores futuros: HighLevel, HubSpot, RD Station, Pipedrive e Salesforce. O OS não inclui pipeline de vendas nem ciclo de vida comercial como fonte de verdade. A [Lead Qualification Model](./LEAD_QUALIFICATION_MODEL.md) detalha essa fronteira.

---

# 31. Paid Media Account Model

Entidades conceituais:

```text
ChannelConnection
AdAccount
Page/Profile
Pixel/ConversionSource
CampaignExternalMapping
CreativeExternalMapping
```

Uma Agency pode administrar múltiplas contas de múltiplos clientes sem mistura.

---

# 32. Meta / Google / TikTok

Inicialmente são connectors/tools, não agentes separados.

```text
Paid Media Strategist
├── Meta Ads Connector
├── Google Ads Connector
└── TikTok Ads Connector
```

Cada connector deve declarar capabilities realmente disponíveis.

---

# 33. Paid Media

Área:

```text
Paid Media
├── Accounts
├── Campaigns
├── Ad Groups / Ad Sets
├── Ads
├── Targeting
├── Creatives
├── Budgets
├── Experiments
├── Recommendations
└── Change History
```

---

# 34. Paid Media Strategist

Responsabilidades:

- channel mix;
- campaign structure;
- objective;
- targeting recommendation;
- budget recommendation;
- experiment design;
- creative requirements;
- execution plan.

Não movimenta spend diretamente.

---

# 35. Experimentation

Experiment é entidade própria do OS.

Tipos:

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

Mesmo quando executado por Meta/Google/TikTok, o experimento continua registrado no Marketing OS.

---

# 36. Experiment UI

Exemplo:

```text
Experiment EXP-041

Hypothesis:
"Autonomia converte melhor do que romance para Persona A"

Control:
Creative A

Treatment:
Creative B

Channel:
Meta

Primary metric:
CPL

Status:
RUNNING
```

---

# 37. Metrics Normalization

O sistema deve criar camada normalizada entre canais.

Exemplo:

```text
Meta spend
Google cost_micros
TikTok spend
↓
normalized.spend
```

Manter também o valor nativo.

---

# 38. Attribution

O MVP deve declarar modelo de atribuição.

Métricas devem registrar:

- source;
- attribution window;
- timestamp;
- freshness;
- normalized definition.

Não comparar métricas incompatíveis sem aviso.

---

# 39. Performance

Área:

```text
Performance
├── Executive
├── Channel
├── Campaign
├── Audience
├── Persona
├── Creative
├── Offer
├── Landing Page
├── Experiments
└── Recommendations
```

---

# 40. Performance Optimizer

Responsabilidades:

- analisar métricas;
- detectar anomalias;
- comparar com targets;
- cruzar Persona × Creative × Channel × Offer;
- recomendar otimizações;
- indicar dados insuficientes;
- gerar recommendation artifact.

---

# 41. Recommendation Model

Ações iniciais:

```text
INCREASE
KEEP
REDUCE
PAUSE
INVESTIGATE
CREATE_VARIANT
```

Recommendation não é Execution.

---

# 42. Budget Management

Budget é estado crítico.

Regras:

- LLM não altera budget;
- JEV não bypassa limits;
- toda alteração possui source metrics;
- toda alteração possui reason;
- toda alteração é auditada;
- aprovação humana é padrão inicial.

---

# 43. JEV

Fase futura.

Quando houver dados e guardrails suficientes:

```text
STATE
+
METRICS
+
TARGET
+
ALLOWED ACTIONS
↓
JEV
↓
ACTION + CONFIDENCE
```

Regras determinísticas devem existir antes e depois.

---

# 44. Controlled Auto-Execution

Fora do MVP.

Só pode existir quando:

- dados suficientes;
- confidence alta;
- max delta respeitado;
- campaign cap respeitado;
- agency policy permite;
- client policy permite;
- connector saudável;
- nenhuma trava humana;
- rollback existe.

---

# 45. Client Portal

Client Portal is part of the MVP. A aplicação oferece ao cliente uma superfície do mesmo Control Plane, limitada ao seu Client Workspace.

O escopo inicial inclui:

- Overview;
- Campaigns;
- Creatives;
- Approvals;
- Performance;
- Reports;
- Requests.

Nessas áreas, o cliente pode consultar entregas e resultados compartilhados, comentar, solicitar mudanças e decidir aprovações conforme seu papel. O portal não expõe configuração interna de agentes, custos internos da agência, cross-client analytics, configurações técnicas internas, administração avançada de integrações nem informações de outros clientes.

---

# 46. Reports

Gerar relatórios:

- client performance;
- campaign performance;
- creative performance;
- paid media;
- experiment results;
- executive summary;
- monthly report.

Podem ser exportados ou compartilhados.

---

# 47. Agents Area

A interface deve mostrar:

- agentes disponíveis;
- Agent Runs;
- status;
- custo;
- modelo;
- duração;
- artifacts;
- errors;
- approvals;
- eval health.

Não exigir uso do TUI Eve para operação diária.

---

# 48. Team agentic inicial

```text
Marketing Lead
├── Product Marketer
├── Product & Domain Specialist
├── Audience Intelligence
├── Content Marketer
├── Creative Producer
├── Social Media Coordinator
├── SEO
└── Email
```

Segunda wave:

```text
├── Paid Media Strategist
└── Performance Optimizer
```

Disponibilidade atual do repositório: Marketing Lead e sete especialistas Eve, incluindo os cinco originais, Product & Domain Specialist e Creative Producer. Audience Intelligence, Paid Media Strategist, Performance Optimizer e Lead Qualification Agent são planejados; o diagrama acima representa composição alvo, não agentes já instalados.

---

# 49. Product & Domain Advisor por cliente

Cada Client Workspace pode configurar seu Advisor Profile.

Fluxo:

```text
Client Workspace
↓
Advisor Profile
↓
product-domain-specialist
↓
Product Context
+
Domain Pack
+
Client Sources
+
Policies
```

O agente continua genérico.

---

# 50. Data isolation

Isolamento obrigatório entre:

- Agency Tenants;
- Client Workspaces;
- Products quando policy exigir.

Nenhum tool call pode aceitar somente um ID e confiar que o modelo tem autorização.

Authorization deve ser server-side.

---

# 51. System of Record

Supabase/PostgreSQL é a fonte oficial para dados estruturados.

Eve session state não é System of Record.

Notion não é System of Record.

Blob/storage binário não é System of Record para estado de negócio.

---

# 52. Observabilidade

OpenTelemetry deve correlacionar:

```text
agency_id
client_workspace_id
product_id
campaign_id
agent_run_id
artifact_id
experiment_id
approval_id
trace_id
```

IDs de alta cardinalidade não devem ser usados indiscriminadamente como labels de métricas agregadas.

---

# 53. Audit

Registrar ações como:

- login;
- membership change;
- integration connect;
- approval;
- publish;
- send;
- spend;
- budget change;
- pause/resume;
- Product Context approval;
- Domain Pack approval;
- Advisor Profile change.

---

# 54. Requisitos funcionais

| ID | Requisito | Critério de aceite |
|---|---|---|
| FR-01 | Gerenciar Agency Tenants | Um tenant não acessa dados de outro por UI, API, tool ou integração |
| FR-02 | Gerenciar múltiplos clientes | Agência cria e administra vários Client Workspaces isolados |
| FR-03 | Gerenciar memberships por escopo | Usuário pode ter papel na agência e papéis diferentes por cliente |
| FR-04 | Cadastrar Products/Brands por cliente | Cada produto possui owner e contexto próprio |
| FR-05 | Configurar Advisor Profile por cliente/produto | Cliente usa especialista de segmento sem alterar agentes genéricos |
| FR-06 | Versionar Product Context | Versões aprovadas são imutáveis e rastreáveis |
| FR-07 | Gerenciar Domain Packs | Packs são versionados e associados sem contaminar outros clientes |
| FR-08 | Criar solicitações de trabalho | Request gera WorkItem/AgentRun rastreável |
| FR-09 | Acompanhar Agent Runs | UI mostra status, outputs, custo, falhas e approvals |
| FR-10 | Criar Audience Research | Pesquisa registra fontes e evidências |
| FR-11 | Criar Segments e Personas | Persona possui version, evidence, confidence e status |
| FR-12 | Gerenciar Campaigns | Campaign vincula cliente, produto, público, budget, canais e targets |
| FR-13 | Gerenciar Content Artifacts | Conteúdo é versionado e canônico no OS |
| FR-14 | Produzir Creative Sets | Brief gera peças e variantes rastreáveis |
| FR-15 | Produzir imagens | Assets registram provider, custo, direitos e versão |
| FR-16 | Produzir landing pages/books | Entregas possuem preview, revisão e approval |
| FR-17 | Produzir vídeo/voz | Fase posterior com providers e cost guardrails |
| FR-18 | Gerenciar Approval Inbox | Aprovações ficam centralizadas e escopadas |
| FR-19 | Conectar Meta por cliente | Conta é isolada e credentials não chegam ao modelo |
| FR-20 | Conectar Google Ads por cliente | Conta e customer IDs ficam escopados |
| FR-21 | Conectar TikTok Ads por cliente | Conta fica escopada ao Client Workspace |
| FR-22 | Planejar Paid Media | Agent produz plano sem executar spend automaticamente |
| FR-23 | Criar Experiments | Hypothesis, arms, metrics e resultados ficam no OS |
| FR-24 | Importar métricas | Métricas preservam origem e definição |
| FR-25 | Normalizar métricas | Dashboard compara canais usando definição canônica |
| FR-26 | Acompanhar publicações | Artifact publicado mantém external ID e performance |
| FR-27 | Exibir Performance Dashboard | Usuário analisa canal, campanha, audience e creative |
| FR-28 | Produzir recommendations | Performance Optimizer cria recommendations tipadas |
| FR-29 | Gerenciar budget recommendations | Mudanças possuem limits, evidence, reason e approval |
| FR-30 | Aprovar ação externa | Publish/send/spend/delete requer policy válida |
| FR-31 | Executar ações idempotentes | Retry não duplica ação externa |
| FR-32 | Dashboard multi-cliente | Agência enxerga visão consolidada apenas dos clientes autorizados |
| FR-33 | Client Portal no MVP | Cliente acessa Overview, Campaigns, Creatives, Approvals, Performance, Reports e Requests somente em seu Workspace; dados internos da agência e de outros clientes ficam ocultos |
| FR-34 | Gerenciar integrações | Cada cliente conecta e revoga suas próprias contas |
| FR-35 | Gerenciar custos | Custos de IA/media generation são atribuídos a cliente/campanha |
| FR-36 | Auditar ações | Ações críticas podem ser reconstruídas |
| FR-37 | Operar sem Notion | Fluxos principais funcionam sem Notion |
| FR-38 | Notion opcional | Import/export é idempotente e não vira dependência |
| FR-39 | Multi-idioma futuro | Contextos e conteúdos podem evoluir para múltiplos idiomas |
| FR-40 | Offboarding de cliente | Revogação desconecta integrações e preserva/exporta dados conforme policy |
| FR-41 | Oferecer Engagement por canal | Os seis tipos de canal são modelados; apenas capacidades de integrações efetivamente habilitadas aparecem como operáveis |
| FR-42 | Operar Agentic Email | Campaigns, broadcasts, sequences, segments, templates, experiments, automations delimitadas, performance e AI recommendations vinculam versões ao Client |
| FR-43 | Autorizar envio real | Consentimento, supressão, audience/payload snapshot, role, policy e idempotência são verificados antes do envio; retry incerto não duplica disparo |
| FR-44 | Preparar Lead Qualification futura | Lead, identidade, origem, qualificação, conversa, evento, consentimento e handoff têm ownership por Client; CRM retém pipeline e vendas |
| FR-45 | Operar Web UI como superfície principal | Agency, Client e Portal suportam fluxo diário; Marketing Lead é contextual, sem chat como homepage |

---

# 55. Requisitos não funcionais

## Security
- least privilege;
- RLS;
- OAuth tokens server-side;
- secret redaction;
- prompt injection controls;
- audit.

## Reliability
- idempotency;
- retries limitados;
- health checks;
- fallback;
- reconciliation.

## Observability
- OpenTelemetry;
- trace correlation;
- AI telemetry;
- connector telemetry.

## Performance
- UI responsiva;
- dashboards com caching/aggregation quando necessário;
- imports assíncronos.

## Scalability
- múltiplas agências;
- múltiplos clientes;
- múltiplas contas de mídia;
- execução paralela de agents.

---

# 56. Requisitos de privacidade

Dados de clientes devem respeitar:

- minimização;
- finalidade;
- retenção;
- deleção;
- isolamento;
- consentimento quando aplicável.

First-party data usada para Audience Intelligence deve ser governada.

---

# 57. Métricas de sucesso do produto

## Agência
- tempo para onboard de cliente;
- clientes ativos;
- campanhas gerenciadas;
- aprovação média;
- retrabalho;
- margem operacional;
- custo agentic.

## Cliente
- campaign performance;
- CPL;
- CPA;
- ROAS;
- leads;
- conversions;
- experiment velocity.

## Agentic
- Agent Run success;
- correction rate;
- advisory acceptance;
- creative approval rate;
- recommendation acceptance;
- agent cost.

---

# 58. Learning Loop

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

---

# 59. Escopo por fases

As fases abaixo registram a decomposição anterior. A sequência vigente de produto é o [Roadmap](./ROADMAP.md), reconciliado com o [Product Update Plan](../harness/MARKETING_OS_PRODUCT_UPDATE_PLAN.md): Client Portal is part of the MVP; métricas básicas entram cedo; Engagement Email sucede o core e integra o MVP; WhatsApp, Lead Qualification e CRM são ondas futuras.

## Fase 1 — Agency Control Plane
- Agency Tenant;
- Client Workspace;
- RBAC;
- Supabase Auth/RLS;
- Product;
- Product Context;
- Campaign;
- Artifact;
- Approval;
- basic dashboard.

## Fase 2 — Agent Operations
- AgentRun;
- Marketing Lead integration;
- Product/Domain Advisor;
- Content;
- Social;
- SEO;
- Email.

## Fase 3 — Creative + Audience
- Audience Intelligence;
- Segments;
- Personas;
- Creative Studio;
- image generation;
- experiments.

## Fase 4 — Paid Media Read/Plan
- Meta connector;
- Google Ads connector;
- TikTok connector;
- metrics read;
- account mapping;
- Paid Media Strategist.

## Fase 5 — Paid Media Controlled Execution
- campaign/ad creation;
- publish approval;
- budget approval;
- experiment execution.

## Fase 6 — Performance Optimization
- normalized metrics;
- Performance Optimizer;
- recommendations;
- creative feedback loop.

## Fase 7 — Bounded Automation
- JEV;
- deterministic guardrails;
- limited autoexecution.

---

# 60. Fora do escopo inicial

- auto-spend irrestrito;
- agente autônomo sem approval;
- um agente hardcoded por cliente;
- um agente hardcoded por segmento;
- um agente separado por canal sem necessidade;
- white-label completo;
- billing complexo da plataforma;
- auto-optimization sem dados suficientes.
- CRM completo, pipeline de vendas e telephony suite;
- inbox omnichannel amplo e chatbot builder genérico;
- WhatsApp, SMS, Instagram DM, Facebook Messenger e Web Chat operacionais no primeiro release.

---

# 61. Critérios de ready para MVP de agência

O MVP é considerado operacional quando:

- multi-tenancy entre Agency Tenants passa testes;
- Client Workspace isolation passa testes;
- roles funcionam;
- Product Context funciona;
- Campaign funciona;
- Requests/AgentRuns funcionam;
- Artifact/Approval funciona;
- dashboard agência/cliente existe;
- ao menos uma integração externa funciona de ponta a ponta;
- OTel está ativo;
- audit log está ativo;
- Eve opera usando contexto do cliente sem misturar tenants.
- Client Portal e métricas básicas suportam revisão e resultados por Client;
- Agentic Email percorre Segment → estratégia → conteúdo/criativo → broadcast ou sequence → aprovação → envio autorizado → métricas → aprendizado.

---

# 62. Critérios de ready para Paid Media

Antes de habilitar ações reais:

- connector auth seguro;
- account mapping;
- approval policy;
- audit;
- idempotency;
- metrics freshness;
- budget policy;
- rollback/reconciliation;
- test account/sandbox validado.

---

# 63. Critérios de ready para auto-optimization

Só depois de:

- histórico suficiente;
- guardrails definidos;
- evals;
- confidence calibration;
- human override;
- rollback;
- audit;
- approval explícito da agência/cliente.

---

# 64. Questões abertas

1. O top-level será chamado Agency ou Organization no modelo técnico?
2. A plataforma atenderá apenas agências no MVP ou também marcas diretas?
3. Quais roles exatos serão necessárias?
4. Qual storage de assets será escolhido?
5. Qual provider de imagem será inicial?
6. Qual provider de vídeo será inicial?
7. Qual modelo de atribuição será MVP?
8. Qual canal de Paid Media será integrado primeiro?
9. Client Advisor será configurado por Client ou por Product?
10. Quais Domain Packs estarão disponíveis no piloto?
11. Como first-party data entrará no Audience Intelligence?
12. Qual policy de retenção por cliente?
13. Qual política de autoapproval?
14. Qual limite de budget change no futuro?
15. Resend ou Brevo será o primeiro adapter do OS e qual o recorte inicial de sequences/automations?
16. Quais critérios de identidade, retenção e qualificação liberam o Lead Qualification Agent futuro?
17. Qual CRM recebe o primeiro handoff e quais campos de feedback são permitidos?

---

# 65. Resultado esperado

O Marketing Management OS deve permitir que uma agência opere:

```text
MANY CLIENTS
+
MANY PRODUCTS
+
MANY CAMPAIGNS
+
MANY CHANNEL ACCOUNTS
+
MANY AGENT RUNS
```

com isolamento, contexto e rastreabilidade.

O sistema final não é apenas um time de agentes.

É:

```text
A MULTI-TENANT MARKETING OPERATING SYSTEM
FOR AGENCIES
WITH
AGENTIC EXECUTION
+
CREATIVE PRODUCTION
+
PAID MEDIA
+
PERFORMANCE MANAGEMENT
+
CONTINUOUS LEARNING
```
