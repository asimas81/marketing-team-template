# MARKETING_OS_PROTOTYPE_INSPIRATION.md

# Marketing Management OS — Inspiração de Protótipo

**Versão:** 1.0  
**Objetivo:** orientar a criação do primeiro protótipo do Agentic Marketing Operations Platform for Agencies.

## 1. Estratégia de referência

Não copiar um concorrente inteiro.

Usar a melhor referência por problema:

| Área | Referência | O que absorver |
|---|---|---|
| Agency / Clients | HighLevel | hierarchy, subaccounts, switching, dense management UI |
| Client Portal | Vendasta | client-facing dashboard, reporting, products/services, communication |
| Reporting | AgencyAnalytics | KPI clarity, white-label, client dashboard |
| Multi-channel Metrics | Reportei | project/client context, unified channel reporting |
| Workflow / Approval | mLabs | internal/client review flow |
| Brand / Audience Context | Jasper | reusable brand, knowledge and audience context |
| Creative + Media Intelligence | Smartly | creative/media/performance learning loop |

## 2. HighLevel

Inspirar:
- Agency → Clients hierarchy
- client/subaccount list
- search and filters
- account switching
- operational density

Evitar:
- CRM-heavy navigation
- excessive modules
- clutter

Nossa versão deve ser marketing-operations-first.

## 3. Vendasta

Inspirar:
- client portal as branded home
- key metrics at a glance
- client self-service
- products/services visibility
- communication access

Nossa evolução:
Performance + Campaigns + Approvals + Requests + Creative Review.

## 4. AgencyAnalytics

Inspirar:
- clean KPI row
- dashboards by client
- date filters
- white-label
- shareability
- multi-client executive view

Nossa evolução:
Metric + AI interpretation + recommended action.

## 5. Reportei

Inspirar:
- project/client context
- unified multichannel metrics
- executive overview
- timeline
- strong Brazilian agency workflow fit

Nossa evolução:
reporting → recommendation → approval → action → learning.

## 6. mLabs

Inspirar:
Backlog → Strategy → Production → Internal Review → Client Review → Approved → Scheduled → Published

Nossa evolução:
show active agent, AgentRun, artifact version and approval policy inside each item.

## 7. Jasper

Inspirar:
- Brand Voice
- Audiences
- Knowledge
- reusable context objects
- source-aware context

Nossa evolução:
Audience → Evidence → Confidence → Version → Hypotheses → Experiments → Performance.

## 8. Smartly

Inspirar:
creative + media + performance + continuous learning.

Nossa versão deve simplify enterprise complexity for agency workflows.

## 9. Prototype Information Architecture

### Agency Level
- Dashboard
- Clients
- Requests
- Approvals
- Reports
- Agents
- Integrations
- Settings

### Client Level
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

## 10. Screen 01 — Agency Dashboard

Objetivo: responder em 10 segundos:
- quais clientes precisam de atenção?
- quais campanhas estão fora de meta?
- quais approvals estão pendentes?
- quais Agent Runs falharam?
- quanto está sendo investido?

Wireframe:

Agency Dashboard
- Spend
- Leads
- CPA
- Active Clients
- Needs Attention
- Client Performance Table
- Pending Approvals
- Integration Health

## 11. Screen 02 — Clients

Referência principal: HighLevel.

Tabela:
- Client
- Account Manager
- Active Campaigns
- Spend
- CPA
- Approvals
- Integration Health
- Status

## 12. Screen 03 — Client Overview

Referência: Vendasta + AgencyAnalytics.

Header:
Client Logo | Client Name | Account Manager | Advisor

Widgets:
- current campaigns
- performance
- approvals
- recent activity
- recommendations

## 13. Screen 04 — New Request

Cards:
- Create Campaign
- Create Content
- Create Creative
- Analyze Performance
- Research Audience
- Other

Context:
Client / Product / Campaign

Marketing Lead assists completion.

## 14. Screen 05 — Agent Run

