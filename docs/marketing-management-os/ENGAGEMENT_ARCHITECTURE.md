# ENGAGEMENT_ARCHITECTURE

## Escopo e fase

Engagement é a capacidade de planejar, preparar, executar e medir interações com públicos no contexto de um Client Workspace. O contrato funcional de canal reconhece `EMAIL`, `WHATSAPP`, `SMS`, `INSTAGRAM_DM`, `FACEBOOK_MESSENGER` e `WEB_CHAT`. Email é o primeiro canal planejado; WhatsApp, SMS, Instagram DM, Facebook Messenger e Web Chat são futuros. A existência de um tipo no modelo não implica conector disponível, permissão de envio ou inbox unificada. O contrato técnico, policies de consentimento, credenciais, rate limit, idempotência e auditoria pertencem ao [Harness Engagement Channel Contract](../harness/contracts/ENGAGEMENT_CHANNEL_CONTRACT.md) e às [policies do Harness](../harness/README.md).

## Modelo funcional

`EngagementChannel` declara tipo, capacidades efetivas e estado por Client Workspace. Uma `ClientIntegration` vincula a identidade/canal externo ao Client autorizado. `EngagementCampaign` referencia Campaign, Product, objetivo e audiência. `EngagementSegment` é uma definição versionada de público; resolução de destinatários ocorre no momento autorizado da execução. `EngagementTemplate` e `EngagementArtifact` registram conteúdo/versionamento por canal. `EngagementSequence` ordena etapas e condições; `EngagementEvent` registra resultado observado de envio, recepção ou interação. `ConversationThread` agrupa trocas quando o canal e a fase oferecerem conversação. Para Email, `Consent`/supressão precisa existir por identidade de contato, finalidade e canal mesmo antes do Lead model completo; futuramente pode vincular-se a LeadIdentity. IDs externos são referências reconciliadas; o OS mantém o estado canônico.

Cada entidade operacional pertence a `(agency_id, client_workspace_id)`; vínculos com Product, Campaign, Segment e Lead devem permanecer no mesmo Client. `EMAIL` admite broadcast e sequence no primeiro recorte. Para os canais futuros, capacidades como outbound, inbound, reply, template, scheduling e webhooks são descobertas por integração, sem pressupor paridade. O [Domain Model](./DOMAIN_MODEL.md) define relações e a [spec de Email](./AGENTIC_EMAIL_MARKETING_SPEC.md) fixa a primeira experiência.

## Fluxo de operação

```text
Audience/Segment → Campaign Goal → Channel Strategy → Content/Creative
→ Artifact/Sequence → Editorial Review → Execution Authorization
→ Channel Provider → Engagement Events/Metrics → Performance → Learning
```

O Control Plane valida Client, integração, identidade de canal, consentimento vigente, supressão, audience snapshot, versão da peça e autorização da ação. A UI mostra preparação, agendamento, envio e publicação como decisões distintas. Respostas incertas exigem reconciliação antes de novo disparo. Dados recebidos viram eventos com origem, instante e correlação; não atualizam Product Context ou Persona sem proposta e revisão. O [Approval Model](./APPROVAL_MODEL.md) define as decisões de negócio e o [Learning Loop](./MARKETING_LEARNING_LOOP.md) liga resultados a hipóteses.

## Superfície Web e fronteira de produto

Engagement é uma área do Client Workspace. O primeiro recorte mostra Email Campaigns, Broadcasts, Sequences, Segments, Templates, Experiments e Performance, com status e aprovações. Navegação de canais futuros é progressiva, conforme integração real e policy. Chat/Marketing Lead pode iniciar ou explicar trabalho no contexto da página, mas a UI de gestão é a superfície principal. O [Design System](../harness/MARKETING_OS_DESIGN_SYSTEM.md) governa UX/UI; a [Prototype Inspiration](../harness/MARKETING_OS_PROTOTYPE_INSPIRATION.md) orienta a tela de Engagement.

O OS cobre aquisição, engajamento, qualificação futura, medição e otimização. Opportunity, pipeline, sales e customer lifecycle pertencem ao CRM. [Lead Qualification](./LEAD_QUALIFICATION_MODEL.md) define o handoff futuro. Um inbox omnichannel amplo permanece fora do escopo inicial.

## Gates de evolução

- Email: contrato de canal, integração Client-scoped, audience e consentimento verificáveis, templates/artefatos versionados, aprovações de envio, deduplicação e métricas reconciliadas.
- WhatsApp e demais canais: identidade, regras de consentimento e capacidades específicas validadas antes de habilitar qualquer ação; ConversationThread/receive só quando houver integração e ownership definidos.
- Lead Qualification e CRM: modelo de Lead, política de dados e handoff revisados antes da primeira sincronização. Nenhum canal ou conector futuro está marcado como pronto.
