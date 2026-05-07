# gitagents — sistema modular de contexto (Codex-first)

Este repositório organiza uma arquitetura de contexto **modular**, **escalável** e **token-efficient** para IA (Codex), com agentes especializados, skills sob demanda, rules curtas e workflows paralelos.

## Estrutura

- **Canônico (recomendado):** `.codex/` (agents/skills/rules/workflows/templates/automations)
- **Kits legados (preservados):**
  - `agentsCodex/` — Agent Kit genérico (agentes + skills + rules)
  - `agentsClaude/` — conjunto de agentes no formato do Claude
  - `agentsGemini/` — conjunto de agentes no formato do Gemini
- **Exemplo de contexto de projeto:** `contextTCC/` (não é agente/skill/rule)

## Quando usar cada agente (conceito)

- **Maestro/Orquestrador**: decompõe, delega e consolida.
- **Design UI (Claude Design-like)**: revisa UI/UX e define checklist.
- **Frontend**: implementa UI e lógica de cliente.
- **Backend**: implementa API/regras de negócio e contratos.
- **Integration**: garante compatibilidade front/back e config de ambiente.
- **QA/Test**: valida cenários e regressões.
- **Security**: valida auth/autorização/inputs e riscos.
- **Docs**: mantém documentação curta e correta.

## Regra-chave: Design antes de concluir

Sempre que houver impacto em **interface, layout, frontend visual ou experiência do usuário**:

1. **Design UI** propõe mudanças mínimas + checklist
2. **Frontend** implementa
3. **Design UI** revisa/valida
4. **QA/Test** valida (incluindo responsividade básica)

Backend/Security/QA/Docs só acionam design quando houver impacto visual/UX.

## Como combinar agents + skills + rules

- **Agents**: quem analisa e decide (responsabilidades + checklists).
- **Skills**: como executar bem (sob demanda).
- **Rules**: como coordenar, consolidar e validar.

## Leitura rápida (recomendado)

- Routing + paralelismo: `.codex/docs/context-engineering.md`
- Rules curtas: `.codex/rules/`
- Skills sob demanda: `.codex/skills/`
- Workflows: `.codex/workflows/`
- Kit legado (se precisar): `agentsCodex/README.md`
