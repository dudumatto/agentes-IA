Claude Context & Rules
Tech Stack & Arquitetura
Backend: Java 21, Spring Boot 4.0.3, Spring Data JPA, Hibernate, Maven, REST (Jackson), Lombok, Validation (Bean Validation), Spring Security (JJWT 0.12.6), Springdoc OpenAPI 3.0.0.

Frontend: React 18.3.1 (Vite 6.3.5), Tailwind CSS 4.1.12, React Router DOM, Axios, Hooks (useState, useEffect, useContext, useReducer), Custom Hooks, ESLint, Prettier, Vitest + React Testing Library.

Node: 18.x || 20.x

Arquitetura: Camada controller → service → repository → entity. DTOs obrigatórios. Pacotes por feature no backend. No frontend, estrutura: components/, hooks/, services/, utils/, pages/.

Diretrizes de Código - Backend (Spring Boot 4.0.3)
Pacotes: controller, service, repository, model (entity & DTO), config, exception, util, security.

Nomenclatura: Classes em PascalCase, métodos em camelCase. Interfaces: Repository, Service.

Injeção de Dependência: Usar constructor injection via @RequiredArgsConstructor do Lombok. Proibido @Autowired em campos.

DTOs: Uso obrigatório para entrada/saída. Jamais expor Entities em Controllers.

Tratamento de Exceções: Global com @ControllerAdvice. Retornar ResponseEntity<ErrorResponse> padronizado.

Security: Implementação com JJWT 0.12.6 (usar nova sintaxe de Jwts.builder()).

Diretrizes de Código - Frontend (React & Tailwind 4)
Estilização: Priorizar utilitários do Tailwind CSS 4.1.12. Seguir novos padrões de configuração do v4.

Componentes: Funcionais com arrow functions. Nomeação PascalCase.

Build Tool: Vite. Respostas de erro e scripts devem considerar o ambiente Vite.

Consumo de API: Instância centralizada do Axios em services/api.js com interceptores para anexar o Token JWT.

Organização: - src/components/ (UI reutilizável)

src/pages/ (Páginas/Rotas)

src/services/ (Integração API)

Regras de Comportamento da IA (Redução de Tokens)
Seja Conciso: Responda apenas com o código necessário ou a solução direta.

Sem Verbosidade: Proibido introduções (ex: "Claro, eu posso ajudar...") ou conclusões.

Diff-Only: Ao modificar arquivos existentes, forneça apenas o trecho alterado.

Foco Técnico: Priorizar segurança (Java 21 features), performance e conformidade com o TCC.

Zero Explicação: Não explique o que o código faz, a menos que eu pergunte "por quê".