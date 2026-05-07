# semantic-dispatch

Ordem de dispatch:
1. Detectar dominio principal.
2. Escolher 1 owner.
3. Adicionar especialistas por risco/sinal semantico.
4. Carregar rules do dominio.
5. Carregar micro-skills especificas.
6. Escolher workflow.

Fallback:
- se dominio ambiguo: `research-agent` + `planning-agent`
- se risco alto: adicionar `review-agent` e `testing-agent`

