# Git Strategy

`main` protegida por repositório. Feature inicia em SPEC aprovada e branch com ID comum, por exemplo `feature/MMOS-A01-agency-tenant`, seguida de PR, CI, revisão de segurança/comportamento quando aplicável e aprovação humana antes de merge. Alteração cross-repo usa mesmo ID em PRs vinculadas; contrato do OS é publicado antes do client Eve, com janela de compatibilidade. ADR estrutural acompanha PR de SPEC.

Não commitar credenciais, `.env*`, `node_modules`, `.eve`, `.vercel`, `.output` ou dados reais. PR descreve problema, mudança, migração, testes, riscos, rollback e impacto no contrato. Merge/deploy não são atos automáticos do agente de desenvolvimento. Esta tarefa não cria branch, commit, push, PR ou deploy.
