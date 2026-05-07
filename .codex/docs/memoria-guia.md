# memoria-guia (Obsidian)

Objetivo: reduzir tokens mantendo contexto persistente e reutilizável.

## Estrutura recomendada (vault)

`02-projects/<projeto>/`
- `README.md`
- `PROJECT_CONTEXT.md`
- `MEMORY.md` (índice; links curtos)
- `LEARNINGS.md` (curado; evitar histórico infinito)

## Uso diário (genérico)

- Carregar contexto do projeto:
  - `node E:/second-brain/scripts/memory/memory-cli.mjs load --project <projeto>`
- Salvar memória (curta e reutilizável):
  - `node E:/second-brain/scripts/memory/memory-cli.mjs save --project <projeto> --text "..." `
- Aprender (quando houver material novo):
  - `node E:/second-brain/scripts/memory/memory-cli.mjs learn --project <projeto>`

## Boas práticas

- salvar apenas: decisões, bugs+fix, padrões, workflows.
- evitar: logs, dumps e conversa inteira.
- preferir “resumo + links” ao invés de texto longo.

