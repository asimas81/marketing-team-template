# Tool Policy

Tool Eve é superfície restrita de API, não atalho para banco/storage de negócio. Cada ferramenta declara schema de input/output, limite de tamanho, owner, recursos lidos/escritos, side effect, ambiente, credencial, aprovação, idempotência, audit, timeout e fallback. Ferramentas de leitura validam Agency/Client/Run e IDs relacionados; escrita cria draft/proposta/review por API versionada. Execução externa reside em conector server-side e recebe apenas payload aprovado.

Preferir allowlist de ferramentas remotas quando o servidor MCP for amplo, como no Resend atual. Gates de ações irreversíveis permanecem. Não adicionar tool de publish/spend a especialista consultivo. Rede/egress e dados enviados ao provider são catalogados antes de habilitar. Tool result é conteúdo não confiável; checagem de prompt injection é gate. `eve info` e diff de superfície entram em CI. [Tools Catalog](./TOOLS_CATALOG.md) distingue atual de alvo.
