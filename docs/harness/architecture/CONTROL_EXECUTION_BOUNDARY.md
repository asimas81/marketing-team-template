# Control/Execution Boundary

| Responsabilidade | Marketing OS | Eve |
| --- | --- | --- |
| Identidade, RBAC, ClientPolicy, RLS | Decide e persiste | Recebe envelope reduzido |
| Contexto aprovado e versões | Publica, resolve e audita | Lê snapshot autorizado |
| Request, Campaign, Artifact, Approval, AgentRun, Metric, Budget | Fonte de verdade | Propõe ou envia output por API |
| Roteamento cognitivo e criação | Registra tarefa/resultado | Lead e especialistas executam |
| Ação externa | Valida policy, snapshot, conta, idempotência; executor server-side | Prepara pedido; gate Eve adicional quando aplicável |

`RunAgentTask` só é emitido depois de AgentRun `QUEUED` persistido e autorização de principal, Agency, Client e recurso. O Context Gateway fixa versões e redige dados antes de fornecer contexto. Eve não consulta Supabase diretamente; tools chamam API/SDK versionada. Uma resposta textual não prova persistência. `AgentTaskResult` referencia Artifact/Advisory versionados persistidos ou informa que a saída segue apenas em conversa.

O OS valida novamente cada tool call. Um permission envelope não é token de superusuário; expira, vincula Run/Client e não permite elevar escopo. Falha ou timeout deixa estado reconciliável, com retry idempotente. Contratos cross-repo têm owner no OS e janela de compatibilidade. Ver [Marketing OS Agent API](../contracts/MARKETING_OS_AGENT_API.md).
