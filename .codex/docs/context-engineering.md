# context-engineering

## Principios

- Contexto minimo por padrao.
- Progressive disclosure: indice -> routing -> agent -> rule -> micro-skill -> docs.
- Context slicing: carregar apenas o dominio da task.
- Context compression: resumo + ponteiro para detalhes.
- Semantic layering: cada pasta tem uma funcao unica.

## Camadas de carregamento

1. `.codex/AGENTS.md`, `.codex/RULES.md`, `.codex/SKILLS.md`
2. `routing/semantic-dispatch.md`
3. 1 owner agent
4. rules do dominio
5. micro-skills especificas
6. workflow operacional
7. memory/docs sob demanda

## Anti-patterns

- carregar `docs/` ou `memory/` inteiro por padrao
- duplicar stack/regras em varios agentes
- misturar workflow dentro de rules
- salvar contexto especifico de projeto na `.codex` global

