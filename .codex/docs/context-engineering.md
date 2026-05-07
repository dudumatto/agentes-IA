# context-engineering

## Princípios

- Contexto mínimo por padrão (progressive disclosure).
- Modularidade: agentes/skills/rules/workflows/templates/docs separados.
- Fonte canônica única (`.codex/`) para evitar drift entre “kits”.

## Roteamento (mínimo + paralelo)

- Escolher 1 owner (frontend/backend/architecture).
- Antes de codar (onda A): design/security/architecture (se aplicável).
- Antes de concluir (onda B): testing + review.

## Anti-patterns

- carregar `RULES` e `LEARNINGS` inteiros sempre
- duplicar stack/regras em múltiplos agentes
- criar docs monolíticas (>2k tokens)

