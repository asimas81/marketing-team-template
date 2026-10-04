# Open Decisions

Decisões abaixo precisam de owner e ADR/SPEC antes da implementação afetada. `TO_VALIDATE` significa que a arquitetura não fixa comportamento de provider sem teste/documentação específica.

| Tema | Opções/questão | Gate |
| --- | --- | --- |
| Nome e mercado | `AgencyTenant` versus Organization; agência apenas ou marca direta | SPEC-A01 |
| Login e RBAC | Fluxo Auth inicial, revogação de membership, papéis/grants e aprovação dupla | SPEC-A01/A02 |
| Client Portal | MVP ou fase posterior; visibilidade padrão e publicação de relatórios | SPEC-A09 |
| Advisor/Domain | Perfil Client com override Product, packs piloto, remoto e RAG | SPEC-A05/Domain |
| Storage | Vercel Blob privado versus Supabase Storage; rich text e export | Artifact/Creative |
| Eventos | Outbox/queue, retries, streaming/Realtime de AgentRun | AgentRun API |
| Contratos | OpenAPI/JSON Schema/package, generated client, autenticação Eve e trace context | API/Agent Context |
| Ambiente | Staging isolado, vault dinâmico, credenciais OAuth e contas de teste | Client Integration |
| Criativo | Imagem/vídeo/voz/render providers, licença, custo e limite por Run | Creative |
| Audiência | Fontes first-party, consentimento, confidence e validação de Persona | Audience |
| Mídia | Canal piloto, capabilities reais por conta, identidade de campaign/ad/adset e stop rules | Paid Media |
| Métricas | Atribuição MVP, normalização, janela mínima e freshness | Metrics/Performance |
| Verba/JEV | Limites por Agency/Client/Campaign, autoapproval, início de JEV e autoexecução | Budget/Optimization |
| Operação | Retenção, RTO/RPO, custo, observabilidade, alertas e offboarding | Foundation/Operations |

Decisões já fixadas: Control Plane separado de execução Eve; Supabase PostgreSQL/Auth/RLS como alvo; OpenTelemetry como padrão; Marketing OS API como fronteira; Product Context/Domain Pack versionados; humano como orquestrador de releases e aprovação inicial de ações externas. Essas decisões não significam que serviços foram conectados.
