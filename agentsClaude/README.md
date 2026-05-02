# 🎼 Time de Subagentes — Guia de Instalação

## Agentes incluídos

| Arquivo | Agente | Função |
|---|---|---|
| `maestro.md` | 🎼 Maestro | Orquestrador — planeja e delega |
| `design-ui-agent.md` | 🎨 Design UI Agent | UI/UX — layout, responsividade, a11y, polimento |
| `frontend-specialist.md` | ⚛️ Frontend Specialist | React, Vite, Tailwind CSS |
| `backend-specialist.md` | ☕ Backend Specialist | Spring Boot, Java 21, JWT |
| `integration-engineer.md` | 🔗 Integration Engineer | CORS, contratos, variáveis de ambiente |
| `quality-reviewer.md` | 🔍 Quality Reviewer | Revisão de código, segurança, padrões |

---

## Instalação

### Opção 1 — Global (disponível em todos os projetos)
```bash
mkdir -p ~/.claude/agents
cp *.md ~/.claude/agents/
```

### Opção 2 — Apenas neste projeto (recomendado)
```bash
mkdir -p .claude/agents
cp *.md .claude/agents/
```

---

## Como usar no Claude Code

### Deixar o Maestro coordenar (recomendado)
```
Implemente um módulo de cadastro de produtos com CRUD completo
```
O Maestro automaticamente decompõe a tarefa e delega aos agentes certos.

Regra: se houver impacto em UI/UX (layout/visual/responsividade/a11y), o Maestro inclui uma revisão do `design-ui-agent` antes do `quality-reviewer`.

### Invocar um agente diretamente
```
@frontend-specialist crie um componente de tabela paginada para listar produtos
```
```
@backend-specialist crie o endpoint GET /api/produtos com paginação
```
```
@quality-reviewer revise os arquivos que acabamos de criar
```

### Fluxo completo manual
```
Use o @maestro para implementar autenticação completa com login, logout e proteção de rotas
```

---

## Fluxo Automático do Maestro

```
Usuário → Maestro
              ↓ planeja e define contrato de API
    ┌─────────┴──────────┐
    ↓                    ↓
Backend Specialist   Frontend Specialist
    └─────────┬──────────┘
              ↓ ambos concluídos
         Integration Engineer
              ↓ integração validada
          Quality Reviewer
              ↓ relatório final
            Usuário
```
