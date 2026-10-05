# LEAD_QUALIFICATION_MODEL — roadmap

## Fronteira de produto

O consentimento mínimo por identidade/canal é pré-condição do primeiro Email; o Lead model completo e seu vínculo com esse registro vêm depois.

Lead Qualification é capacidade futura do Marketing OS. O OS cobre `acquire → engage → qualify → measure → optimize`; CRM externo cobre `opportunity → pipeline → sales → customer lifecycle`. O registro de Lead no OS serve para atribuição, consentimento, conversa de marketing, avaliação e handoff. Ele não cria pipeline comercial, forecast ou cadastro mestre de cliente. Os primeiros conectores CRM planejados são HighLevel, HubSpot, RD Station, Pipedrive e Salesforce, todos futuros.

## Modelo conceitual

| Entidade | Finalidade e invariantes |
| --- | --- |
| Lead | Pessoa ou contato identificável no escopo de um Client; estado de marketing, Product/Campaign de origem e retenção; merge explícito e auditado |
| LeadIdentity | Identificador por canal, como email ou handle, vinculado ao Lead e ao Client; não usar identificador externo como autorização |
| LeadSource | Origem, Campaign, canal, touchpoint, momento e evidência de atribuição; fonte desconhecida permanece explícita |
| LeadQualification | Avaliação versionada de critérios, sinais, conclusão, confiança, evidências, ressalvas e revisão humana quando exigida |
| ConversationThread | Sequência de interação por Lead, canal e identidade; disponível apenas em canais com recepção/identidade suportadas |
| EngagementEvent | Fato observado de envio, recebimento, resposta ou ação, com provider, ID externo, tempo e deduplicação |
| Consent | Estado e prova por LeadIdentity, canal, finalidade e momento; opt-out/supressão prevalece sobre campanhas e sequences |
| Handoff | Snapshot minimizado da qualificação, consentimento e referências enviado ao CRM autorizado; estado, external ID, retry/reconciliação e feedback |

Todas essas entidades pertencem a `(agency_id, client_workspace_id)` e só referenciam Product/Campaign/integração do mesmo Client. LeadIdentity traduz a identidade de canal tratada no [Engagement Channel Contract](../harness/contracts/ENGAGEMENT_CHANNEL_CONTRACT.md); a nomenclatura de payload deve ser fechada na SPEC de API. Lead não substitui AudienceSegment: segmento é definição de público; Lead é registro individual sujeito a finalidade, consentimento e retenção. O [Domain Model](./DOMAIN_MODEL.md) situa os vínculos.

## Fluxo futuro

```text
LeadSource → Lead/LeadIdentity → Consent → EngagementEvent/ConversationThread
→ LeadQualification proposta → revisão/policy → Handoff → CRM
→ feedback de resultado permitido → Metrics/Performance/Learning
```

O Lead Qualification Agent é futuro e subordinado ao Marketing Lead. Recebe apenas `agency_id`, `client_workspace_id`, `product_id`, `campaign_id`, `lead_id`, estado de consentimento, canal e permission envelope, mais referências estritamente necessárias à tarefa; resolve conteúdo autorizado sob demanda. Ele propõe qualificação e evidências, não altera CRM diretamente nem envia mensagem. O OS decide autorização, versiona o resultado e comanda o Handoff. Regras de minimização de contexto e execução estão no [Harness Context Contract](../harness/contracts/AGENT_CONTEXT_CONTRACT.md).

## UI e gates

A futura área de Engagement pode mostrar Lead e timeline de conversas apenas a papéis autorizados, com fonte, consentimento, sinais, decisão de qualificação e estado do handoff. O Client Portal mostra somente o recorte permitido por policy. Antes de habilitar a capacidade, fechar identidade/deduplicação, finalidade, base de consentimento por canal, retenção/deleção, critérios de qualificação, revisão, contrato de feedback CRM, isolamento multi-tenant, conectores e tratamento de falhas. WhatsApp, CRM e Lead Qualification permanecem roadmap; nenhuma dessas capacidades está `READY`.
