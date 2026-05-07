# parallel-dispatch

Ondas de execucao:

Wave 0:
- `research-agent` quando contexto estiver incompleto
- `planning-agent` quando tarefa for grande

Wave 1:
- owner do dominio
- especialistas de risco (design/security/performance/architecture)

Wave 2:
- implementacao pelo owner
- revisao paralela por `testing-agent` e `review-agent`

Regra:
- tarefas independentes podem rodar em paralelo
- escrita em arquivos deve ter ownership claro

