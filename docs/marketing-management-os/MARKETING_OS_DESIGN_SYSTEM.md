# MARKETING_OS_DESIGN_SYSTEM.md

# Marketing Management OS — Design System

**Versão:** 1.0  
**Tipo:** B2B SaaS / Agency Operations / Data-Dense / AI-Native  
**Direção:** premium, calma, precisa, operacional e confiável.

## 1. Princípio visual

A interface deve parecer uma plataforma de operação de agência, não um chatbot.

Evitar:
- neon AI
- estética consumer
- excesso de gradients
- cards excessivamente grandes
- chat como homepage
- ilustrações de robôs

Priorizar:
- scanability
- context awareness
- dense data with low noise
- clear status
- actionability
- confidence

## 2. Inspiração combinada

HighLevel → Agency/Client hierarchy  
Vendasta → Client portal  
AgencyAnalytics + Reportei → Dashboards  
mLabs → Workflow/approvals  
Jasper → Brand/Audience/Knowledge context  
Smartly → Creative + Media + Intelligence loop

## 3. Estrutura de marca

### Platform Chrome
Neutro, consistente e estável.

### Tenant Branding
Configurável por Agency e, no portal, opcionalmente por Client:
- logo
- accent
- favicon
- portal header
- report branding

Cores semânticas não podem ser sobrescritas pelo tenant.

## 4. Tipografia

Recomendado: Geist  
Fallback: Inter, system-ui, sans-serif

Escala:
- Display 32/40 600
- H1 28/36 600
- H2 22/30 600
- H3 18/26 600
- Body 14/22 400
- Body Strong 14/22 600
- Small 13/18 400
- Caption 12/16 500
- Metric 24/30 600

## 5. Color System

### Neutrals
- bg-app: #F6F7F9
- bg-surface: #FFFFFF
- bg-subtle: #F9FAFB
- bg-dark: #111827
- text-primary: #101828
- text-secondary: #475467
- text-muted: #667085
- border: #E4E7EC
- border-strong: #D0D5DD

### Platform Brand
- brand-50: #F3F3FF
- brand-100: #E7E7FF
- brand-500: #6366F1
- brand-600: #5558E8
- brand-700: #4547C8

### Intelligence Accent
- intel-50: #ECFDF9
- intel-500: #14B8A6
- intel-600: #0D9488

### Semantic
- success: #12B76A
- warning: #F79009
- danger: #D92D20
- info: #2E90FA

## 6. Spacing
Base 4px.
Escala: 4, 8, 12, 16, 20, 24, 32, 40, 48, 64.

Sidebar: 240px  
Collapsed: 72px  
Page padding desktop: 24–32px  
Card gap: 16px

## 7. Radius
- small 6px
- default 8px
- card 12px
- large 16px
- pill 999px

## 8. Navigation

### Agency Sidebar
- Dashboard
- Clients
- Requests
- Approvals
- Reports
- Agents
- Integrations
- Settings

### Client Sidebar
- Overview
- Product & Advisor
- Audiences
- Campaigns
- Content
- Creative Studio
- Experiments
- Engagement
- Paid Media
- Performance
- Agents
- Integrations
- Settings

## 9. Context Switcher

Componente crítico no topo:

Agency → Client → Product

Exemplo:
Nora Agency › Doce Capítulo › Product: Doce Capítulo

Deve permitir search rápido e reduzir erro de contexto multi-tenant.

## 10. Page Header

Padrão:
Breadcrumb  
Title  
Description  
Secondary actions  
Primary action

## 11. Cards

### Metric Card
CPL  
R$ 38,42  
↓ 12,4%

### Status Card
Creative Production  
3 in review  
2 approved

### Insight Card
Campaign B deteriorating 28%  
[Investigate]

### Client Card
Logo, client, campaigns, spend, CPA, approvals, health.

## 12. Tables

Suportar:
- sorting
- filtering
- search
- bulk selection
- saved views
- sticky header
- column visibility
- density toggle

