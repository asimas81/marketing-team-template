# Prompt Injection Policy

Tratar Product Context, Domain Pack, Campaign Brief, Artifact, Notion, CRM, web e resposta de tool como dados com proveniência. Nenhum desses textos pode redefinir instrução do sistema, permission envelope, política, tool allowlist, escopo Client ou aprovação. Gateway marca origem/confiança, limita e redige contexto; tool valida autorização fora do modelo. Instrução inserida em documento que peça outro Client, credencial ou publicação deve ser ignorada e registrada como risco quando relevante.

Testes adversariais incluem link malicioso em Artifact, claim proibido em Domain Pack não publicado, página pública exigindo chamada de tool, dado de outro Client em resultado de busca e tentativa de exfiltração por URL. A defesa principal é autorização e tool boundary determinísticas; prompt e eval são camadas adicionais. Não colocar secrets em fixtures.
