# Roadmap Inicial

O roadmap descreve hipóteses de evolução. Não representa compromisso com todas as funcionalidades.

## Fase 0 — Fundação

Objetivo: transformar o Discovery em um repositório executável.

Entregas:

- definir nome provisório;
- definir empresa fictícia;
- criar repositório;
- estruturar documentação;
- definir convenções de tickets;
- criar Docker Compose;
- criar PostgreSQL inicial;
- definir mecanismo de reset do ambiente.

## Fase 1 — MVP SQL

Objetivo: validar a experiência principal.

Entregas:

- ticket 000 de onboarding;
- aproximadamente 10 tickets SQL;
- progressão de dificuldade;
- área padronizada para soluções;
- Pull Request template;
- testes automáticos;
- GitHub Actions;
- documentação para fork e sincronização com upstream;
- teste com primeiros usuários.

Critério de saída:

Participantes externos conseguem executar onboarding, resolver tickets e interpretar feedback do CI sem intervenção constante do mantenedor.

## Fase 2 — SQL avançado e modelagem

Possibilidades:

- queries analíticas;
- window functions;
- performance;
- índices;
- análise de planos;
- modelagem dimensional;
- problemas de qualidade;
- mudanças de regra de negócio.

## Fase 3 — Python e ETL/ELT

Possibilidades:

- ingestão de arquivos;
- transformação;
- idempotência;
- tratamento de erros;
- logging;
- testes;
- incrementalidade.

## Fase 4 — Orquestração

Introdução de Apache Airflow e problemas envolvendo:

- DAGs;
- dependências;
- retries;
- backfill;
- parametrização;
- falhas parciais;
- observabilidade;
- pipelines incrementais.

## Fase 5 — Plataforma de dados

Possibilidades:

- object storage local;
- Data Lake/Lakehouse;
- formatos colunares;
- particionamento;
- catálogo;
- qualidade;
- lineage;
- governança.

## Fase 6 — Operação e incidentes

Tickets deixam de ser apenas novas implementações e passam a incluir:

- pipeline quebrado;
- dados incorretos;
- SLA violado;
- query lenta;
- duplicidade;
- schema drift;
- reprocessamento;
- investigação de causa raiz.

## Fase 7 — IA e geração assistida de conteúdo

Objetivo: aumentar a capacidade de criação e manutenção de desafios.

Possibilidades:

- agente gerador de tickets;
- agente gerador de datasets;
- agente de testes;
- agente revisor;
- agente simulando stakeholder;
- geração de variações de tickets;
- avaliação assistida por LLM para critérios subjetivos.

## Fase 8 — Plataforma opcional

Somente se houver necessidade comprovada:

- backend;
- autenticação;
- perfil do participante;
- histórico centralizado;
- badges;
- ranking;
- portal web;
- métricas de aprendizagem/prática.
