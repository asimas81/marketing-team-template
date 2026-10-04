# ADR Register — propostas

| ADR | Decisão proposta | Estado |
| --- | --- | --- |
| 001 | Separar Control Plane Marketing OS de Execution Plane Eve | Proposta no PRD, aprovação formal pendente |
| 002 | Supabase PostgreSQL como SoR; Auth + RLS em dois níveis | Proposta no PRD, estratégia/testes detalhados pendentes |
| 003 | Marketing OS API como única fronteira de dados para agentes | Proposta, formato/autenticação pendentes |
| 004 | Product Context/Domain Pack versionados e Advisor Profile por Client/Product | Proposta, schema/governança pendentes |
| 005 | Approval de negócio no OS + gate Eve de execução | Proposta, matriz final de papéis pendente |
| 006 | OTel como padrão de correlação cross-plane | Proposta, propagação e retenção pendentes |
| 007 | Contratos canônicos no OS, sem terceiro repo inicial | Proposta, OpenAPI/package pendente |
| 008 | Assets privados em Vercel Blob ou Supabase Storage | Aberta, avaliação necessária |
| 009 | Outbox/queue e reconciliação de ações externas | Aberta, implementação concreta necessária |
| 010 | Audience evidenciada, métricas normalizadas, budget determinístico antes de JEV | Proposta, thresholds/atribuição pendentes |
| 011 | EngagementChannel comum com Email primeiro e canais futuros por capability | Proposta, payloads e provider inicial pendentes |
| 012 | ConsentRecord e suppression por Client/canal/finalidade; SEND separado de DRAFT/PREPARE/SCHEDULE/PUBLISH | Proposta, política por jurisdição e papel pendente |
| 013 | Lead de marketing e CRM handoff mínimo, sem pipeline comercial no OS | Proposta, identidade/deduplicação/mapping pendentes |

Cada ADR deverá registrar contexto, opções, consequência, owner, data e revisão humana antes de se tornar `ACCEPTED`. A existência deste registro não declara aprovação nem altera infraestrutura.
