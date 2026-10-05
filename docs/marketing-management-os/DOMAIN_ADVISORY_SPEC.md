# DOMAIN_ADVISORY_SPEC

## Papel e acionamento

`product-domain-specialist` é um subagente Eve consultivo. O lead o aciona para estratégia/brief de Campaign, revisão de claim, interpretação de métrica com nuance vertical, conflito de fontes, incerteza material sobre Product ou política de Workspace/Domain Pack que exige revisão. Para Product genérico com contexto suficiente e sem regra relevante, o lead pode seguir diretamente ao especialista de craft. O OS decide quando uma revisão é obrigatória; o agente cumpre a policy recebida.

## Entrada mínima

`agent_run_id`, `workspace_id`, `product_id`, tarefa e principal solicitante. `campaign_id` e `artifact_id` são opcionais. O Context Gateway entrega apenas os trechos necessários de Workspace Policy, Product Context publicado, Domain Pack ativo, Campaign, artefatos aprovados e métricas observadas. Cada trecho traz ID, versão, estado e fonte. IDs no prompt não autorizam leitura; a API resolve membership e escopo antes de entregar dados.

## Hierarquia e classificação

Prioridade: Workspace Policy → Product Context aprovado → Domain Pack aprovado → estratégia de Campaign aprovada → brand guidance → artefatos de Product aprovados → contexto corrente da Campaign → métricas observadas → pesquisa pública → inferência. A política de autorização do sistema prevalece sobre todos. O parecer classifica afirmações como `APPROVED_FACT`, `DOMAIN_RULE`, `OBSERVED_DATA`, `EXTERNAL_EVIDENCE`, `ASSUMPTION`, `INFERENCE` ou `OPEN_QUESTION`. Pesquisa externa pode revelar conflito, nunca promover um fato sem aprovação.

## Handoff obrigatório

| Campo | Conteúdo |
| --- | --- |
| Identidade | ID do advisory, Workspace/Product/Campaign, tarefa, run e versões de Product Context/Domain Pack |
| Status | `APPROVED`, `APPROVED_WITH_CONSTRAINTS`, `NEEDS_REVIEW` ou `BLOCKED` |
| Resumo | Conclusão curta com escopo e principais ressalvas |
| Verdade e guidance | Fatos do produto, recomendações de domínio e vocabulário preferido/a evitar |
| Restrições e claims | Itens obrigatórios/proibidos; claims aprovados, dependentes de evidência ou proibidos |
| Riscos | Tipo, gravidade, descrição, evidência e ação sugerida |
| Incerteza | Premissas, questões abertas e conflito a resolver |
| Evidência | Refs de contexto, pack, Campaign e fontes externas com data |
| Próximo especialista | `downstream_brief.must_include` e `must_avoid` prontos para delegação |

`APPROVED` significa que a revisão de domínio passou; não autoriza campanha, peça ou envio. `APPROVED_WITH_CONSTRAINTS` permite continuar apenas com as condições explícitas. `NEEDS_REVIEW` pede decisão ou fonte ausente. `BLOCKED` exige restrição aprovada e impacto material citados. O OS cria Review Task humana para os dois últimos estados quando a política determinar.

## Propostas e permissões

Correção de Product Context ou Domain Pack é proposta com campo, valor atual, valor proposto, motivo, evidência, impacto e necessidade de aprovação. O owner humano da entidade decide a versão nova. Permissões do especialista: leitura autorizada, pesquisa pública, criação de advisory, comentário, risk flag e proposta. O catálogo de ferramentas não deve expor publish, send, spend, delete, mudança de orçamento, billing, secrets ou permissões. Toda escrita passa pela API do OS, com auditoria, sem banco direto.

## Avaliação mínima

Casos: SaaS genérico sem pack não inventa regra vertical; produto financeiro usa pack obrigatório e pede evidência para claim; Product Context insuficiente resulta em `NEEDS_REVIEW`; Campaign que contradiz contexto aprovado resulta em revisão/bloqueio justificado; pesquisa pública conflitante é registrada sem sobrescrever contexto. Regressões medem fidelidade ao Product, domínio, claims, classificação epistemológica, isolamento, prompt injection, qualidade do handoff e falsos bloqueios. O [plano de evals](./EVAL_PLAN.md) define gates comuns.

## Advisor por Client v2

O `workspace_id` legado torna-se `client_workspace_id`, acompanhado de `agency_id`. O OS resolve Advisor Profile efetivo por Client/Product e fornece suas versões de Domain Pack, fontes e policies; o subagente continua o mesmo entre clientes. O parecer e as propostas carregam os dois IDs de tenancy e não podem citar fonte privada de outro Client. Se o perfil for obrigatório e estiver ausente, desatualizado ou sem fonte suficiente, o estado é `NEEDS_REVIEW` e o fluxo dependente aguarda owner humano. Remote Advisor futuro usa o mesmo contrato e limites.
