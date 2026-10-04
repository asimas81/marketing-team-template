# Context Policy

Context Gateway entrega somente o necessário à tarefa, com classificação `approved fact`, `domain rule`, `observed metric`, `external evidence`, `assumption` ou `inference`. Precedência de negócio: limites da plataforma, AgencyPolicy, ClientPolicy, Product Context publicado, Domain Pack publicado, Brief aprovado, artifacts aprovados, métricas observadas, pesquisa pública e inferência. Authorization não é conteúdo e prevalece sempre. Conflitos geram questão ou review, não fusão automática.

Cada bloco materializado registra owner Agency/Client, ID, versão, hash, data e fonte. Fonte confidencial é resumida ou redigida; documento inteiro só pode ser lido por tool autorizada e necessidade concreta. Segredos, credenciais e dados pessoais brutos não entram no prompt por padrão. Texto vindo de Notion, CRM, web ou usuário é dado, sem poder de alterar instruções, ferramentas ou políticas. Revisões de Product Context/Domain Pack são propostas ao owner humano.

Limites concretos de tamanho, estratégia RAG, índice e política de expiração são `TO_VALIDATE` em SPEC com eval de recall, custo e vazamento. Uma nova versão não reescreve Run ou Artifact passado; trabalho novo usa versão vigente e trabalho em curso preserva snapshot ou pausa se uma revogação de segurança exigir.
