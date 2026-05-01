# PROJECT CONTEXT

> **Fonte de verdade:** código do repositório (principal) + `caminhos API TCC.docx` (rotas pretendidas) + `TCC COTIL 2026.pdf` (visão geral).  
> **Observação importante (PDF):** o arquivo `TCC COTIL 2026.pdf` não é extraível de forma confiável com as ferramentas locais disponíveis neste ambiente (conteúdo majoritariamente não-textual/encodado). Portanto, este contexto se apoia **principalmente no código** e usa o `.docx` como referência de intenção, apontando divergências explicitamente.

## 📌 Descrição do Sistema

Pelo **código** e pela documentação de rotas (`caminhos API TCC.docx`), o sistema é uma plataforma para:
- autenticação de usuários (com foco em **cadastro público apenas para ALUNO**),
- cadastro/gestão de **projetos** (iniciação científica/TCC),
- **inscrição** de alunos em projetos, com fluxo de aprovação/rejeição por orientador,
- **recrutamento** (aprovação direta) de colaboradores,
- **conversas/mensagens** (privadas e por projeto),
- **documentos** por usuário (upload + download/preview),
- **feedback** de alunos participantes,
- **progresso** de projeto,
- **notificações** para eventos do sistema,
- visão de **dashboard** com contadores.

## 🧠 Arquitetura

### Backend (Spring Boot)
- **Padrão real:** MVC em camadas (Controller → Service → Repository) com DTOs de request/response.
- **Persistência:** Spring Data JPA/Hibernate com entidades anotadas (`@Entity`) e repositórios `JpaRepository`/`JpaSpecificationExecutor`.
- **Filtros/busca:** combinações de filtros em `ProjetoService` via `Specification<Projeto>`.
- **Erros:** uso recorrente de `ResponseStatusException` nos services; controllers retornam `ResponseEntity`.
- **Documentação:** OpenAPI/Swagger habilitado via `OpenApiConfig`.

### Frontend (React + Vite)
- **Integração HTTP:** `fetch` centralizado em `src/app/services/api.js`, adicionando `Authorization: Bearer <token>` quando há token em `localStorage`.
- **URL base:** `VITE_API_URL` (fallback `http://localhost:8080`).
- **Estado auth:** token persistido em `localStorage` (`tcc_auth_token`), e contexto de autenticação em `AuthProvider`.

## ⚙️ Backend

### Controllers e Endpoints (código real)

Todos endpoints abaixo exigem autenticação **exceto**: `/api/auth/login`, `/api/auth/register`, Swagger (`/v3/api-docs/**`, `/swagger-ui/**`, `/swagger-ui.html`) e `/error` (ver `SecurityConfig`).

- `AreaController`
  - `GET /api/areas`
- `AuthController`
  - `POST /api/auth/register`
  - `POST /api/auth/login`
  - `POST /api/auth/logout`
  - `PUT /api/auth/senha`
- `UsuarioController`
  - `GET /api/usuarios` (apenas ORIENTADOR)
  - `GET /api/usuarios/pagina` (apenas ORIENTADOR)
  - `GET /api/usuarios/me`
  - `PUT /api/usuarios/me/preferencias`
  - `GET /api/usuarios/minhas-inscricoes`
  - `GET /api/usuarios/{id}`
  - `PUT /api/usuarios/{id}`
  - `DELETE /api/usuarios/{id}` (soft-delete: `ativo=false`)
  - `GET /api/usuarios/{id}/projetos`
  - `GET /api/usuarios/{id}/inscricoes`
  - `GET /api/usuarios/{id}/documentos`
- `ProjetoController`
  - `GET /api/projetos` (filtros: `status`, `areaId`, `area`, `curso`, `busca`)
  - `GET /api/projetos/pagina` (+ `meusProjetos`, `page`, `size`, `sort`, `direction`)
  - `GET /api/projetos/{id}`
  - `POST /api/projetos`
  - `PUT /api/projetos/{id}`
  - `DELETE /api/projetos/{id}`
  - `POST /api/projetos/{id}/recrutar`
  - `GET /api/projetos/{id}/colaboradores`
  - `DELETE /api/projetos/{id}/colaboradores/{usuarioId}`
