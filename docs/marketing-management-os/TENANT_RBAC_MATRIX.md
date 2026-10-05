# TENANT_RBAC_MATRIX

## Resolução de autorização

Autorização = principal autenticado + AgencyMembership ativa + ClientWorkspaceMembership ou grant administrativo explícito + recurso no escopo + ação + policy efetiva. O servidor decide; RLS reforça. `Agency Owner/Admin` podem administrar Clients da própria Agency conforme política, com acesso auditado. `Account Director` vê apenas carteira atribuída; `Account Manager` opera apenas Clients atribuídos. Papéis profissionais não concedem automaticamente permissão sobre todo Client. Um `Client Approver` precisa ainda de escopo de decisão e nunca aprova fora do próprio Client.

Legenda: A = permitido por papel, S = somente Client explicitamente atribuído, P = conforme policy/escopo da aprovação, — = negado. Todas as permissões pressupõem Agency correta; operações externas exigem aprovação adicional.

| Ação | Owner/Admin agência | Director/Manager | Strategist/Creative/Media/Analyst | Client Admin | Client Approver | Client Reviewer | Client Viewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Criar/arquivar Client e definir AgencyPolicy | A | — | — | — | — | — | — |
| Atribuir equipe da agência ao Client | A | S conforme delegação | — | — | — | — | — |
| Convidar/remover membros do próprio Client | A | S conforme delegação | — | P | — | — | — |
| Ver Client Dashboard, Campaigns e Reports | A | S | S | A | A | A | A |
| Criar Request/brief/draft | A | S | S conforme função | P | P | — | — |
| Editar Product Context/Domain binding | A | S | S para Strategist | P | — | — | — |
| Publicar Product Context/ClientPolicy | P | P | — | P | — | — | — |
| Comentar/revisar entrega | A | S | S | A | A | A | — |
| Aprovar editorial/estratégia | P | P | P se designado | P | P | — | — |
| Autorizar publish/send/spend/budget | P | P | P se designado | P | P se designado | — | — |
| Conectar/revogar conta externa | A | S com grant | — | P | — | — | — |
| Ver consolidação da Agency | A | S apenas carteira | — | — | — | — | — |

Para todas as ações, `P` exige `ApprovalPolicy` ativa, papel designado, objeto e versão exatos, separação de funções se configurada e Client owner correspondente. `S` não pode ser inferido da AgencyMembership apenas. Analyst recebe leitura de métricas do Client atribuído, Media Buyer prepara planos e ações dentro do Client atribuído; nenhum papel profissional autoriza gasto direto. Service accounts só operam por endpoint com escopo delegável e trilha de auditoria.

Testes obrigatórios: usuário em duas Agencies com papéis distintos, agência administradora versus cliente vizinho, manager sem atribuição, Client Viewer tentando mutação, Client Approver tentando aprovar outro Client, remoção de membership durante AgentRun, recurso com `agency_id` correto e `client_workspace_id` errado, bypass por Data API e execução por service role.
