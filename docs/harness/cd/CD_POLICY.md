# CD Policy

Ambientes Development, Preview/Staging e Production têm projetos e dados separados conforme [Environment Matrix](../ENVIRONMENT_MATRIX.md). Preview não publica, envia ou gasta em contas reais por padrão; mocks/test accounts e bloqueio de executor externo são exigidos. Production exige CI verde, revisão de segurança, migration compatível e testada, evals verdes, smoke OTel e aprovação humana. A publicação do runtime Eve segue seu fluxo próprio; dependências cross-repo usam rollout compatível e feature gate.

Rollback de UI/runtime não reverte automaticamente migration ou efeito externo. Plano de release inclui versão de contrato, backup/restauração, janela de observação, health de integrações, monitoramento de custo e gatilho de reversão. Para send/publish/spend incerto, reconciliar estado antes de tentar de novo. Esta documentação não configura Vercel, Supabase nem deploy.
