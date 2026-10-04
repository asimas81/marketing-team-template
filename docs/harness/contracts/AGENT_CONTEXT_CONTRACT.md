# Agent Context Contract v2

## Envelope mínimo

`contract_version`, `agency_id`, `client_workspace_id`, `agent_run_id`, `task_type`, `requested_by`, `product_id?`, `campaign_id?`, `artifact_id?`, `permission_envelope`, `trace_id`, `cost_limit`. `workspace_id` dos contratos legados equivale a `client_workspace_id`. IDs são referências verificadas pela API. O OS fixa `client_policy_version`, `product_context_version`, `domain_pack_version?`, `advisor_profile_version?`, `campaign_brief_version?` e versões de artifacts de entrada antes da delegação.

## Carregamento

Ordem: autorização → policy efetiva → objetivo/tarefa → Product Context → Campaign/Brief → Domain Pack/Advisor quando necessário → artifacts relevantes → métricas observadas quando necessárias → instrução do usuário. Cada item traz ID, versão, estado, fonte e timestamp. Preferir resumo curto com referências recuperáveis; limites de bytes/tokens por tipo serão definidos em SPEC a partir de medições. Conteúdo sensível é redigido; dados pessoais brutos entram apenas com finalidade e grant. Pesquisa pública e material importado permanecem dados de menor confiança.

Se membership expirar, recurso sair do Client, versão publicada for revogada ou fonte obrigatória faltar, o gateway falha fechado ou devolve `NEEDS_REVIEW` conforme policy. Contexto stale não é atualizado silenciosamente durante Run; nova versão exige nova execução ou revisão. Cada tool revalida escopo. Não carregar dados de outros Clients no prompt; analytics de agência fornece apenas agregado autorizado em fluxo separado. Formato serializado, limites numéricos e autenticação delegada são decisões de SPEC.
