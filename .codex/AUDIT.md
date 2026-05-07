# Auditoria (estado atual → gargalos)

## Estrutura atual (observada)

- Repositório:
  - `agentsCodex/` (kit genérico: agents+skills+rules)
  - `agentsClaude/` (variante Claude: agentes grandes e stack duplicada)
  - `agentsGemini/` (variante Gemini: agentes com regras “Zero Chat”)
  - `contextTCC/PROJECT_CONTEXT.md` (contexto de exemplo, ~4.5k tokens)
  - `ROTINA.md` (integração com vault Obsidian)
- Codex global (máquina): `C:\Users\Administrator\.codex/` (não é parte do repo)
- Obsidian vault: `E:\second-brain/` (memórias + scripts)

## Hotspots de token (principais)

- `contextTCC/PROJECT_CONTEXT.md` é monolítico (~4.5k tokens).
- Somando **todos** os kits do repo (Codex+Claude+Gemini+contexto): ~19k tokens (carregar tudo é inviável).
- Loader do vault (`E:\second-brain\scripts\memory\src\commands\load-memory.mjs`) sempre inclui:
  - `RULES.md` e `LEARNINGS.md` do projeto → cresce sem limite e vira “contexto excessivo”.

## Redundâncias (conceituais)

- Repetição de:
  - stack + versões (em vários agentes)
  - checklists iguais (spacing 4/8/..., loading/error, prefers-reduced-motion, upload validation)
  - regras globais (compatibilidade/“não inventar”/“ler arquivos”)
- Efeito: mais tokens, mais ruído, roteamento pior e menos paralelismo real.

## Gargalos de arquitetura

- “Um kit por modelo” (Codex/Claude/Gemini) sem fonte canônica → drift inevitável.
- Memória do vault mistura:
  - regras (invariantes)
  - contexto de projeto
  - learnings históricos
  em um único “dump” no início da sessão.

