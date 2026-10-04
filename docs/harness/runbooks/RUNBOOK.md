# Operations Runbook

## Triagem comum

Identificar ambiente, Agency/Client, `trace_id`, `agent_run_id`, ação e versão sem copiar segredo/PII. Consultar AuditEvent, aprovação, estado do Run e health do conector. Classificar: auth/RLS, contexto stale, Eve/AI Gateway, banco, geração, publicação/envio/gasto incerto, import métrica ou custo. Definir owner, impacto, contenção, recuperação e comunicação ao usuário.

## Casos prioritários

| Incidente | Contenção e recuperação |
| --- | --- |
| Suspeita de cross-tenant leak | Desabilitar endpoint/tool/integração afetada, preservar audit/trace protegidos, revogar grants, escalar segurança; release bloqueado até correção e teste de regressão |
| Supabase/API indisponível | Pausar novas mutações e runs; não usar sessão Eve como SoR; restaurar serviço e reconciliar jobs pendentes |
| Eve/model timeout | Manter AgentRun em estado rastreável, limitar retry, preservar versões de input e custo; retomar ou falhar explicitamente |
| Send/publish/spend com resposta incerta | Bloquear retry cego; consultar provider por external ID/idempotency key, reconciliar e registrar resultado antes de nova tentativa |
| Conector expirado/reauth | Marcar health, impedir execução, alertar owner Client, reautorizar com escopos verificados e auditar |
| Custo anômalo | Pausar geração/runs conforme cap, investigar modelo/provider e corrigir policy; não ampliar budget via agente |
| Offboarding | Suspender runs/ações, revogar conexões, exportar, remover acesso e validar retenção conforme [modelo](../../marketing-management-os/CLIENT_OFFBOARDING_MODEL.md) |

Backup/restore e RTO/RPO concretos dependem de ambiente/SPEC. Depois de incidente, registrar causa, impacto, correção, eval/test novo e decisão de reabilitação humana. Este runbook é alvo documental, não automação configurada.
