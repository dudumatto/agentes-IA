# load-policy

Camadas de contexto:
1. Indices: `.codex/AGENTS.md`, `.codex/RULES.md`, `.codex/SKILLS.md`
2. Routing: `routing/semantic-dispatch.md`
3. Owner agent
4. Rules do dominio
5. Micro-skills especificas
6. Workflow operacional
7. Docs/memory apenas se necessario

Regra:
- nunca carregar `docs/` ou `memory/` inteiro por padrao
- preferir 1 agente owner + 0-3 especialistas

