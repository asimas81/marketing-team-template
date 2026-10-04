# Marketing OS ↔ Agent Runtime API

## Contrato lógico

`RunAgentTask` recebe o envelope do [Context Contract](./AGENT_CONTEXT_CONTRACT.md), idempotency key e capability solicitada. O OS persiste AgentRun `QUEUED`, invoca Eve e registra `RUNNING`, eventos, custo e resultado terminal `SUCCEEDED`, `FAILED` ou `NEEDS_REVIEW`. `AgentTaskResult` inclui `agent_run_id`, `status`, `summary`, IDs/version/hash de artifacts, `advisory_id?`, `risk_flags`, `approval_required`, versões usadas e `trace_id`. Erros distinguem `UNAUTHORIZED`, `NOT_FOUND_OR_HIDDEN`, `CONTEXT_STALE`, `POLICY_BLOCKED`, `EXTERNAL_UNCERTAIN` e falha transitória, sem revelar existência de recurso de outro Client.

Tools de leitura (`get_product_context`, `get_domain_pack`, `get_campaign`, `get_artifact`, `get_campaign_metrics`) e de escrita limitada (`create_artifact`, `create_domain_advisory`, `create_creative_artifact`, `submit_for_review`, `raise_risk_flag`, `update_agent_run_event`) passam pela API. O serviço verifica principal delegado, Run, Agency, Client, recurso, ação, versão e limite de custo em cada chamada. Nenhuma tool recebe service role ou token OAuth. Ações externas usam endpoint separado que exige ApprovalRequest válido, payload hash, ExternalAccount do mesmo Client e idempotency key.

O owner canônico do contrato será o Control Plane, publicado para Eve como OpenAPI/JSON Schema ou pacote versionado a decidir. Mudança breaking exige versão, janela de compatibilidade, client gerado e contract tests em ambos os lados. Transporte Eve, assinatura do envelope e propagação de identidade são `TO_VALIDATE`, não APIs afirmadas como existentes.
