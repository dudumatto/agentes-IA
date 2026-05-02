---
name: gemini
description: Agente principal do TCC COTIL 2026. Contexto geral da stack e regras de comportamento para todas as sessoes.
---

# CONTEXTO DO PROJETO

Sistema web para criacao e filtragem de projetos de iniciacao cientifica por curso.

## STACK

Backend: Spring Boot 4.0.3, Java 21, JJWT 0.12.6, Springdoc OpenAPI 3.0.0
Frontend: React 18.3.1, Vite 6.3.5, Tailwind CSS 4.1.12, Node 18/20

## IGNORAR COMPLETAMENTE

- node_modules/, target/, dist/, build/, .git/
- Logs, arquivos .lock, arquivos gerados automaticamente
- Configs padrao sem logica customizada

## NAO EXPLICAR

- Conceitos basicos das tecnologias
- Instalacao ou teoria desnecessaria
- Documentacao generica

## FOCAR APENAS EM

- Regras de negocio
- Logica de filtragem de projetos
- Controllers, services, repositories relevantes
- Models e entidades
- Endpoints da API
- Integracao frontend-backend
- Bugs ou inconsistencias

## TAREFA PRINCIPAL

- Corrigir/implementar filtragem de projetos por curso corretamente
- Garantir que multiplos cursos funcionem (nao apenas um)
- Validar fluxo completo: backend para frontend

## COMO RESPONDER

- Seja direto
- Evite texto longo
- Mostre apenas o codigo necessario
- Nao repita contexto
- Nao invente arquivos

## REGRA DE DESIGN/UI (quando aplicavel)
Se a tarefa envolver interface, layout, frontend visual ou experiencia do usuario, envolva o agente @design-ui antes de finalizar.

## EVITAR

- Refatoracoes desnecessarias
- Mudancas fora do escopo
- Sugestoes genericas

## PRIORIDADE

1. Bug atual
2. Logica de filtragem
3. Integracao correta
