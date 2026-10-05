# PERFORMANCE_OPTIMIZATION_MODEL

## Dados e comparabilidade

`CampaignMetricDefinition` define nome, unidade, fórmula, owner e versão; `ChannelMetricMapping` traduz métrica nativa preservando valor bruto; `MetricSnapshot` guarda Client, Product/Campaign/Artifact/variant/conta, fonte, collected/observed_at, timezone, período, janela de atribuição e freshness; `AttributionSnapshot` explicita modelo e diferenças; `PerformanceTarget` fixa meta antes da leitura. Dashboard sinaliza métricas incompatíveis e atraso de dados. Agregação multi-client é SQL sobre Clients autorizados e só usa definições comparáveis.

O futuro `performance-optimizer` lê métricas autorizadas e propõe `PerformanceRecommendation` tipada: `INCREASE`, `KEEP`, `REDUCE`, `PAUSE`, `INVESTIGATE`, `CREATE_VARIANT`. Cada recomendação vincula métricas, baseline, contexto, confiança, limites, custo/impacto e validade. Falta de amostra ou frescor gera `INVESTIGATE`, não ação executável. O especialista não altera budget nem pausa campanha.

Antes e depois de qualquer decisão: regras determinísticas conferem conversões/spend/duração mínimos, janela de atribuição, health da conta, status de campanha, trava de experimento, human hold, limite diário/da campanha/Client/Agency e delta máximo. JEV pode futuramente escolher entre opções estreitas permitidas; não define valor livre de gasto nem substitui policy. Inicialmente `Recommendation → Human Approval → Connector Execution → Reconciliation`; autoexecução fica fora do MVP. Toda mudança financeira tem razão, fonte, ator, aprovação, diff e AuditEvent. `CREATE_VARIANT` abre CreativeBrief/Experiment novo, sem alterar peça aprovada.
