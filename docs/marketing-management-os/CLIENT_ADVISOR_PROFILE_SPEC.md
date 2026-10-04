# CLIENT_ADVISOR_PROFILE_SPEC

## Propósito e escopo

`AdvisorProfile` configura o consultor genérico `product-domain-specialist` por Client Workspace, com override opcional por Product. O perfil de Product herda restrições do perfil do Client e só pode torná-las mais estritas. O perfil não contém verdade de produto nem conhecimento vertical copiado: referencia versões publicadas de Product Context, Domain Pack, fontes autorizadas e ClientPolicy. `agent_binding=local_eve` é o padrão; `remote_eve` é extensão futura sujeita a contrato, isolamento e avaliação equivalentes.

Envelope conceitual: `id`, `agency_id`, `client_workspace_id`, `product_id?`, `version`, `status`, `name`, `domain_pack_refs`, `knowledge_source_refs`, `required_review_types`, `claims_policy_ref`, `risk_policy_ref`, `model_policy_ref`, `agent_binding`, `owner`, `approved_by`, `effective_at`. Versões ativas são imutáveis e AgentRun fixa `advisor_profile_id/version` e todas as referências resolvidas.

## Resolução e execução

O Context Gateway resolve o perfil efetivo após autorização de Client e Product. Se não houver perfil, usa Product Context e policy; a revisão de domínio é opcional salvo exigência de ClientPolicy/Domain Pack/risco. O Lead pede parecer para estratégia, brief, claims ou leitura de performance quando aplicável. O especialista devolve advisory com fatos, restrições, riscos, evidência e estado `APPROVED`, `APPROVED_WITH_CONSTRAINTS`, `NEEDS_REVIEW` ou `BLOCKED`. Estes estados não aprovam campanha nem publicação. Propostas de mudança de Pack exigem owner humano e nova versão.

Perfil ou fonte desatualizada bloqueia apenas os fluxos cujo policy exige revisão; o sistema exibe a pendência e o owner. Evals devem provar que dois Clients com perfis diferentes não compartilham fontes, que Product override não enfraquece policy e que desativar um pack devolve comportamento genérico. Remote Agent futuro recebe envelope minimizado e identidade delegada, nunca credencial ou acesso direto ao banco.
