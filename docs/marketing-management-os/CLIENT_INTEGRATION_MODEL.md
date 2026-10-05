# CLIENT_INTEGRATION_MODEL

## Ownership e catálogo

`ClientIntegration` pertence exatamente a `(agency_id, client_workspace_id)`, com provider, capabilities descobertas, escopos concedidos, `credential_ref` opaca, `connected_by`, timestamps, health e política de uso. `ExternalAccount` vincula uma integração a `external_account_id`, tipo (ad account, customer, page, pixel, lista, propriedade analytics etc.), nome, permissões e status. Um ID externo pode aparecer em mais de um contexto apenas após verificação de ownership e autorização explícita; nunca é prova de acesso por si. `CampaignExternalMapping` e `CreativeExternalMapping` exigem Client owner idêntico ao da conta externa e do objeto interno.

Meta, Google Ads, TikTok Ads, CRM, Resend, Brevo, Analytics e Notion opcional usam esse modelo. Integração de plataforma no nível Agency pode administrar instalação/consentimento, mas toda conta operacional e ação mantém Client owner explícito. O Resend atual autoriza por usuário via Vercel Connect; a migração deve reconciliar principal, Client, domínio, lista e permissões antes de habilitar envio pelo OS.

## Ciclo de vida

1. Admin autorizado inicia OAuth no contexto do Client; `state` associa sessão, Agency, Client e intenção com expiração. Callback server-side valida estado e identidade, descobre contas e escopos e apresenta seleção explícita.
2. Credencial dinâmica fica em vault/serviço seguro, criptografada e rotacionável; banco guarda apenas referência e metadados. Token não entra no browser, prompt, Artifact, trace ou resposta de tool.
3. Conta selecionada recebe mapping e capability manifest efetivamente verificado. `CONNECTED`, `DEGRADED`, `EXPIRED`, `REAUTH_REQUIRED`, `DISCONNECTED` são estados de health. A UI mostra escopo, conta, permissões, último sync e responsável sem segredos.
4. Reauth substitui credencial preservando trilha. Revogação bloqueia novas ações, tenta revogar no provedor, invalida mappings ativos e registra resultado. Falha de revogação fica pendente com alerta.
5. Webhooks são autenticados, deduplicados, correlacionados à conta/Client e reconciliados; evento sem owner conhecido fica em quarentena, sem mutar estado de outro Client.

Antes de execução, API revalida membership, ClientPolicy, capacidade, health, account mapping, aprovação sobre snapshot e idempotency key. Conector recebe token somente no serviço executor. Retries de send/publish/spend consultam estado externo antes de repetir. [CHANNEL_CONNECTORS_SPEC](./CHANNEL_CONNECTORS_SPEC.md) detalha o contrato por canal. Escolha concreta de vault e fluxos OAuth por provider permanece aberta para SPEC.