- `InscricaoController`
  - `GET /api/inscricoes`
  - `GET /api/inscricoes/pagina`
  - `GET /api/inscricoes/{id}`
  - `POST /api/inscricoes`
  - `PUT /api/inscricoes/{id}`
  - `DELETE /api/inscricoes/{id}`
  - `DELETE /api/inscricoes/{id}/cancelar`
  - `GET /api/inscricoes/projeto/{projetoId}`
  - `GET /api/inscricoes/projeto/{projetoId}/pagina`
  - `PUT /api/inscricoes/{id}/aprovar`
  - `PUT /api/inscricoes/{id}/rejeitar`
- `DocumentoController`
  - `POST /api/documentos/upload` (multipart)
  - `GET /api/documentos/usuario/{usuarioId}`
  - `DELETE /api/documentos/{id}`
  - `GET /api/documentos/{id}/download`
  - `GET /api/documentos/{id}/preview` (somente PDF)
- `ConversaController`
  - `POST /api/conversas` (abre/cria por projeto)
  - `GET /api/conversas/projeto/{projetoId}`
  - `POST /api/conversas/projeto/{projetoId}/abrir`
  - `POST /api/conversas/privada/{outroUsuarioId}`
  - `GET /api/conversas/{usuarioId}`
  - `GET /api/conversas/{usuarioId}/pagina`
  - `GET /api/conversas/{usuarioId}/todas`
  - `GET /api/conversas/{id}/mensagens`
  - `GET /api/conversas/{id}/mensagens/pagina`
  - `POST /api/conversas/{id}/mensagem`
  - `PUT /api/conversas/mensagem/{mensagemId}`
  - `DELETE /api/conversas/mensagem/{mensagemId}`
- `FeedbackController`
  - `POST /api/feedback`
  - `GET /api/feedback/projeto/{id}`
  - `GET /api/feedback/projeto/{id}/pagina`
  - `GET /api/feedback/usuario/{id}`
  - `GET /api/feedback/usuario/{id}/pagina`
- `ProgressoController`
  - `POST /api/projetos/{id}/progresso`
  - `GET /api/projetos/{id}/progresso`
  - `GET /api/projetos/{id}/progresso/pagina`
  - `PUT /api/progresso/{id}`
  - `DELETE /api/progresso/{id}`
- `NotificacaoController`
  - `GET /api/notificacoes`
  - `GET /api/notificacoes/pagina`
  - `PUT /api/notificacoes/{id}/ler`
  - `PUT /api/notificacoes/ler-todas`
- `DashboardController`
  - `GET /api/dashboard`

### Services (regras de negócio relevantes – código real)

- `AuthService`
  - **Cadastro público só para `TipoUsuario.ALUNO`**; tenta bloquear cadastro de orientador via `/api/auth/register`.
  - JWT gerado com `sub=email` + claim `tipo`.
  - `changePassword`: valida senha atual e atualiza hash BCrypt.
- `ProjetoService`
  - `create`: orientador cria projeto como orientador; caso contrário cria como aluno e **cria inscrição automática APROVADA para o aluno criador**.
  - `delete/update`: permitido apenas para orientador do projeto ou aluno criador.
  - `recrutar`: permitido para “gestores do projeto” (orientador do projeto ou aluno criador) e apenas para usuários do tipo ALUNO; cria/atualiza inscrição como APROVADA.
  - Filtros por `Specification`: `status`, `areaId`, `area`, `curso`, `busca`. Suporte especial a `status=ATIVO` (interpreta como ABERTO ou EM_ANDAMENTO).
- `InscricaoService`
  - `create`: **apenas ALUNO**; só permite em projeto com `StatusProjeto.ABERTO`; evita duplicidade (confere via repository + unique constraint).
  - `aprovar/rejeitar`: **apenas ORIENTADOR** e deve ser orientador do projeto.
  - `cancel`: somente dono (aluno da inscrição).
- `ConversaService`
  - Conversa por projeto: valida participação (dono do projeto ou aluno com inscrição APROVADA).
  - Privada: impede conversa consigo mesmo; cria conversa com `participantes`.
  - Mensagens: editar/excluir apenas pelo remetente; notifica participantes/orientador/aluno criador.
