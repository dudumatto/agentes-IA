# reorganization-report

Data: 2026-05-06

## Objetivo

Deixar o repositório pronto para uso global: modular, token-efficient, sem duplicação e com nomes padronizados (kebab-case).

## Antes (resumo)

Top-level:
- `.codex/` (estrutura própria, mas com agentes `*.agent.md` e skills em subpastas `*/SKILL.md`)
- `agentsCodex/`, `agentsClaude/`, `agentsGemini/` (kits legados com conteúdo sobreposto)
- `MEMORIA_GUIA.md` e `ROTINA_IA.md` (docs globais fora de `.codex/`)
- `contextTCC/` (contexto específico de exemplo)

Problemas:
- nomes inconsistentes (`*.agent.md`, skills em subpastas) vs padrão desejado
- repetição de regras/checklists entre kits
- docs globais espalhadas fora de `.codex/`

## Depois (estrutura final)

`.codex/`
- `AGENTS.md` / `RULES.md` / `SKILLS.md` (índices leves)
- `agents/` (agentes padronizados)
- `skills/` (skills padronizadas)
- `rules/` (rules padronizadas)
- `workflows/` (processos passo a passo)
- `templates/` (formatos reutilizáveis)
- `docs/` (documentação explicativa)

## Renomeados / convertidos

Agentes (de `*.agent.md` → `*.md`):
- `.codex/agents/*-agent.agent.md` → `.codex/agents/*-agent.md`

Skills (de `.../SKILL.md` → `skills/*.md`):
- `.codex/skills/**/SKILL.md` → `.codex/skills/*.md` (lista padronizada)

Rules (novas, padronizadas):
- criado conjunto em `.codex/rules/*.md` (curtas e obrigatórias)

Workflows/Templates (padronizados):
- `.codex/workflows/*.md` e `.codex/templates/*.md`

Docs (centralizados):
- criado `.codex/docs/*` e `MEMORIA_GUIA.md` / `ROTINA_IA.md` viraram ponteiros

## Duplicações removidas/evitadas

- removidos índices antigos dentro de `.codex/agents/` e `README`s redundantes dentro de `.codex/`
- removidas skills antigas em formato “pasta + SKILL.md”
- removidas rules/workflows/templates antigos em nomes não padronizados

## Links e referências

- atualizado `README.md` para apontar para `.codex/docs/context-engineering.md`
- verificado: sem referências para caminhos antigos de rules/workflows/templates removidos

## Observações importantes

- `agentsCodex/`, `agentsClaude/`, `agentsGemini/` e `contextTCC/` foram preservados (compatibilidade).
- Existem diretórios vazios legados dentro de `.codex/` (ex.: `.codex/automations/` e subpastas antigas de skills) que **não puderam ser removidos via shell** no sandbox atual por ACL/deny de delete; o conteúdo foi removido e não é mais referenciado.

## Próximos ajustes recomendados

1) (Opcional) mover kits legados para uma pasta `legacy/` e manter apenas ponteiros (se você quiser “repo ultra-limpo”).
2) (Fora do repo) ajustar o loader do vault (`E:/second-brain/scripts/memory/...`) para suportar perfil “mínimo” (não imprimir `RULES.md` e `LEARNINGS.md` sempre).

