# `.codex/` — Context Architecture (Modular)

Este diretório é a **fonte canônica** do seu sistema de contexto para IA (Codex-first):

- `agents/` — especialistas leves (responsabilidade única)
- `skills/` — módulos pequenos (progressive disclosure)
- `rules/` — regras curtas, proibitivas e diretas
- `workflows/` — roteiros de execução paralela (research → plan → execute → review)
- `templates/` — trechos reutilizáveis (prompts, checklists, notas de memória)
- `automations/` — docs e templates de automações (sem acoplamento a um app)

Compatibilidade:
- `agentsCodex/`, `agentsClaude/`, `agentsGemini/` permanecem como kits legados/alternativos.
- Use este `.codex/` como “origem” para evoluções e geração de variantes.

