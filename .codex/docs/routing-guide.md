# routing-guide

Objetivo: carregar o menor contexto suficiente para executar bem.

## Processo

1. Leia `.codex/AGENTS.md`, `.codex/RULES.md`, `.codex/SKILLS.md`.
2. Use `routing/semantic-dispatch.md`.
3. Escolha 1 owner.
4. Adicione especialistas apenas por sinal semantico.
5. Carregue micro-skills pelo `routing/skill-map.md`.
6. Escolha workflow pelo `routing/workflow-map.md`.

## Exemplos

- "corrigir upload inseguro" -> `upload-security-agent`, `upload-security.md`, `debug-workflow.md`
- "otimizar query JPA" -> `backend-agent`, `performance-agent`, `spring-data-jpa.md`
- "animacao GSAP com scroll" -> `animation-agent`, `gsap-scrolltrigger.md`, `animation-performance.md`
- "reduzir tokens da memoria" -> `memory-agent`, `token-efficiency-agent`, `memory-compression.md`

