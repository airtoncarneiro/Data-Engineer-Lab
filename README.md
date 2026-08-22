# Data Engineering Work Simulator

> Nome provisório do projeto.

## Visão geral

Este projeto propõe um **simulador de trabalho para Engenharia de Dados**. O objetivo não é ensinar tecnologias do zero, mas oferecer um ambiente no qual pessoas que já estudaram conceitos e ferramentas possam **aplicar o conhecimento em situações próximas do mundo real**.

O participante assume o papel de Engenheiro de Dados de uma empresa fictícia, recebe demandas em formato de tickets, investiga dados e documentação, implementa soluções e submete suas entregas a validações automatizadas.

## Problema

Quem está iniciando em Engenharia de Dados encontra cursos, vídeos e exercícios de sintaxe, mas normalmente não possui acesso a:

- ambiente corporativo realista;
- demandas de negócio contextualizadas;
- bases de dados relacionadas entre si;
- código legado e documentação incompleta;
- pipelines e dependências;
- fluxo Git/PR/CI;
- feedback sobre uma solução entregue.

O projeto busca preencher essa lacuna entre **conhecer uma tecnologia** e **saber utilizá-la para resolver problemas de Engenharia de Dados**.

## Experiência proposta

O participante deverá:

1. fazer fork do repositório principal;
2. preparar o ambiente local;
3. executar o onboarding da empresa fictícia;
4. receber e selecionar tickets disponíveis;
5. investigar contexto, dados e regras de negócio;
6. implementar a solução;
7. abrir uma Pull Request no próprio fork;
8. receber validação automática pelo CI;
9. corrigir eventuais problemas;
10. concluir o ticket e avançar na jornada.

## MVP

A primeira versão deverá validar a experiência principal com o menor escopo possível:

- PostgreSQL em container;
- base de dados previamente populada;
- onboarding;
- aproximadamente 10 tickets SQL progressivos;
- respostas implementadas pelo participante;
- Pull Requests no fork do participante;
- GitHub Actions para validação automática;
- sem backend próprio;
- sem ranking global obrigatório.

## Evolução prevista

Após validar o MVP, o simulador poderá incorporar:

- Python;
- modelagem de dados;
- ETL/ELT;
- Apache Airflow;
- qualidade de dados;
- observabilidade;
- Data Lake/Lakehouse;
- cloud;
- incidentes e troubleshooting;
- performance e otimização;
- CI/CD e IaC;
- agentes de IA para geração, revisão e manutenção de desafios.

## Documentação

- [Visão do produto](docs/VISION.md)
- [Discovery](docs/DISCOVERY.md)
- [Princípios do projeto](docs/PRINCIPLES.md)
- [Arquitetura inicial](docs/ARCHITECTURE.md)
- [Roadmap](docs/ROADMAP.md)
- [Backlog inicial](docs/BACKLOG.md)

## Status

**Discovery / definição do MVP.**

As decisões registradas nesta documentação funcionam como fonte inicial da verdade e deverão orientar as próximas etapas do projeto.
