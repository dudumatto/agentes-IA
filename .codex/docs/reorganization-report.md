# reorganization-report

Data: 2026-05-07

## Objetivo

Transformar a arquitetura em um AI Operating System modular para Codex, Claude e Gemini, otimizado para multi-agentes, token efficiency, context engineering, routing semantico e memoria persistente.

## Estrutura antes

- `.codex/` com agentes, skills, rules, workflows, templates e docs.
- `agentsCodex/`, `agentsClaude/`, `agentsGemini/` como kits legados com bastante overlap.
- `contextTCC/PROJECT_CONTEXT.md` como contexto especifico e grande.
- Docs raiz (`ROTINA_IA.md`, `MEMORIA_GUIA.md`) ja convertidas em ponteiros.

Hotspots:
- `contextTCC/PROJECT_CONTEXT.md` e kits legados sao os maiores custos de token.
- Overlap recorrente entre frontend/design/security/review/test.
- Faltavam `routing/` e `memory/` como camadas explicitas.

## Estrutura depois

`.codex/`
- `AGENTS.md`, `RULES.md`, `SKILLS.md` como indices leves.
- `agents/` com agentes especializados.
- `skills/` com micro-skills.
- `rules/` com regras curtas e obrigatorias.
- `workflows/` com passos operacionais.
- `routing/` com dispatch semantico.
- `memory/` com camadas de memoria elastica.
- `templates/` com formatos reutilizaveis.
- `docs/` com guias de arquitetura, routing, contexto, tokens e memoria.

## Agentes criados

- `auth-security-agent.md`
- `upload-security-agent.md`
- `performance-agent.md`
- `refactor-agent.md`
- `debug-agent.md`
- `research-agent.md`
- `planning-agent.md`

## Agentes ajustados

- `security-agent.md` virou triagem AppSec geral e delega auth/upload.
- `review-agent.md` ficou focado em auditoria final independente.

## Micro-skills criadas

- React: `react-components.md`, `react-hooks.md`, `react-performance.md`, `react-state-management.md`
- Spring: `spring-controllers.md`, `spring-services.md`, `spring-data-jpa.md`
- UI/animation: `accessibility.md`, `design-tokens.md`, `tailwind-layout.md`, `gsap-scrolltrigger.md`, `animation-performance.md`
- Context/memory/routing: `context-compression.md`, `semantic-routing.md`, `memory-compression.md`
- API/security: `api-contracts.md`, `jwt-security.md`

## Skills removidas/mescladas

- `react-best-practices.md` -> micro-skills React.
- `spring-best-practices.md` -> micro-skills Spring.
- `testing-workflows.md` -> workflows + testing rules.

## Rules adicionadas

- `memory-rules.md`
- `routing-rules.md`
- `refactor-rules.md`
- `context-rules.md`

## Workflows adicionados

- `planning-workflow.md`
- `refactor-workflow.md`
- `debug-workflow.md`

## Routing

Criado `.codex/routing/`:
- `semantic-dispatch.md`
- `domain-map.md`
- `skill-map.md`
- `workflow-map.md`
- `load-policy.md`
- `parallel-dispatch.md`

Melhoria:
- task -> dominio -> owner -> especialistas -> micro-skills -> workflow.

## Memoria

Criado `.codex/memory/`:
- `long-term-memory.md`
- `project-memory.md`
- `learnings.md`
- `summaries.md`
- `semantic-indexes.md`
- `compression-policy.md`
- `memory-graph.md`

Melhoria:
- memoria como indice + resumo + ponteiro, sem dump.
- projeto fica fora da `.codex` global.

## Docs atualizadas

- `agent-architecture.md`
- `routing-guide.md`
- `context-engineering.md`
- `token-guide.md`
- `memoria-guia.md`
- `rotina-ia.md`

## Melhorias de token efficiency

- indices leves no topo.
- micro-skills carregadas sob demanda.
- docs e memory fora do prompt base.
- routing define camadas de load.
- contexto especifico (`contextTCC/`) permanece fora da `.codex`.

## Observacoes

- `agentsCodex/`, `agentsClaude/` e `agentsGemini/` foram preservados como compatibilidade/legado.
- Diretorios vazios antigos dentro de `.codex/skills/` e `.codex/automations/` foram removidos apos limpeza elevada.

## Proximos upgrades recomendados

1. Criar exporters para gerar variantes Claude/Gemini a partir da `.codex` canonica.
2. Mover kits legados para `legacy/` quando nao precisar mais de compatibilidade top-level.
3. Ajustar o loader do vault para `--profile minimal`.
4. Criar script de validacao de links e routing.
