# Agent Runbook

Para Run falho, usar `agent_run_id`/`trace_id` e Client autorizado; consultar versão de contexto, status, tool calls, custo e erro. Se falta contexto, abrir review em vez de fabricar informação. Se membership/policy falhar, encerrar com erro de autorização, sem revelar recurso oculto. Se provider/modelo falhar, limitar retry e preservar input versionado; retomar apenas operação idempotente. Se Artifact não persistiu, não exibir link/ID fictício.

Send/publicação/gasto com resposta incerta exige consulta ao OS/conector e reconciliação antes de nova tentativa. Prompt injection detectada gera risk flag e revisão da fonte; não elevar permissão. Em incidente cross-client, pausar tools afetadas e seguir [runbook de segurança](./runbooks/RUNBOOK.md). Registrar causa, decisão humana, correção e eval de regressão. Este runbook não habilita tool nem operação externa.