- `DocumentoService`
  - Upload/listagem: **somente do próprio usuário** (`usuarioId` do request deve ser o mesmo do token).
  - Valida tamanho (10MB), content-type, extensão e uma “assinatura mínima” (PDF header, ZIP `PK` para docx, OLE2 para doc).
  - Download/preview: valida que caminho está dentro de `uploads/documentos` e existe.
- `FeedbackService`
  - Criar feedback: **somente ALUNO** com inscrição **APROVADA** no projeto; bloqueia avaliar o próprio projeto; impede duplicidade por `uk_feedback_projeto_avaliador`.
- `ProgressoService`
  - Criar/listar por projeto: exige participação (mesma lógica de conversa).
  - Atualizar/remover: autor do registro ou dono do projeto.
- `NotificacaoService`
  - Leitura: apenas dono da notificação.
  - “Marcar todas”: atualiza em loop e salva lista.
- `DashboardService`
  - Agrega contadores consultando repositórios.

## 🗄️ Banco de Dados

### Configuração real (application.properties)
- PostgreSQL (URL via `DB_URL`, com fallback apontando para Supabase).
- `spring.jpa.hibernate.ddl-auto=update` (**sem migrations versionadas**).

### Entidades principais (JPA) e relacionamentos (código real)

- `Usuario` (`usuario`)
  - `tipo` (`TipoUsuario`): define `ROLE_<TIPO>` no Spring Security
  - flags: `ativo`, `tema`, `notificacoesAtivas`
- `Aluno` (`aluno`)
  - `@OneToOne Usuario` (coluna `id_usuario`)
  - `@ManyToOne Curso` (`id_curso`)
- `Orientador` (`orientador`)
  - `@OneToOne Usuario` (`id_usuario`)
- `Curso` (`curso`)
- `AreaPesquisa` (`area_pesquisa`)
  - `@ManyToOne Curso` (`id_curso`)
- `Projeto` (`projeto`)
  - `@ManyToOne AreaPesquisa` (`id_area`)
  - `@ManyToOne Orientador` (`id_orientador`) *(service usa como “dono”, mas o modelo permite muitos projetos por orientador)*
  - `@ManyToOne Aluno` (`id_aluno_criador`) *(idem)*
- `Inscricao` (`inscricao`)
  - `@ManyToOne Aluno` (`id_aluno`) + `@ManyToOne Projeto` (`id_projeto`)
  - unique constraint `uk_inscricao_aluno_projeto (id_aluno, id_projeto)`
- `Conversa` (`conversa`)
  - `@ManyToOne Projeto` (`id_projeto`, **pode ser null** em conversa privada)
  - `@ManyToMany Usuario` via tabela `conversa_participantes`
  - `@OneToMany Mensagem` (lazy)
- `Mensagem` (`mensagem`)
  - `@ManyToOne Conversa` + `@ManyToOne Usuario (remetente)`
- `Documento` (`documento`)
  - `@ManyToOne Usuario`
  - enums: `TipoDocumento`, `StatusDocumento`
- `Feedback` (`feedback`)
  - `@ManyToOne Projeto` + `@ManyToOne Usuario (avaliador)`
  - unique constraint `uk_feedback_projeto_avaliador (id_projeto, id_usuario_avaliador)`
  - `@Check(nota BETWEEN 1 AND 5)`
- `Progresso` (`progresso`)
  - `@ManyToOne Projeto` + `@ManyToOne Usuario (autor)`
  - enum: `TipoProgresso`
- `Notificacao` (`notificacao`)
  - `@ManyToOne Usuario`
  - enum: `TipoNotificacao`

### Queries / Specifications
- `ProjetoRepository` implementa `JpaSpecificationExecutor` e também métodos derivados (`findByAreaCursoNomeContainingIgnoreCase`, etc.).
- `ProjetoService.createSpecification(...)` combina filtros e possui regra especial para `status=ATIVO`.
- `ConversaRepository` usa `@Query` para localizar conversa privada entre dois usuários.

## 🔐 Segurança

### Autenticação (código real)
- JWT via `JwtService` (JJWT), com:
  - `sub = email`
  - claim `tipo = TipoUsuario.name()`
  - expiração: 30 dias
