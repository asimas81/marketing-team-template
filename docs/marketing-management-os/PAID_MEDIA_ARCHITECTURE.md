# PAID_MEDIA_ARCHITECTURE

## Separação de responsabilidades

O futuro `paid-media-strategist` recomenda channel mix, estrutura, objetivo, audiência, budget e experimento, produzindo plano versionado no Client Workspace. Meta, Google e TikTok são conectores, não agentes separados inicialmente. O Marketing OS decide policy, aprovação, ownership, budget e estado canônico. O conector executa uma ação autorizada na conta externa e reconcilia o resultado.

`AdAccount`, `ChannelConnection`, `CampaignExternalMapping`, `AdGroup/AdSetExternalMapping`, `AdExternalMapping`, `CreativeExternalMapping` e `ConversionSource` pertencem a um único Client. Nenhum mapping é criado sem Client e ExternalAccount verificados. A estrutura interna da Campaign permanece canal agnóstica; IDs de provider são referências e não substituem entidades internas. Capabilities disponíveis são descobertas por conta, escopo e versão da API; ausência vira `UNSUPPORTED`, não execução simulada.

Fluxo de escrita: plano/draft → validação de contexto, conta, saúde, budget e claims → aprovação editorial do artifact → autorização humana do payload externo e custo → execução idempotente → reconciliação → publicação/MetricSnapshot/AuditEvent. Criar draft interno pode ser automático; publicação, spend, budget change, pause/resume e launch de experimento exigem policy e aprovação humana iniciais. Falha incerta não permite retry cego. Read-only metrics requer consentimento e mapping antes de importar.

Gate de produção: Agency/Client isolation e RLS testados; OAuth/vault e revogação; account mapping; aprovação e audit; idempotência/reconciliação; budget cap; metric freshness; ambiente/test account; capability discovery; evals de plano e segurança. Nenhum conector real está implementado por esta documentação. Ver [CHANNEL_CONNECTORS_SPEC](./CHANNEL_CONNECTORS_SPEC.md), [CLIENT_INTEGRATION_MODEL](./CLIENT_INTEGRATION_MODEL.md) e [PERFORMANCE_OPTIMIZATION_MODEL](./PERFORMANCE_OPTIMIZATION_MODEL.md).
