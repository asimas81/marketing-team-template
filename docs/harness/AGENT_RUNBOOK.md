# Agent Runbook

Para Run falho, usar `agent_run_id`/`trace_id` e Client autorizado; consultar versão de contexto, status, tool calls, custo e erro. Se falta contexto, abrir review em vez de fabricar informação. Se membership/policy falhar, encerrar com erro de autorização, sem revelar recurso oculto. Se provider/modelo falhar, limitar retry e preservar input versionado; retomar apenas operação idempotente. Se Artifact não persistiu, não exibir link/ID fictício.

Send/publicação/gasto com resposta incerta exige consulta ao OS/conector e reconciliação antes de nova tentativa. Prompt injection detectada gera risk flag e revisão da fonte; não elevar permissão. Em incidente cross-client, pausar tools afetadas e seguir [runbook de segurança](./runbooks/RUNBOOK.md). Registrar causa, decisão humana, correção e eval de regressão. Este runbook não habilita tool nem operação externa.

Em Email/Engagement futuro, uma tentativa de envio sem consentimento, com opt-out, suppression, identidade de canal ambígua ou approval vencido termina bloqueada e auditada. O agente não tenta contornar por outro canal. Timeout depois de SEND requer reconciliação do message ID pelo OS; não reinvocar a tool por conta própria. Lead Qualification com contexto insuficiente retorna `NEEDS_REVIEW` e não sincroniza CRM. Esses fluxos não alteram os gates do especialista `email` atual nesta execução.
