# CI Policy

Control Plane futuro: install reproduzível, lint/typecheck, unit/domain tests, build, validation de migrations, testes de grants/RLS positivos e negativos, contract tests, integração com mocks, Playwright dos fluxos críticos, secret/security scan e artifact de evidência. Testes de isolamento usam duas Agencies e dois Clients com papéis distintos; policy que existe mas não bloqueia ID adulterado falha o pipeline.

Runtime Eve atual: `pnpm validate` (check, typecheck e discovery com zero erro/aviso), `eve info` com especialistas/tools/connections esperados, tests de tool/contract e evals de contexto, claim, prompt injection, autorização e handoff. Verificar que a superfície de Resend/Notion e gates destrutivos não ampliaram acidentalmente. E2E cross-plane: Request → AgentRun → Eve → Artifact → UI → approval; outra trilha Creative → review → approval, com trace e custo. Testes reais de provider usam ambiente/test account separado e nunca são requisito de PR comum.

CI publica relatório de testes, evals e diffs de contrato. Falha de segurança, RLS, contrato ou eval crítico bloqueia merge. Nenhum pipeline novo foi configurado aqui; este é o contrato para SPECs.
