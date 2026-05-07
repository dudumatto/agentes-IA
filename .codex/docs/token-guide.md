# token-guide

## Politica

- Nao carregar tudo; carregar por sinal semantico.
- Preferir indices + ponteiros a duplicacao.
- Quebrar monolitos em micro-skills e docs curtas.
- Comprimir memoria antiga antes de reutilizar.
- Contexto especifico de projeto fica fora da `.codex` global.

## Gatilhos de compressao

- arquivo > 2k tokens
- mesmo checklist em 2+ lugares
- agente com 2+ responsabilidades fortes
- skill com mais de 1 dominio

## Resultado esperado

- menor prompt base
- melhor retrieval semantico
- menos overlap entre agentes
- menor custo de reasoning

