# AGENTS (Codex-first)

Objetivo: selecionar **o mínimo de agentes** necessários e trabalhar em paralelo, com prompts pequenos.

## Agentes

- `architecture-agent.agent.md`
- `backend-agent.agent.md`
- `frontend-agent.agent.md`
- `design-agent.agent.md`
- `animation-agent.agent.md`
- `testing-agent.agent.md`
- `security-agent.agent.md`
- `review-agent.agent.md`
- `token-efficiency-agent.agent.md`
- `memory-agent.agent.md`

## Regra prática

- UI/UX/visual → `design-agent` + `frontend-agent` (+ `animation-agent` se houver motion)
- API/contrato/regra → `backend-agent` (+ `security-agent` se houver auth/inputs/uploads)
- Mudança grande/risco → sempre incluir `review-agent` + `testing-agent`

Workflows: ver `../workflows/`.

