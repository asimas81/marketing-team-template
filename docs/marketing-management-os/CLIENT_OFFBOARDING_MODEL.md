# CLIENT_OFFBOARDING_MODEL

## Runbook alvo

Offboarding é transição controlada de um `ClientWorkspace`, iniciada por Agency Owner/Admin ou owner delegado. Registra motivo, solicitante, prazo, política de retenção, responsabilidades contratuais e um `offboarding_id`. Não apaga dados imediatamente. O Client entra em `OFFBOARDING`, bloqueando novas Requests, AgentRuns e execuções externas enquanto leitura/exportação autorizada continua.

1. Inventariar Campaigns ativas, schedules, AgentRuns, approvals, contas externas, webhooks, assets, dados pessoais, relatórios e custos. Mostrar plano e dependências ao responsável.
2. Cancelar ou concluir AgentRuns com estado e auditoria; desabilitar agendas, publicar/enviar/gastar e revogar approvals de execução pendentes. Para ação já enviada, reconciliar resultado externo antes de encerramento.
3. Desconectar ClientIntegrations, revogar tokens no vault/provedor e webhooks, verificar revogação e registrar falhas. Outros Clients da Agency continuam inalterados.
4. Exportar dados canônicos, versões, fontes, métricas com definição e referências externas em pacote controlado com manifest/checksum; registrar quem recebeu e autorização.
5. Encerrar ClientWorkspaceMemberships e acesso ao portal. Arquivar Campaigns e referências. Aplicar retenção, anonimização ou deleção conforme ClientPolicy, contrato e limites da plataforma; preservar audit obrigatório pelo prazo definido.
6. Verificar impossibilidade de acesso por Client/AgentRun/connector, inexistência de credencial ativa e integridade do export. Marcar `ARCHIVED` apenas após pendências resolvidas ou documentadas.

Falhas de revogação ou exportação deixam offboarding em estado pendente com owner, retry controlado e alerta. Recuperação dentro da janela de retenção exige nova autorização e reconexão explícita; approvals e tokens antigos não são reativados automaticamente. Decisões de prazo de retenção, formato de exportação e tratamento de dados sob litígio permanecem para SPEC/policy.
