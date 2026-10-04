# CLIENT_PORTAL_MODEL

## Surface do Control Plane

Client Portal é uma interface do mesmo Marketing OS, usando Supabase Auth, API, entidades, AuditEvents e RLS compartilhados. Não duplica banco nem sincroniza uma segunda verdade. Cada sessão de usuário cliente está fixada a Clients para os quais existe ClientWorkspaceMembership ativa. Não há dashboard multi-cliente para papéis de cliente.

`Client Admin` administra membros do próprio Client e vê operação conforme ClientPolicy; `Client Approver` decide os tipos de aprovação designados; `Client Reviewer` comenta e pede mudanças; `Client Viewer` lê conteúdo permitido. Papéis podem ser combinados apenas por grants explícitos. A agência define quais campanhas, criativos, relatórios e métricas são compartilháveis; `internal_only` nunca aparece no portal. URLs assinadas de assets têm escopo e duração limitados.

Fluxo: convite → identidade → membership → seleção de Client → overview → revisão/comentário/aprovação → histórico. A aprovação no portal usa o mesmo `ApprovalRequest` versionado, registra ator autenticado e retorna ao mesmo estado do OS. A remoção do usuário invalida acesso e sessões futuras; links compartilhados não permitem bypass. O Client recebe informação do que foi solicitado, por quem, prazo, efeito de execução e consequência de rejeição.

Escopo MVP do portal (habilitação ainda aberta): visão de campanhas/entregas, comentários, approvals, resultados e relatórios. Administração de integrações e budget requer grants específicos. Ver [TENANT_RBAC_MATRIX](./TENANT_RBAC_MATRIX.md) e [APPROVAL_MODEL](./APPROVAL_MODEL.md).
