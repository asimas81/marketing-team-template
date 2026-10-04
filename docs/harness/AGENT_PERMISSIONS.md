# Agent Permissions

Permission envelope é emitido pelo OS por Run, com Agency, Client, Product/Campaign, recursos, ações, side effects e expiração. O agente não altera envelope e tools verificam novamente no OS. `read`, `draft`, `recommend` e `prepare` são permitidos conforme policy; `publish`, `send`, `spend`, `delete` e produção deploy exigem aprovação de negócio e enforcement da operação. Nenhum agente acessa Supabase, token OAuth ou service role diretamente.

Domain Specialist pode criar advisory/proposta, sem aprovar campanha; Creative Producer pode criar artifact/variant, sem publicar; Audience futura cria hipótese evidenciada, sem targeting sensível ou execução; Paid Media futura propõe plano, sem gasto; Performance futura recomenda, sem budget mutation. Email mantém gates Eve existentes para sends. [Matriz](./permissions/PERMISSIONS_MATRIX.md) detalha por agente. Falta de grant resulta em negação auditada sem revelar recurso de outro Client.
