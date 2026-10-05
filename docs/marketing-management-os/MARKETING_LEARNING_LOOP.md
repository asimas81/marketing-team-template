# MARKETING_LEARNING_LOOP

## Ciclo canônico

```text
Product Context + Domain Pack + Client Policy
→ Audience Research → Segment/Persona hypotheses
→ Campaign strategy → Content/Creative
→ Experiment/Paid Media/Publications
→ Native + normalized metrics
→ Performance recommendation
→ Deterministic policy → Human approval when required → External action
→ New evidence → review of Persona, Product Context, Domain Pack and strategy
```

O OS versiona cada entrada e saída e mantém a linha de proveniência `Client → Product → Campaign → AgentRun → Artifact/variant → Approval → ExternalAction → MetricSnapshot → Recommendation`. Dados observados não atualizam automaticamente Product Context, Domain Pack ou Persona validada. A mudança vira proposta, diff, revisão e versão nova. Uma recomendação `CREATE_VARIANT` gera novo CreativeBrief e Experiment, com aprovação própria.

O ciclo usa evidência com fonte, data, definição, confiança e limitações. Métrica agregada não prova causalidade; experimento inconclusivo preserva incerteza. O Lead Eve orquestra trabalho cognitivo de um Client por execução; analytics cross-client roda no Control Plane e entrega apenas agregado autorizado. JEV e automação limitada são fases posteriores sujeitas a guardrails e evals.

## Email primeiro, Engagement expansível

O loop passa também por `Audience → Campaign Goal → Email Strategy → Content/Creative → Sequence/Broadcast → Approval → Resend/Brevo → EngagementEvent/Metrics → Performance → Learning`. O primeiro canal planejado é `EMAIL`; WhatsApp, SMS, Instagram DM, Facebook Messenger e Web Chat só participam após integração e definição de métricas próprias. Eventos observados preservam provider, janela, freshness e limitações; abertura/clique não são prova isolada de conversão. AI recommendations vinculam hipótese, evidência, impacto esperado, risco e ação proposta, com nova aprovação antes de executar. `LeadQualification` e CRM Handoff, quando futuros, poderão fornecer feedback permitido para medir qualidade, sem importar pipeline comercial como estado do OS. O [Agentic Email](./AGENTIC_EMAIL_MARKETING_SPEC.md) detalha o primeiro percurso.