## 13. Workflow Board

Colunas:
Backlog → Strategy → Production → Internal Review → Client Review → Approved → Scheduled → Published

Cards exibem:
- client
- campaign
- artifact
- assignee/agent
- due date
- approval state

## 14. Agent Run

Mostrar operação e evidência, não avatar decorativo.

Exemplo:
Marketing Lead — RUNNING  
Started 2m ago  
Current: Creative Producer  
Cost: $0.82

Timeline:
Lead → Audience Intelligence → Domain Advisor → Creative Producer

## 15. AI Recommendation Pattern

Toda recomendação deve ter:
- recommendation
- confidence
- evidence
- impact
- risk
- action

Nunca apenas “AI suggests”.

## 16. Client Portal

Menu simples:
- Overview
- Campaigns
- Creatives
- Approvals
- Performance
- Reports
- Requests

Ocultar:
- internal agent config
- cross-client metrics
- internal cost
- technical settings

## 17. Audience Intelligence UI

Tabs:
Segments | Personas | Research | Evidence | Hypotheses

Persona detail:
- status
- confidence
- goals
- barriers
- evidence
- experiments
- performance
- version history

## 18. Creative Studio

Tabs:
Briefs | Creative Sets | Drafts | In Review | Approved | Published

Detail:
Preview | Versions | Comments | Claims | Sources | Performance

## 19. Experiment UI

Mostrar:
- hypothesis
- control
- variants
- primary metric
- sample
- duration
- confidence
- recommendation

## 20. Paid Media UI

Tabs:
Overview | Accounts | Campaigns | Ads | Experiments | Budgets | Recommendations

KPIs:
Spend, Target, CPA/CPL, Conversions, Pacing, Alerts

## 21. Performance UI

Filters:
Period, Channel, Campaign, Persona, Creative

KPIs:
Spend, Leads, CPL, Conversions, CPA, ROAS

Sections:
Trend, Channel Mix, Creative Winners, Audience Winners, Experiments, Recommendations, Change History

## 22. Engagement UI

MVP:
Email

Future:
Email, WhatsApp, SMS, Instagram DM, Messenger

Tabs:
Campaigns | Sequences | Segments | Templates | Conversations | Performance

## 23. Approval UI

Toda aprovação responde:
- o que está sendo aprovado?
- quem pediu?
- o que vai acontecer?
- qual custo?
- o que mudou?
- qual versão?

Ações:
Request Changes | Reject | Approve

Ações financeiras destacam REAL SPEND.

## 24. Chat / Marketing Lead

Chat deve ser utility surface:
- right-side drawer
- command palette
- contextual “Ask about this campaign”

Não usar chat como homepage.

## 25. Command Palette

Ctrl/Cmd + K:
- switch client
- new request
- create campaign
- open approval
- ask lead
- find artifact

## 26. Responsive

Desktop-first para operação.
Mobile focado em:
- dashboards
- approvals
- comments
- quick actions

## 27. Accessibility

WCAG AA baseline:
- keyboard
- focus
- contrast
- labels
- textual equivalents for charts
- non-color status cues

## 28. White Label

Agency-level:
- logo
- accent
- custom domain
- portal title

Client Portal:
- client logo
- optional co-branding

## 29. Component Library

Recomendado:
Radix primitives + shadcn/ui ou equivalente + domain components.

Componentes específicos:
- AgencySwitcher
- ClientSwitcher
- AgentRunTimeline
- ApprovalCard
- PersonaEvidencePanel
- CampaignHealthBadge
- CreativePreview
- ExperimentComparison
- PerformanceRecommendation
- IntegrationHealth
- MetricCard

## 30. Regra final

Toda tela deve responder visualmente:
- Where am I?
- Which client?
- What is happening?
- What needs my attention?
- What changed?
- What happens if I click this?

`DESIGN_SYSTEM_READY_FOR_PROTOTYPE = true`