- `JwtAuthFilter`:
  - lê `Authorization: Bearer <token>`,
  - extrai email, carrega `Usuario` do banco, valida token e popula `SecurityContext`.

### Autorização (código real)
- `SecurityConfig` exige autenticação para quase tudo; **não há** uso de `@PreAuthorize`/method security.
- Autorização fina é feita manualmente nos **services** com base em:
  - `TipoUsuario` (ALUNO vs ORIENTADOR),
  - ownership (ex.: editar projeto só se for orientador do projeto ou aluno criador),
  - participação por inscrição APROVADA (conversa/progresso/feedback).

### Validações
- DTOs anotados com `jakarta.validation` e controllers usam `@Valid`.
- Services fazem validações adicionais (ex.: `DocumentoService` valida arquivo e permissões; `ProjetoService` valida status; `InscricaoService` valida tipo do usuário e status do projeto).

## 🔍 Funcionalidades implementadas (confirmadas no código)

- Autenticação: login/register/logout/troca de senha.
- Usuário: perfil `/me`, edição do próprio usuário, preferências, listagem por orientador, soft-delete.
- Projetos: CRUD + listagem com filtros + paginação + “meus projetos”.
- Áreas de pesquisa: `GET /api/areas` (lista `id/nome`).
- Inscrições: CRUD parcial + cancelar + listar por projeto + aprovar/rejeitar.
- Recrutamento: aprova diretamente inscrição de aluno em projeto (`POST /api/projetos/{id}/recrutar`).
- Conversas/mensagens: por projeto e privadas, envio/edição/exclusão de mensagens.
- Feedback: aluno aprovado registra nota/comentário por projeto; listagens por projeto/usuário.
- Progresso: registros por projeto + edição/remoção por autor ou dono.
- Notificações: listar, marcar lida, marcar todas.
- Documentos: upload/listar/remover + download + preview PDF.
- Dashboard: agregação de métricas.

## ⚠️ Funcionalidades incompletas ou divergentes (docs vs código)

### Divergências com `caminhos API TCC.docx` (intenção) vs backend (real)
- DOCX cita `POST /api/usuarios` (cadastrar usuário). **Não existe** no backend; o cadastro real é `POST /api/auth/register` (e só ALUNO).
- DOCX cita `GET /api/projetos/{id}/inscricoes`. Backend real usa `GET /api/inscricoes/projeto/{projetoId}`.
- DOCX cita módulo `GET /api/mensagens` / `GET /api/mensagens/{id}`. Backend real modela mensagens dentro de conversas (`/api/conversas/...`).
- DOCX cita `curriculo` e `historico` do usuário (`/api/usuarios/{id}/curriculo`, `/api/usuarios/{id}/historico`). **Não existe** no backend.
- DOCX cita filtros como `/api/projetos?area=computacao`:
  - Backend aceita `area` como parâmetro, mas **a spec usa igualdade (`cb.equal`)**, não `contains ignore case` (pode divergir de expectativa de “busca por área”).
- DOCX não menciona endpoints que existem no código: `/api/dashboard`, `/api/*/pagina`, `/api/auth/senha`, `/api/documentos/{id}/download`, `/api/documentos/{id}/preview`, etc.

### PDF (`TCC COTIL 2026.pdf`)
- Não foi possível extrair com fidelidade o texto para validar requisitos detalhados. Qualquer validação de detalhes de “visão” além do que está no código foi evitada (Caveman Mode).

## ⚡ Fluxos principais (código real)

### 1) Cadastro/Login
1. `POST /api/auth/register` (somente ALUNO) → retorna `{ token, usuario }`
2. `POST /api/auth/login` → retorna `{ token, usuario }`
3. Frontend armazena token em `localStorage` (`tcc_auth_token`) e passa a enviar `Authorization: Bearer ...`.

### 2) Criar projeto
1. `GET /api/areas` → lista de áreas (id/nome)
2. `POST /api/projetos`:
   - Se usuário é ORIENTADOR: projeto fica vinculado ao orientador.
   - Se usuário é ALUNO: projeto fica vinculado ao aluno criador e uma inscrição APROVADA é criada automaticamente para ele.

