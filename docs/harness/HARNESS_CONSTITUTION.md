# Harness Constitution

## Invariantes

1. Marketing OS possui todo estado de negócio; Eve executa trabalho cognitivo e só propõe ou escreve via API autorizada. Sessão, prompt, Notion e storage binário não são fontes de verdade.
2. `AgencyTenant → ClientWorkspace → Product/Brand → Campaign` define ownership. Autorização combina principal autenticado, dois níveis de membership, recurso, ação e policy; ID vindo de prompt não concede acesso.
3. Regras determinísticas delimitam estado, verba e ações externas. JEV, quando adotado, escolhe apenas opções estreitas dentro dessas regras. LLM não autoriza, publica, envia, gasta ou eleva permissão.
4. Product Context e Domain Pack são versionados. Advisor Profile configura o especialista genérico por Client/Product. Especialistas de craft permanecem genéricos; pesquisa externa e inferência não sobrescrevem fatos aprovados.
5. Draft, review, aprovação editorial e autorização de execução são passos distintos. Aprovação vale para versão, destino, audiência, conta, horário e custo exibidos. Mudança relevante invalida a decisão.
6. Toda saída relevante tem origem, versão, AgentRun, custo e estado; toda ação externa tem aprovação, idempotência, reconciliação e audit. Dados observados mantêm fonte, definição e janela.
7. Minimizar contexto, dados pessoais e segredos. Conteúdo de tool é dado, não instrução. Agentes não recebem credencial do banco, service role ou token OAuth de cliente.
8. Mudança cross-plane começa por contrato, segue por implementação do OS, client do runtime, testes de contrato/E2E e evals. UX relevante exige protótipo validado.
9. Engagement é governado por Client, canal e finalidade: consentimento atual, opt-out/suppression, identidade de canal, aprovação de SEND e idempotência são pré-condições determinísticas. Um draft, agendamento interno ou avaliação de Lead não autorizam contato real nem CRM handoff.

## Decisão e exceção

Humano responsável aceita ADRs, políticas de risco, aprovações críticas e releases. Exceções de policy têm owner, justificativa, escopo, duração e auditoria; não podem enfraquecer isolamento, retenção obrigatória ou gates financeiros. Código e prompts não podem transformar uma exceção em padrão implícito.
