# Agent Runtime Topology

Estado atual: Lead Eve e sete subagentes locais (`product-marketer`, `product-domain-specialist`, `content-marketer`, `creative-producer`, `social-media-coordinator`, `seo`, `email`). O Lead usa descrição de cada subagente para delegar, e o especialista recebe sessão nova com brief autocontido. O web app atual é chat, não Control Plane operacional.

Alvo: adicionar `audience-intelligence` após dados e revisão de evidência; `paid-media-strategist` após Campaign/Experiment/Client Integration; `performance-optimizer` após métricas normalizadas. São SPECs futuras, não agentes disponíveis. Meta, Google e TikTok começam como adapters. Advisor Profile por Client/Product configura o mesmo `product-domain-specialist`; Remote Agent fica para necessidade comprovada de isolamento ou release independente. Creative Producer mantém adapters por formato em vez de um agente por mídia.

O OS cria AgentRun e permission envelope; Eve decide sequência cognitiva e devolve artifacts/advisories. Handoffs usam IDs e versões fixadas, nunca contexto completo de vários Clients no mesmo Run. Nenhum especialista recebe autoridade direta de publish/send/spend/delete. [AGENT_TOPOLOGY](../../marketing-management-os/AGENT_TOPOLOGY.md) registra as responsabilidades de craft e [runtime contract](../../marketing-management-os/AGENT_RUNTIME_CONTRACT.md) os campos alvo.
