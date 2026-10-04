# Worktree Policy

Worktree é opcional para isolar SPECs paralelas ou revisar alteração cross-repo. Cada worktree tem branch, owner e feature ID; comandos rodam na raiz correta. Não compartilhar `.env.local` ou links `.vercel` entre worktrees sem configuração segura específica. Gerados e dependências permanecem fora do Git. Antes de remover worktree, conferir diffs, arquivos não rastreados e aprovações; nunca usar limpeza destrutiva automática sobre trabalho de outro agente.

Para features em dois repositórios, manter um worktree por repo com mesmo feature ID e matrizes de compatibilidade. Atualizar contrato/consumer sequencialmente; PRs separados permitem revisar blast radius. Esta política não solicita nem autoriza worktree nesta execução documental.
