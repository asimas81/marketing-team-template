# EXPERIMENTATION_MODEL

## Entidades e desenho

`Experiment` pertence a Client e Campaign, referencia MarketingHypothesis, tipo (`CREATIVE`, `AUDIENCE`, `MESSAGE`, `OFFER`, `LANDING_PAGE`, `CHANNEL`, `BUDGET`, `BIDDING`), método `MARKETING_OS_EXPERIMENT` ou `NATIVE_PLATFORM_EXPERIMENT`, owner, status e versão. `ExperimentArm` fixa artifact/creative/audience/offer e versão; `ExperimentMetric` fixa definição canônica, janela e alvo; `ExperimentObservation` guarda snapshot observado, fonte e frescor; `ExperimentDecision` registra leitura, evidência e aprovador.

Antes do lançamento, registrar hipótese falsificável, controle/tratamento, única variável intencional quando cabível, métrica primária, amostra/duração mínimas, start/stop rule, conta/canal e riscos. A plataforma pode executar mecanismo nativo, mas o OS mantém governança e resultado canônico. Cross-channel exige comparabilidade de atribuição e não deve receber inferência causal quando desenho não sustenta. Mudança de braço, audiência, budget ou métrica após aprovação cria versão e nova autorização.

Estados sugeridos `DRAFT → READY_FOR_REVIEW → APPROVED → RUNNING → COMPLETED → ANALYZED`, com `PAUSED`, `CANCELLED`, `INCONCLUSIVE`. `START_EXPERIMENT` e alterações com publicação/gasto exigem aprovação de execução; rascunho e recomendação podem ser automáticos. Budget/bidding nunca autoexecutam no MVP. O resultado mostra intervalo, amostra, janela, limitações e decisão, inclusive inconclusivo. UI apresenta hypothesis, arms, timeline, métricas e resultado por Client. Evals cobrem evidência, desenho, stop rules e claims causais indevidos.
