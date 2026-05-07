# Migração (compatível, sem quebra)

## Objetivo

Tornar `.codex/` a **fonte canônica** e manter `agentsCodex/`, `agentsClaude/`, `agentsGemini/` como:
- legados preservados
- alvos de export/geração (futuro)

## Caminho recomendado (ordem)

1) Adotar `.codex/` para trabalho diário (agents/skills/rules/workflows).
2) Manter kits legados sem mexer (compat).
3) Gradualmente:
   - reduzir duplicação nos kits legados
   - migrar checklists para skills pequenas em `.codex/skills/`
4) (Opcional) Criar “exporters” para gerar variantes Claude/Gemini a partir de templates.

## Integração com o vault (token-efficient)

Problema: `load` do vault imprime `LEARNINGS.md` + `RULES.md` sempre.

Sugestão (sem quebrar):
- manter `load` como está
- adicionar um perfil “mínimo” (novo comando/flag), por exemplo:
  - `load --profile minimal` (apenas `PROJECT_CONTEXT` + últimas memórias)
  - `load --include README,PROJECT_CONTEXT,MEMORY` (sem LEARNINGS/RULES)

Observação: isto requer editar scripts em `E:\second-brain\scripts\memory\...` (fora do repo).

## Mapeamento de agentes (alto nível)

- `.codex/agents/frontend-agent` ≈ `agentsCodex/agents/FRONTEND` ≈ `agentsClaude/frontend-specialist` ≈ `agentsGemini/react-pro`
- `.codex/agents/backend-agent` ≈ `agentsCodex/agents/BACKEND` ≈ `agentsClaude/backend-specialist` ≈ `agentsGemini/spring-expert`
- `.codex/agents/design-agent` ≈ `agentsCodex/agents/DESIGN_UI` ≈ `agentsClaude/design-ui-agent` ≈ `agentsGemini/design-ui`
- `.codex/agents/security-agent` ≈ `agentsCodex/agents/SECURITY` (e parte do `quality-reviewer`/`revisor`)
- `.codex/agents/testing-agent` ≈ `agentsCodex/agents/QA_TEST`
- `.codex/agents/review-agent` ≈ `agentsClaude/quality-reviewer` ≈ `agentsGemini/revisor`
- `.codex/agents/architecture-agent` (novo; faltava como unidade leve)
- `.codex/agents/token-efficiency-agent` (novo; faltava como unidade leve)
- `.codex/agents/memory-agent` (novo; faltava como unidade leve)
- `.codex/agents/animation-agent` (novo; faltava como unidade leve)

