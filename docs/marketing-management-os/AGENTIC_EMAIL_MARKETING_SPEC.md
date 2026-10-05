# AGENTIC_EMAIL_MARKETING_SPEC

## Objetivo e fase

Email é o primeiro canal planejado da área [Engagement](./ENGAGEMENT_ARCHITECTURE.md), após o core de agência, Client Workspace, Campaign, Artifact, Approval, Audience e métricas básicas. A experiência combina operação estruturada na Web UI com propostas de agentes, preservando controle humano sobre envio real. O especialista Eve `email` existente adapta copy pronta para inbox e opera Resend no template atual; a experiência de Agentic Email descrita aqui é alvo do OS, não uma funcionalidade já entregue.

## Capacidades de produto

| Capacidade | Comportamento alvo |
| --- | --- |
| Campaigns | Vincular objetivo, Product, Campaign, Segment, oferta, período e metas no Client |
| Broadcasts | Preparar envio único a um audience snapshot, com versão de conteúdo e destino |
| Sequences | Ordenar mensagens, intervalos, condições de entrada/saída e estado por execução |
| Segments | Usar definições e versões de audiência, tamanho estimado e elegibilidade no momento do envio |
| Templates | Reutilizar estrutura de email sem perder versão de copy, claims, identidade e layout |
| Experiments | Registrar hipótese, variantes, métrica primária, janela e decisão; resultados não viram causalidade automática |
| Automations | Permitir somente regras delimitadas, observáveis e autorizadas; sem envio autônomo irrestrito |
| Performance | Preservar eventos e métricas nativas, definições, janela, fonte, freshness e limitações |
| AI recommendations | Produzir sugestões evidenciadas de assunto, CTA, sequência, público ou horário, sem executá-las diretamente |

## Fluxo canônico

```text
Audience → Campaign Goal → Email Strategy → Content / Creative → Sequence
→ Approval → Resend / Brevo → Metrics → Performance → Learning
```

`Content Marketer` origina a peça; `email` a adapta para assunto, preview, corpo, texto simples, links, alt text e encaixe de canal. `creative-producer` pode fornecer visual revisável. Domain Advisor intervém quando Product/Domain Policy ou claims exigirem. Marketing Lead encadeia essas entregas pelo Campaign Brief e versões fixadas. A estratégia, a seleção de Segment e uma recommendation são propostas; só o Control Plane grava a decisão de negócio e libera execução autorizada.

## Objetos e estados

`EmailCampaign` especializa uma Campaign de Engagement sem substituir a Campaign principal. `EmailBroadcast`, `EmailSequence`, `EmailSequenceStep`, `EmailTemplate`, `EmailExperiment` e `EmailPerformanceSnapshot` pertencem ao Client e referenciam Product/Campaign, Segment/versão, Artifact/versão, provider e execução quando aplicável. A campanha de email pode conter broadcasts e sequences; cada envio lógico tem chave de idempotência e correlação. Um `draft` editorial pode evoluir para `prepared`, `scheduled`, `sending`, `sent`, `failed` ou `reconciliation_required`; agendamento e envio usam autorizações específicas. Evento de entrega, abertura, clique ou resposta é observado com ressalvas de cobertura e não prova inbox placement.

## Aprovação, integração e UI

A Web UI deve permitir montar Campaign, Broadcast ou Sequence, revisar conteúdo e variantes, inspecionar Segment e consentimento, aprovar um snapshot e acompanhar execução/resultado. `DRAFT`, `PREPARE`, `SCHEDULE`, `SEND` e `PUBLISH` são intenções distintas; aprovação editorial não autoriza `SEND`. O [Approval Model](./APPROVAL_MODEL.md) define o workflow de produto; o [Harness](../harness/APPROVAL_ENFORCEMENT_POLICY.md) define enforcement. Supressão, opt-out, autorização por Client, identidade de remetente, rate limit, retries e duplicate-send prevention são gates de execução do Harness, não instruções de copy.

Resend é a integração operacional existente no template Eve; Resend e Brevo são candidatos do OS e exigem adapters com capacidades declaradas, conta vinculada ao Client e reconciliação de IDs/eventos. A escolha de provider inicial, o alcance de sequences/automations no primeiro release, atribuição e retenção ficam abertos para SPEC. Sem integração configurada, o usuário pode preparar e revisar, mas não enviar.

## Critérios para SPEC e aceite

- Um usuário autorizado prepara um broadcast e uma sequence dentro de um Client, com Segment e versões fixadas, preview e trilha de aprovação.
- Uma mudança de público, conteúdo, remetente ou horário exige reavaliar a autorização executável.
- O commit de envio real passa por consentimento, supressão, policy e idempotência; resultado incerto entra em reconciliação e não gera disparo duplicado.
- Métricas de Email aparecem por Campaign, Broadcast, Sequence e variante com origem, janela e freshness; recommendation referencia evidência e requer nova decisão antes de execução.
- Testes de isolamento entre dois Clients, revogação de integração e opt-out bloqueiam o caminho de envio correspondente.