Timeline:
- Product Marketer
- Audience Intelligence
- Domain Advisor
- Content
- Creative Producer
- Paid Media

Mostrar:
- status
- duration
- cost
- artifacts
- errors
- approvals

## 15. Screen 06 — Audiences

Tabs:
Segments | Personas | Research | Evidence | Hypotheses

Persona Card:
- status
- confidence
- evidence count
- experiments
- recent performance

## 16. Screen 07 — Campaign Detail

Hero screen.

Header:
- Goal
- Budget
- Spend
- CPL/CPA
- Status

Tabs:
Overview | Work | Content | Creatives | Experiments | Paid Media | Performance | Activity

## 17. Screen 08 — Creative Studio

Referência: Smartly + Figma-like review.

Grid visual:
Ad A | Ad B | Carousel | Reel

Each card:
- preview
- status
- channel
- performance if published

Detail:
Preview | Versions | Comments | Claims | Sources | Performance

## 18. Screen 09 — Approval Inbox

Referência: mLabs.

Filters:
All | Internal | Client | Creative | Publication | Budget

Approval detail:
- what is being approved
- destination
- audience
- cost/spend
- changes since last approval
- version

Actions:
Request Changes | Reject | Approve

## 19. Screen 10 — Paid Media

Referência: HighLevel simplicity + Smartly intelligence.

Top:
Meta | Google | TikTok

KPIs:
Spend | CPL/CPA | Conversions | Pacing

Then:
- campaigns
- experiments
- recommendations

## 20. Screen 11 — Experiment

Show:
- hypothesis
- control
- variant
- primary metric
- sample
- confidence
- recommendation

Actions:
Create Variant | Apply Recommendation

## 21. Screen 12 — Performance

Referência: AgencyAnalytics + Reportei.

Filters:
Period | Channel | Campaign | Persona | Creative

KPIs:
Spend | Leads | CPL | Conversions | CPA | ROAS

Below:
- Trend
- Channel Mix
- Creative Winners
- Audience Winners
- Experiments
- Recommendations
- Change History

## 22. Screen 13 — Engagement

MVP:
Email

Tabs:
Campaigns | Sequences | Segments | Templates | Performance

Future channel selector:
Email | WhatsApp | SMS | Instagram | Messenger

## 23. Screen 14 — Client Portal

Menu:
Overview | Campaigns | Creatives | Approvals | Performance | Reports | Requests

More premium and simpler than internal agency UI.

Hide agent internals and operational complexity.

## 24. Screen 15 — Product & Advisor

Tabs:
Product Context | Advisor Profile | Domain Packs | Claims | Sources | Version History

Referência conceitual: Jasper IQ.

## 25. AI interaction pattern

Não usar chat gigante como homepage.

Use:
- right-side assistant drawer
- contextual command bar
- “Ask about this client”
- “Ask about this campaign”
- “Why this recommendation?”
- “Create a variant”

## 26. Prototype Priority

### P0
- Agency Dashboard
- Clients
- Client Overview
- New Request
- Agent Run
- Campaign Detail
- Creative Studio
- Approval Inbox
- Performance
- Client Portal

### P1
- Audiences
- Paid Media
- Experiment
- Product & Advisor
- Engagement

### P2
- Integrations
- Reports builder
- advanced agent settings
- billing/admin

## 27. Prototype acceptance test

O protótipo deve provar que um usuário consegue:
1. escolher um cliente
2. criar uma solicitação
3. acompanhar agentes
4. abrir uma campanha
5. revisar uma persona
6. revisar criativos
7. aprovar uma peça
8. visualizar paid media
9. entender performance
10. aprovar/rejeitar uma recomendação
11. entrar como cliente e aprovar conteúdo

## 28. Visual tone

High-end B2B SaaS  
Data-dense  
Quiet  
Precise  
AI-native, not AI-themed

No neon.
No robot illustrations.
No chat-first homepage.

`PROTOTYPE_DIRECTION_READY = true`
