# Approval Enforcement Policy

Marketing OS persiste ApprovalRequest/Decision de negócio com Agency/Client, target/version/hash, destino, conta, audiência, horário, budget/custo, policy, ator e prazo. Eve approval é gate operacional adicional na tool; sozinho não constitui autorização de negócio. Advisory aprovado e peça aprovada editorialmente não liberam envio/publicação/gasto. O executor revalida snapshot e membership imediatamente antes do side effect.

Mudança de payload, conta, público, horário, valor, versão ou policy invalida autorização. Em modo inicial, send/publish/spend/delete, budget change e ações de mídia que alteram estado externo exigem aprovação humana. Draft/recommend podem ser automáticos quando policy permite. Resposta incerta do provider entra `RECONCILIATION_REQUIRED`, sem retry cego. Evals/testes cobrem autoaprovação indevida, aprovação por outro Client e replay de hash antigo.
