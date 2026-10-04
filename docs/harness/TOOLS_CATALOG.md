# Tools Catalog

Cada tool/connector implementado deverá declarar owner, plano, propósito, leitura/escrita, side effect, aprovação, credencial, ambiente, retry/fallback e audit. O catálogo abaixo distingue estado existente de ferramentas alvo, sem afirmar que alvos estão conectados.

| Grupo | Estado | Owner/plano | Side effect e gate |
| --- | --- | --- | --- |
| `get_brand_context`, `save_brand_context`, preferências e artifact Blob | Existente no template | Eve/runtime | Escrita interna legada; contexto global deve migrar por Client |
| Asset tools Blob | Existente no template | Eve/runtime | Upload/delete; delete gated, ownership OS ainda ausente |
| Notion MCP | Existente | Eve/integração opcional futura | Escrita remota com gates existentes; import/export client-scoped a especificar |
| Resend MCP | Existente | Eve/email | Send/delete gated no Eve; OS business approval futura |
| OS context/read tools | Alvo | OS API → Eve | Read autorizado por Agency/Client/Run; sem token de banco no agente |
| OS draft/advisory/artifact/review tools | Alvo | OS API → Eve | Escrita interna versionada, idempotente e auditada |
| Media channel connectors | Alvo | Executor OS | Publish/spend/budget com approval, account mapping e reconciliação |
| Creative provider adapters | Alvo | OS/runtime conforme SPEC | Custo e binário por Client; geração respeita cap e direitos |
| Engagement read/prepare tools | Futuro | OS API → Eve | Lead/consent/thread minimizados; draft e preparo sem SEND |
| Engagement send/receive adapter | Futuro | Executor OS | ClientIdentity, suppression, approval, rate limit, idempotência, webhook autenticado |
| Lead qualification e CRM handoff | Futuro | Eve proposta → OS executor | Assessment evidenciado; sync externo separado e autorizado |

Inventário exato da superfície atual deve ser extraído de `eve info` na SPEC de integração, com diff em CI. Nomes finais de tools OS, credenciais e política de egress dependem do contrato versionado. Nenhum tool novo foi criado nesta execução.
