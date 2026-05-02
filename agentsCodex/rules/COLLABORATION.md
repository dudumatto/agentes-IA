# Regras de colaboração (fluxo paralelo simulado)

## Objetivo

Simular “agentes em paralelo” com um único assistente, sem perder qualidade:

1) selecionar agentes → 2) análises curtas → 3) consolidar → 4) implementar → 5) validar.

## Seleção de agentes (mínimo necessário)

Use esta tabela como gatilho:

- UI/CSS/tema/layout → **Design/UI + Frontend**
- Contrato/API/regra de negócio → **Backend + Frontend**
- Auth/permissões/uploads/dados sensíveis → **Security + Backend + QA**
- Bug sem causa clara → **QA + (Backend/Frontend) + Security se envolver inputs**
- Feature nova (fluxo) → **Design/UI + Frontend + Backend + QA + Docs**

## Ordem de execução (sempre)

1. **Entender e ler** os arquivos relevantes (sem suposições).
2. Rodar análise dos agentes selecionados, cada um com 3–7 bullets.
3. Consolidar: listar decisões, trade-offs e riscos.
4. Implementar mudanças (mínimas, seguras, compatíveis).
5. Validar: testes/linters/build + checklist manual do QA/Design.

## Resolução de conflitos

Se agentes “discordarem”:

- Priorizar **segurança** > **correção** > **compatibilidade** > **UX** > **performance** > **estética**.
- Registrar a decisão (curta) e a alternativa descartada.

