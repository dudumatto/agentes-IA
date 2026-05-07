# Routing (mínimo + paralelo)

## Seleção mínima

1) Escolha 1 “owner” (frontend OU backend OU architecture).
2) Adicione só o que bloqueia risco real:
   - UI → design (+ animation se necessário)
   - auth/inputs/uploads → security
   - qualquer mudança não-trivial → testing + review
   - decisão estrutural → architecture
   - custo de tokens/duplicação → token-efficiency
   - persistência/Obsidian → memory

## Paralelismo (sem multi-tool)

Rodar em 2 ondas:

- Onda A (antes de codar): `design`/`security`/`architecture` (3–7 bullets cada)
- Onda B (antes de concluir): `testing` + `review` (checklist + riscos)

