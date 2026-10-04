# Environment Matrix

| Dimensão | Development | Preview/Staging | Production |
| --- | --- | --- | --- |
| Vercel OS / Eve | Projetos ou ambientes de desenvolvimento | Projetos isolados de produção | Projetos de produção separados por plano conforme topologia alvo |
| Supabase Auth/Postgres | Projeto e dados sintéticos | Projeto/branch seguro com dados sintéticos | Projeto de produção com backup e acesso controlado |
| AI Gateway/Eve endpoint | Model policy e custo de dev | Capability de teste e evals | Model policy aprovada e observada |
| Integrações e email | Mock/sandbox; sends reais bloqueados | Test accounts; sends reais bloqueados | Contas Client autorizadas, approval e idempotência |
| Publishing/spend/delete | Bloqueado ou fake executor | Bloqueado por padrão; teste controlado isolado | Policy + aprovação + auditoria + reconciliação |
| Secrets | Secret manager/env de dev | Segredos próprios; nunca produção | Vault/env de produção com menor privilégio |
| OTel | Collector local/teste; sem PII | Pipeline de validação/redação | Export protegido, retenção e alertas |

Vínculo concreto de projetos, Supabase branching, vault, cost limits, domínios OAuth, feature gates e política de dados sintéticos são `TO_VALIDATE` em SPEC. Não copiar dados de produção para preview sem processo de anonimização aprovado. A matriz é alvo, sem recursos provisionados nesta execução.
