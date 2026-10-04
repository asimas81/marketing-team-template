# Marketing Management OS Harness

Este diretório materializa o [Harness Engineering v1.2](../marketing-management-os/HARNESS_ENGINEERING_MARKETING_MANAGEMENT_OS.md) como contratos e políticas documentais. O nome `HARNESS_ENGINEERING.md` citado na solicitação não existe; o arquivo com sufixo é a referência presente no repositório. Nenhuma feature, integração ou migration foi implementada.

Os artefatos da raiz e subdiretórios descrevem o futuro repositório `marketing-management-os` (Control Plane); os documentos `AGENT_*`, `TOOL_POLICY`, `EVALS_POLICY`, `PROMPT_INJECTION_POLICY` e `APPROVAL_ENFORCEMENT_POLICY` pertencem logicamente ao futuro `marketing-agents`. Ambos ficam aqui como staging porque este é o repositório atual do template Eve. Os contratos canônicos deverão pertencer ao Control Plane e ser consumidos pelo runtime em versão publicada. Esta separação não cria repositórios nem altera o código existente.

Comece por [Constitution](./HARNESS_CONSTITUTION.md), [System Architecture](./architecture/SYSTEM_ARCHITECTURE.md), [Open Decisions](./OPEN_DECISIONS.md), [Implementation Sequence](./IMPLEMENTATION_SEQUENCE.md) e [Harness Readiness](./HARNESS_READINESS_REPORT.md). O [Spec Readiness Map](./SPEC_READINESS_MAP.md) organiza a decomposição sem tratar documentação como capacidade operacional.