### 3) Inscrição em projeto (ALUNO)
1. `POST /api/inscricoes` com `projetoId` (+ `motivacao`)
2. Backend valida: usuário ALUNO, projeto ABERTO, não duplicado.
3. Notifica orientador do projeto (se existir).

### 4) Aprovar/Rejeitar inscrição (ORIENTADOR)
1. `PUT /api/inscricoes/{id}/aprovar` ou `/rejeitar`
2. Backend valida: usuário ORIENTADOR e orientador do projeto.
3. Notifica o aluno.

### 5) Mensagens
1. Abrir conversa:
   - por projeto: `POST /api/conversas` (ou `/api/conversas/projeto/{projetoId}/abrir`)
   - privada: `POST /api/conversas/privada/{outroUsuarioId}`
2. Enviar mensagem: `POST /api/conversas/{id}/mensagem`
3. Editar/excluir: apenas remetente (`PUT/DELETE /api/conversas/mensagem/{mensagemId}`)

### 6) Documentos
1. Upload: `POST /api/documentos/upload` (multipart: `usuarioId`, `tipo`, `arquivo`)
2. Listar: `GET /api/documentos/usuario/{usuarioId}`
3. Download: `GET /api/documentos/{id}/download`
4. Preview (pdf): `GET /api/documentos/{id}/preview`
5. Remover: `DELETE /api/documentos/{id}`

## 🧪 Testes

### O que existe (código real)
- Backend possui testes com `MockMvc` e `Mockito` para controllers e testes de services:
  - `src/test/java/com/example/tcc_backend/controller/*IntegrationTest.java`
  - `src/test/java/com/example/tcc_backend/service/*Test.java`
- Os testes usam `MockMvcBuilders.standaloneSetup(...)` (sem subir contexto completo / sem filtros de segurança).

### O que falta (lacunas observadas)
- Testes end-to-end com Spring context + SecurityFilterChain (garantir 401/403 reais).
- Testes com banco real (ex.: constraints e mapeamentos) — hoje a maioria é mockada.
- Testes de upload com arquivo real (validações de assinatura/size) e de path traversal.

## 🚨 Problemas estruturais (riscos reais observados)

- **Credenciais no repositório:** `application.properties` contém `DB_USERNAME`/`DB_PASSWORD` e `jwt.secret` com default. Isso é risco de segurança (vazamento de segredo).
- **DDL automático:** `spring.jpa.hibernate.ddl-auto=update` em ambiente compartilhado pode gerar drift de schema e erros não rastreáveis.
- **Autorização espalhada:** regras finas estão em vários services (sem policy central). Funciona, mas aumenta risco de inconsistência ao evoluir.
- **Listagens sem paginação por padrão:** há endpoints “lista total” e “/pagina”; consumo incorreto pode causar payload grande.

## 🧠 Decisões arquiteturais (padrões usados no projeto)

- DTOs de request/response para não expor entidade diretamente (embora alguns endpoints possam retornar listas derivadas de entity em services antes de mapear — depende do controller).
- Validação híbrida: `@Valid` em DTO + validações manuais no service.
- Segurança “pragmática”: Spring Security garante autenticação; autorização fina por regras no service.
- Upload em disco local (`uploads/documentos/<usuarioId>`), com caminho persistido no banco.

## 🔗 Relacionamentos internos (dependências entre módulos)

- `SecurityConfig` → `JwtAuthFilter` → `JwtService` + `UsuarioRepository`
- Services centrais dependem de `AuthHelper` (usuário atual) e repositórios:
  - `ProjetoService` → `ProjetoRepository`, `AreaPesquisaRepository`, `InscricaoRepository`, `UsuarioRepository`, `NotificacaoService`
  - `InscricaoService` → `InscricaoRepository`, `ProjetoRepository`, `AlunoRepository`, `NotificacaoService`
  - `ConversaService` → `ConversaRepository`, `MensagemRepository`, `ProjetoRepository`, `InscricaoRepository`, `UsuarioRepository`, `NotificacaoService`
  - `DocumentoService` → `DocumentoRepository`, `UsuarioRepository`
  - `FeedbackService` → `FeedbackRepository`, `ProjetoRepository`, `InscricaoRepository`
  - `ProgressoService` → `ProgressoRepository`, `ProjetoRepository`, `InscricaoRepository`, `NotificacaoService`

