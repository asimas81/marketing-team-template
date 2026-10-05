# Approval Enforcement Policy

Marketing OS persiste ApprovalRequest/Decision de negócio com Agency/Client, target/version/hash, destino, conta, audiência, horário, budget/custo, policy, ator e prazo. Eve approval é gate operacional adicional na tool; sozinho não constitui autorização de negócio. Advisory aprovado e peça aprovada editorialmente não liberam envio/publicação/gasto. O executor revalida snapshot e membership imediatamente antes do side effect.

Mudança de payload, conta, público, horário, valor, versão ou policy invalida autorização. Em modo inicial, send/publish/spend/delete, budget change e ações de mídia que alteram estado externo exigem aprovação humana. Draft/recommend podem ser automáticos quando policy permite. Resposta incerta do provider entra `RECONCILIATION_REQUIRED`, sem retry cego. Evals/testes cobrem autoaprovação indevida, aprovação por outro Client e replay de hash antigo.

## Engagement: fases distintas

`DRAFT` grava conteúdo interno. `PREPARE` materializa versão, destinatários/segmento, canal, conta, identidade, consentimento, suppression, volume, custo e horário, sem enviar. `SCHEDULE` registra intenção no OS; se agendar no provider já compromete a entrega futura, aplica o gate de `SEND`. `SEND` é a ação externa real e exige policy de Client, aprovação humana inicial sobre snapshot exato, consentimento atual, opt-out/suppression, rate limit, account health e idempotency key. `PUBLISH` é publicação em surface pública e mantém decisão própria. Aprovação editorial do draft não autoriza SEND ou PUBLISH.

Antes da execução agendada, revalidar consentimento e suppression no momento do disparo, além de membership/policy, conta e payload. Revogação de consentimento, alteração de segmento, template, lista, mensagem, horário, conta ou policy invalida autorização. Cada destinatário tem chave de deduplicação e resultado auditável. Provider timeout entra em reconciliação por message ID/idempotency key. `Lead Qualification` e `CRM Handoff` futuros geram recomendação e pedido de ação próprios; não herdam aprovação de campanha ou de envio. Ver [contrato de Engagement](./contracts/ENGAGEMENT_CHANNEL_CONTRACT.md).
