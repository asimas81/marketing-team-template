# Permissions Matrix

O [RBAC de Agency e Client](../../marketing-management-os/TENANT_RBAC_MATRIX.md) governa pessoas. A matriz abaixo restringe capacidades do runtime após o OS resolver principal, Client, recurso, versão e policy. `conditional` exige grants e ferramenta apropriados; nenhum agente acessa banco diretamente.

| Agente/capability | Ler contexto | Criar draft/advisory | Alterar contexto publicado | Publish/send/spend/delete |
| --- | --- | --- | --- | --- |
| Marketing Lead | Client/Product/Campaign autorizado | WorkRequest/brief conforme API | Não | Não |
| Product Marketer | Product e evidência | Proposta de posicionamento/contexto | Não; humano publica versão | Não |
| Product/Domain Specialist | Product/Domain/Campaign | Advisory, risco e proposta | Não | Não |
| Audience Intelligence (futuro) | Pesquisa e dados autorizados | Research, segmento/persona hipotética | Não | Não |
| Content/Social/SEO | Brief e fontes da tarefa | Artifact de craft | Não | Não |
| Creative Producer | Brief, fontes, direitos | Creative artifact/variant | Não | Não |
| Email | Copy aprovada e público autorizado | Draft Resend | Não | Atual: send com gate Eve; no OS futuro, aprovação de negócio e executor autorizado com gate Eve adicional quando aplicável |
| Paid Media Strategist (futuro) | Contexto/métricas/contas permitidos | Plano/draft/targeting/budget proposto | Não | Não |
| Performance Optimizer (futuro) | Métricas normalizadas | Recommendation tipada | Não | Não |
| Channel Connector | Conta e payload autorizados | Resultado externo | Não | Apenas ação exata aprovada, idempotente e auditada |

Conexões legadas do template têm gates Eve próprios; esses gates permanecem, mas não substituem aprovação de negócio persistida no OS. Ferramentas de leitura/escrita devem declarar owner, side effect, credencial, ambiente e fallback no [Tools Catalog](../TOOLS_CATALOG.md).

## Ampliação futura: Engagement

| Capacidade | DRAFT/PREPARE | SCHEDULE | SEND/PUBLISH | CRM handoff |
| --- | --- | --- | --- | --- |
| Email atual via Resend | Draft conforme grants legados | Gate Eve conforme tool | Gate Eve existente; OS approval será obrigatório no fluxo futuro | Não |
| Agentic Email no OS (futuro) | Sim, em Client autorizado | Intenção interna; agendamento externo segue gate SEND | Somente executor com approval, consent/suppression e idempotência | Não por padrão |
| Lead Qualification Agent (futuro) | Assessment/proposta do Lead mínimo | Não | Não | Proposta; executor autorizado separado |
| WhatsApp/SMS/DM/Messenger/Web Chat (futuro) | Só após capability/consent policy por canal | Conforme adapter e policy | Somente executor com aprovação e conta Client | Não por padrão |

Roles humanas do Client determinam quem aprova SEND/PUBLISH e CRM handoff. Permissão de agente nunca substitui opt-in válido, suppression ou rate limit.
