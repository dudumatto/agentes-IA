# agent-architecture

## Camadas

1. Indices: `.codex/AGENTS.md`, `.codex/RULES.md`, `.codex/SKILLS.md`
2. Routing: `routing/`
3. Agents: `agents/`
4. Micro-skills: `skills/`
5. Workflows: `workflows/`
6. Memory: `memory/`
7. Docs/Templates: `docs/`, `templates/`

## Modelo hierarquico

- `planning-agent`: decompoe e escolhe workflow.
- `research-agent`: coleta fatos reais.
- Owner agent: executa dominio principal.
- Specialist agents: reduzem risco especifico.
- `testing-agent` + `review-agent`: validam antes da entrega.

## Regra de ownership

Toda tarefa deve ter 1 owner. Especialistas revisam ou limitam risco; nao disputam ownership.

