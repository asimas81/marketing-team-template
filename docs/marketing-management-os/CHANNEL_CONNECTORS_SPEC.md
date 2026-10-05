# CHANNEL_CONNECTORS_SPEC

## Contrato de adapter

Conectores Meta Ads, Google Ads e TikTok Ads partilham envelope interno: `agency_id`, `client_workspace_id`, `client_integration_id`, `external_account_id`, `action`, `capability_version`, `requested_by`, `approval_id`, `payload_hash`, `idempotency_key`, `trace_id`. A API valida todos antes de fornecer uma referência de credencial ao executor server-side. O adapter declara por conta as capacidades reais de leitura, draft/criação, upload criativo, targeting, experimento nativo, métricas, budget e pause/resume, com permissão, limite, versão e status. Não há suposição de paridade entre plataformas.

Operações são `discover_accounts`, `get_capabilities`, `read_state`, `prepare_action`, `execute_authorized_action`, `read_action_status`, `import_metrics` e `revoke/reauth` conforme provider. `prepare_action` retorna diff, custo/impacto, pré-condições e hash canônico; `execute` exige aprovação válida daquele hash e conta. Resposta registra ID externo, timestamps, status e payload reduzido. Webhooks e polling convergem para reconciliação idempotente. Rate limit e falhas transitórias têm backoff; efeitos externos incertos ficam `RECONCILIATION_REQUIRED`.

OAuth e tokens são client-scoped, criptografados e server-side. O conector não contém estratégia nem decide budget. Toda execução tem AuditEvent e span OTel com IDs de correlação, sem segredo. Evals/contract tests devem verificar conta errada, scope revogado, capability ausente, aprovação vencida, retry e webhook de outro Client. APIs e permissões concretas por provider ficam `TO_VALIDATE` na respectiva SPEC, antes de afirmar suporte.
