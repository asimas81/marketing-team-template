# CLIENT_PORTAL_MODEL

## Surface do Control Plane

Client Portal é uma interface do mesmo Marketing OS, usando Supabase Auth, API, entidades, AuditEvents e RLS compartilhados. Não duplica banco nem sincroniza uma segunda verdade. Cada sessão de usuário cliente está fixada a Clients para os quais existe ClientWorkspaceMembership ativa. Não há dashboard multi-cliente para papéis de cliente.

`Client Admin` vê a operação do próprio Client conforme ClientPolicy; a administração de membros não integra a superfície inicial do portal. `Client Approver` decide os tipos de aprovação designados; `Client Reviewer` comenta e pede mudanças; `Client Viewer` lê conteúdo permitido. Papéis podem ser combinados apenas por grants explícitos. A agência define quais campanhas, criativos, relatórios e métricas são compartilháveis; `internal_only` nunca aparece no portal. URLs assinadas de assets têm escopo e duração limitados.

Fluxo: convite → identidade → membership → seleção de Client → overview → revisão/comentário/aprovação → histórico. A aprovação no portal usa o mesmo `ApprovalRequest` versionado, registra ator autenticado e retorna ao mesmo estado do OS. A remoção do usuário invalida acesso e sessões futuras; links compartilhados não permitem bypass. O Client recebe informação do que foi solicitado, por quem, prazo, efeito de execução e consequência de rejeição.

Client Portal is part of the MVP. Seu escopo inicial inclui `Overview`, `Campaigns`, `Creatives`, `Approvals`, `Performance`, `Reports` e `Requests`, com visualização, comentários, solicitações e decisões limitadas por papel e ClientPolicy. No MVP, o portal não expõe configuração interna de agentes, custos internos da agência, cross-client analytics, configurações técnicas internas, administração avançada de integrações ou informações de outros clientes. Operações de integração e budget permanecem na interface interna e exigem grants específicos. Ver [TENANT_RBAC_MATRIX](./TENANT_RBAC_MATRIX.md) e [APPROVAL_MODEL](./APPROVAL_MODEL.md).
