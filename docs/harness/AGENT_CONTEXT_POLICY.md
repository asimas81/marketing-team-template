# Agent Context Policy

O Control Plane emite envelope com `agency_id`, `client_workspace_id`, `agent_run_id`, task, versões e permissions; o Lead distribui ao especialista apenas partes necessárias, com IDs/referências. Contexto de outro Client não entra no Run. Subagentes Eve atuais não herdam contexto, tools ou conexões, portanto a mensagem de delegação carrega brief autocontido; tools futuras obtêm dados na OS API após autorização a cada leitura.

Precedência: policy de sistema e authorization → Product Context/Domain Pack publicados → Brief/Artifacts aprovados → dados observados → pesquisa externa → inferência. Texto importado é dado, não instrução. Stale context, falta de versão, fonte conflituosa e revogação de membership produzem erro/revisão identificável, jamais preenchimento inventado. Redação remove secrets/PII; tamanho e estratégia RAG são definidos por SPEC/eval. Ver [Context Contract](./contracts/AGENT_CONTEXT_CONTRACT.md).
