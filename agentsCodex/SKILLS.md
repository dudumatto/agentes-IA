# SKILLS.md

## 🎯 Objetivo

Definir as habilidades técnicas que a IA deve usar ao analisar, corrigir ou desenvolver código.

---

## 🐞 Debugging

### Capacidade

* Encontrar causa raiz de bugs
* Analisar stack trace
* Identificar fluxo quebrado
* Diferenciar sintoma vs causa

### Deve fazer

* Apontar linha/arquivo do erro
* Explicar por que acontece
* Sugerir correção mínima

---

## ⚙️ Backend (Spring Boot)

### Capacidade

* Criar e corrigir APIs REST
* Trabalhar com Controllers, Services e Repositories
* Usar DTOs corretamente

### Deve fazer

* Garantir separação de camadas
* Validar dados antes de persistir
* Implementar paginação
* Tratar erros corretamente

---

## 🗄️ Database (JPA/Hibernate)

### Capacidade

* Criar e corrigir queries
* Trabalhar com Specification
* Resolver N+1 queries

### Deve fazer

* Validar relacionamentos (@ManyToOne, etc.)
* Corrigir paths JPA (ex: area.curso.nome)
* Usar JOIN FETCH quando necessário

---

## 🔍 Filtering / Search

### Capacidade

* Criar filtros combinados (AND)
* Trabalhar com query params

### Deve fazer

* Combinar filtros corretamente
* Fazer busca case-insensitive
* Validar parâmetros inválidos

---

## 🎨 Frontend (React)

### Capacidade

* Criar componentes
* Consumir APIs
* Gerenciar estado

### Deve fazer

* Garantir compatibilidade com backend
* Corrigir query params
* Tratar loading e erro

---

## 🔐 Security

### Capacidade

* Validar autenticação JWT
* Implementar controle de acesso

### Deve fazer

* Verificar permissões (aluno vs orientador)
* Validar inputs
* Evitar vulnerabilidades comuns

---

## ⚡ Performance

### Capacidade

* Identificar gargalos
* Otimizar consultas

### Deve fazer

* Evitar loops com query
* Garantir paginação
* Reduzir dados carregados

---

## 🧪 Testing

### Capacidade

* Criar testes unitários e de integração

### Deve fazer

* Testar filtros combinados
* Testar permissões
* Testar erros

---

## ♻️ Refactoring

### Capacidade

* Melhorar código sem alterar comportamento

### Deve fazer

* Reduzir duplicação
* Melhorar nomes
* Dividir métodos grandes

---

## 🧠 Architecture Analysis

### Capacidade

* Entender estrutura do sistema

### Deve fazer

* Mapear fluxo de dados
* Verificar consistência entre camadas
* Detectar problemas estruturais

---

## 🚀 Como usar

Sempre que executar uma task, aplicar as skills relevantes:

### Exemplo

* Bug → Debugging + Backend
* Filtro → Filtering + Database
* API → Backend + Security
* Performance → Performance + Database

---

## 🏁 Prioridade de Skills

1. Debugging
2. Backend
3. Database
4. Security
5. Performance
6. Frontend
7. Testing
8. Refactoring
