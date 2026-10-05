# Engagement Channel Contract — alvo incremental

## Fronteira e sequência de entrega

`EngagementChannel` é uma abstração do Marketing OS para `EMAIL`, `WHATSAPP`, `SMS`, `INSTAGRAM_DM`, `FACEBOOK_MESSENGER` e `WEB_CHAT`. O contrato entra na SPEC de Engagement; Email é a primeira implementação planejada após o core. Identidade de contato, consentimento e supressão mínimos por Client/canal/finalidade são pré-condições do Email; o Lead model completo, os outros canais, CRM e Lead Qualification continuam futuros. O conector Resend do template Eve é uma capacidade legada de email por usuário, sem ownership e consentimento persistidos no OS; não equivale a este contrato. A [arquitetura funcional](../../marketing-management-os/ENGAGEMENT_ARCHITECTURE.md) e a [spec de Agentic Email](../../marketing-management-os/AGENTIC_EMAIL_MARKETING_SPEC.md) definem a experiência de produto.

Cada adapter declara capacidades realmente disponíveis por canal/conta/versão: outbound, inbound, broadcast, sequence, scheduling, template, receipt, unsubscribe/suppression, rate limit e read status. `UNSUPPORTED` é resultado explícito; não se presume equivalência entre canais. Adapter sabe executar e reconciliar; o OS decide política, consentimento, autorização, cadência e estado. No fluxo alvo do OS, Eve propõe conteúdo/segmento e prepara drafts; a credencial operacional fica no executor server-side e o OS decide o envio. O Resend legado mantém seu gate Eve até migração explícita.

## Entidades canônicas

| Entidade | Identidade e invariantes |
| --- | --- |
| `ChannelIdentity` | Identificador de contato por Client/canal/provider, normalizado, pseudonimizado quando possível, com estado de verificação. É necessário para o primeiro Email mesmo sem Lead completo. Mesmo endereço/número em outro Client não concede vínculo nem consentimento. Na fase de Lead, corresponde ao `LeadIdentity` vinculado ao Lead no modelo de produto; a nomenclatura do payload será fechada na SPEC. |
| `ConsentRecord` | Client, ChannelIdentity e Lead opcional futuro, canal, finalidade, base/forma de coleta, fonte/prova, horário, região quando relevante, estado, versão de policy e revogação. Necessário para Email; ausência, expiração ou opt-out bloqueia SEND. |
| `SuppressionEntry` | Supressão/unsubscribe por Client, canal/identidade e finalidade, com origem e data. Lista global do provedor também deve ser respeitada; não é substituída por estado local. |
| `Lead` / `LeadIdentity` | Futuros: `agency_id`, `client_workspace_id`, `lead_id`, `product_id?`, origem e status de marketing; identidade por canal vinculada sob verificação. Não são pré-requisito do primeiro Email nem representam pipeline comercial. |
| `ConversationThread` | Futura: Client, Lead, canal, `ClientIntegration`/conta, status, participantes autorizados e retenção. Threads de canais distintos não se fundem sem associação verificada. |
| `EngagementEvent` | Tipo `PREPARED`, `SCHEDULED`, `SEND_REQUESTED`, `SENT`, `DELIVERED`, `FAILED`, `RECEIVED`, `OPTED_OUT`, `SUPPRESSED` etc., IDs internos/externos, timestamp, payload hash e proveniência. Evento externo é dado não confiável e deduplicado. |
| `EngagementAction` | Intent de envio por Client, segmento/destinatário e Lead opcional futuro, canal, conta, template/artifact version, horário, custo/volume, consent snapshot, approval, idempotency key e estado reconciliável. |
| `QualificationAssessment` / `CrmHandoff` | Futuros: representações executáveis da `LeadQualification` e do `Handoff` do [modelo de produto](../../marketing-management-os/LEAD_QUALIFICATION_MODEL.md), com evidência/limitações, campos mínimos, status e ID externo. Não criam sales pipeline no OS. |

## Estado e autorização

`DRAFT` cria conteúdo interno; `PREPARE` resolve segmento, conta, identidade, consentimento, supressão, versão, horário e custo sem side effect externo; `SCHEDULE` registra intenção interna e revalidação futura; `SEND` executa entrega real; `PUBLISH` torna conteúdo visível em surface pública. Agendamento dentro do provedor que já garante envio futuro é tratado como `SEND` e exige a mesma autorização. Cada transição valida ClientPolicy, membership, finalidade, opt-in/opt-out, suppression, janela de envio, limites, health/capability do conector e aprovação sobre payload exato. Mudança de qualquer entrada relevante exige novo snapshot/approval.

O OS reserva idempotency key durável por `EngagementAction` e destinatário/variante, grava intent antes do side effect e reconcilia provider message ID/webhook. Timeout ou resposta incerta não dispara retry cego. Inbound valida assinatura/conta, resolve Client pela integração autorizada, deduplica evento e verifica se a resposta/qualificação é permitida. Retry tem backoff e limite por canal; rate limit e suppression vencem qualquer instrução do agente.

## Lead Qualification e CRM futuros

Lead Qualification Agent receberá somente `agency_id`, `client_workspace_id`, `product_id`, `campaign_id`, `lead_id`, `consent_state`, `channel` e `permission_envelope`, mais resumo minimizado recuperado por tool autorizada quando a tarefa exigir. Não recebe a base inteira, threads de outros Leads ou credenciais. Saída é assessment com fonte, confiança, perguntas e proposta de handoff; humano/policy decide contato e CRM sync. CRM connector só envia campos necessários para finalidade aprovada, com mapping, idempotência, audit e revogação. Fontes, scoring, identidade entre canais, retenção e permissões por papel são decisões de SPEC.

## Critérios de entrada

Antes de Email pelo OS: Client ownership, autenticação, consent/suppression, business approval, Resend/Brevo account mapping, identidade do remetente, idempotência, reconciliação, métricas e testes cross-client. Antes de qualquer canal futuro: capability real, política de consentimento e opt-out específicos, ambiente de teste, limites, inbound/receipt quando aplicável, segurança e evals. Ver [Security Policy](../security/SECURITY_POLICY.md) e [Approval Enforcement](../APPROVAL_ENFORCEMENT_POLICY.md).
