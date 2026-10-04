# AUDIENCE_INTELLIGENCE_SPEC

## Contrato

Audience Intelligence é uma capacidade do Client Workspace. O futuro subagente genérico `audience-intelligence` pesquisa, propõe segmentos/personas e revisa hipóteses; o Marketing OS mantém fontes, versões, decisões e vínculos com Product/Campaign. `AudienceSegment` é agrupamento objetivo com critérios observáveis; `Persona` é interpretação comunicacional desses dados. Nem texto gerado por LLM nem `confidence` isolada validam uma persona.

`AudienceResearch` vincula Product, pergunta, método, período e fontes. `AudienceResearchSource` guarda tipo (`FIRST_PARTY_DECLARED`, `FIRST_PARTY_BEHAVIORAL`, `CRM_DATA`, `CAMPAIGN_PERFORMANCE`, `CUSTOMER_INTERVIEW`, `SURVEY`, `SEARCH_SIGNAL`, `SOCIAL_SIGNAL`, `PUBLIC_RESEARCH`, `EXTERNAL_REPORT`, `AGENT_INFERENCE`), owner, coleta, consentimento/finalidade, frescor e referência. SegmentVersion guarda critérios e evidências. PersonaVersion guarda goals, barriers, objections, media behavior, language, triggers, evidências, confiança calibrada, limitações e estado `DRAFT`, `HYPOTHESIS`, `TESTING`, `VALIDATED`, `NEEDS_REVIEW`, `DEPRECATED`. `VALIDATED` exige threshold definido em policy, fonte independente e revisão humana.

TargetingHypothesis e MarketingHypothesis distinguem tese de fato e podem originar Experiment. Campaign fixa `audience_segment_version_id` e `persona_version_id`, sem mutação retroativa. Dados pessoais/CRM entram só com autorização, minimização e finalidade; agentes recebem agregados quando bastam. Toda saída cita fonte/data/escopo e marca inferência. UI Audiences oferece Research, Segments, Personas, Evidence, Hypotheses e vínculo com Experiments/Performance. Evals cobrem grounding, viés, dados sensíveis, falsa validação e revisão após evidência nova.
