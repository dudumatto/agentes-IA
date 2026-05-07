# memoria-guia

Objetivo: reduzir tokens mantendo contexto persistente e reutilizavel.

## Estrutura recomendada (vault)

`02-projects/<projeto>/`
- `README.md`
- `PROJECT_CONTEXT.md`
- `MEMORY.md` (indice; links curtos)
- `LEARNINGS.md` (curado; evitar historico infinito)

## Uso diario (generico)

- Carregar contexto: `node E:/second-brain/scripts/memory/memory-cli.mjs load --project <projeto>`
- Salvar memoria: `node E:/second-brain/scripts/memory/memory-cli.mjs save --project <projeto> --text "..."`
- Aprender: `node E:/second-brain/scripts/memory/memory-cli.mjs learn --project <projeto>`

## Boas praticas

- salvar apenas decisoes, bugs+fix, padroes e workflows.
- evitar logs, dumps e conversa inteira.
- preferir resumo + links.
- usar `.codex/memory/compression-policy.md` para memoria antiga.
- usar `.codex/memory/semantic-indexes.md` para retrieval.

