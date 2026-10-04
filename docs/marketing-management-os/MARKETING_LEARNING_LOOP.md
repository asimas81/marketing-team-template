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
