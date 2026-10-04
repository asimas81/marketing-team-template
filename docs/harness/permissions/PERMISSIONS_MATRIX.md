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
| Email | Copy aprovada e público autorizado | Draft Resend | Não | Send só via aprovação OS + gate Eve |
| Paid Media Strategist (futuro) | Contexto/métricas/contas permitidos | Plano/draft/targeting/budget proposto | Não | Não |
| Performance Optimizer (futuro) | Métricas normalizadas | Recommendation tipada | Não | Não |
| Channel Connector | Conta e payload autorizados | Resultado externo | Não | Apenas ação exata aprovada, idempotente e auditada |

Conexões legadas do template têm gates Eve próprios; esses gates permanecem, mas não substituem aprovação de negócio persistida no OS. Ferramentas de leitura/escrita devem declarar owner, side effect, credencial, ambiente e fallback no [Tools Catalog](../TOOLS_CATALOG.md).
