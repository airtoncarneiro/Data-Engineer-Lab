# Roadmap Inicial

O roadmap descreve hipóteses de evolução e é a fonte única para a evolução pós-MVP. Não representa compromisso com todas as funcionalidades.

A progressão do laboratório deve considerar duas dimensões complementares:

- **complexidade tecnológica**: SQL, modelagem, Python, Airflow, plataforma, cloud e operação;
- **natureza do trabalho**: construir, modificar, corrigir, refatorar, otimizar, investigar e operar/troubleshooting.

Essas dimensões podem ser combinadas ao longo das fases. A introdução de cenários brownfield não constitui uma fase isolada: é uma característica transversal dos tickets.

## Fase 0 — Fundação

Objetivo: transformar o Discovery em um repositório executável.

Entregas:

- definir nome provisório;
- definir empresa fictícia;
- criar repositório;
- estruturar documentação;
- definir convenções de tickets;
- definir schema mínimo para tickets estruturados;
- incluir tipo de ticket como metadado do modelo;
- criar Docker Compose;
- criar PostgreSQL inicial;
- definir mecanismo de reset do ambiente.

## Fase 1 — MVP SQL

Objetivo: validar a experiência principal e a geração assistida de desafios.

Entregas:

- ticket 000 de onboarding;
- aproximadamente 10 tickets SQL;
- progressão de dificuldade;
- área padronizada para soluções;
- Pull Request template;
- testes automáticos;
- GitHub Actions;
- documentação para fork e sincronização com upstream;
- gerador assistido por IA para propostas estruturadas de tickets;
- validação humana/editorial antes da publicação de tickets gerados;
- estrutura mínima para registrar evidências objetivas das entregas;
- feedback por IA sobre entregas quando viável, apoiado por resultados determinísticos;
- possibilidade de incluir pontualmente tickets não greenfield quando agregarem valor ao MVP, sem exigir cobertura de toda a taxonomia;
- teste com primeiros usuários.

Critério de saída:

Participantes externos conseguem executar onboarding, resolver tickets e interpretar feedback do CI sem intervenção constante do mantenedor. O projeto também consegue gerar propostas de tickets por IA que respeitam as convenções pedagógicas e técnicas antes de revisão/publicação.

## Fase 2 — SQL avançado e modelagem

Possibilidades:

- queries analíticas;
- window functions;
- performance;
- índices;
- análise de planos;
- modelagem dimensional;
- problemas de qualidade;
- mudanças de regra de negócio;
- tickets `bugfix`, `refactoring`, `performance` e `legacy` aplicados a SQL;
- cenários brownfield com queries existentes cujo comportamento precisa ser compreendido e preservado;
- variações de desafios geradas a partir de competências e dificuldade informadas.

## Fase 3 — Python e ETL/ELT

Possibilidades:

- ingestão de arquivos;
- transformação;
- idempotência;
- tratamento de erros;
- logging;
- testes;
- incrementalidade;
- manutenção e refatoração de pipelines existentes;
- investigação de comportamento legado e dívida técnica plausível.

## Fase 4 — Orquestração

Introdução de Apache Airflow e problemas envolvendo:

- DAGs;
- dependências;
- retries;
- backfill;
- parametrização;
- falhas parciais;
- observabilidade;
- pipelines incrementais;
- correção e evolução de DAGs existentes;
- troubleshooting de fluxos herdados.

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

A natureza do trabalho passa a enfatizar investigação e operação. Tickets podem incluir:

- pipeline quebrado;
- dados incorretos;
- SLA violado;
- query lenta;
- duplicidade;
- schema drift;
- reprocessamento;
- investigação de causa raiz;
- manutenção de componentes legados;
- correções com necessidade explícita de preservar comportamento e evitar regressões.

## Fase 7 — IA avançada e adaptação

Objetivo: evoluir da geração assistida do MVP para personalização e automação baseadas em evidências.

Possibilidades:

- agente gerador de datasets;
- agente de testes;
- AI Code Reviewer;
- agente simulando stakeholder;
- avaliação assistida por LLM para critérios subjetivos;
- Skill Graph;
- inferência de competências a partir do histórico;
- seleção adaptativa da próxima competência;
- Progression Agent;
- geração de variações individualizadas de tickets;
- arquitetura multiagente.

### AI Code Reviewer

O AI Code Reviewer deve complementar, e não substituir, as validações determinísticas.

Responsabilidades possíveis:

- comentar legibilidade e manutenibilidade;
- levantar edge cases não cobertos explicitamente;
- questionar decisões técnicas e trade-offs;
- apontar complexidade desnecessária;
- estimular justificativa técnica do participante;
- utilizar evidências produzidas pelo CI como contexto para o feedback.

Critérios objetivos que possam ser testados devem continuar sendo validados por testes e verificações determinísticas. O revisor por IA não deve atuar como autoridade única de aprovação da entrega.

A publicação totalmente autônoma de desafios deverá ser considerada apenas se houver mecanismos suficientes de validação, observabilidade e governança.

## Fase 8 — Plataforma opcional

Somente se houver necessidade comprovada:

- backend;
- autenticação;
- perfil do participante;
- histórico centralizado;
- evidências de competência centralizadas;
- badges;
- ranking;
- portal web;
- métricas de aprendizagem/prática;
- visualização de progressão e competências.

A visão de longo prazo poderá convergir para uma **plataforma adaptativa de treinamento de Engenharia de Dados baseada em evidências de competência**, mantendo o simulador profissional como núcleo da experiência.

## Direção arquitetural pós-MVP (hipótese)

O diagrama abaixo representa uma possível direção conceitual para evolução após a validação do MVP. É uma hipótese de arquitetura, não uma arquitetura aprovada nem um compromisso de implementação.

```text
Skill Profile / Skill Graph
          │
          ▼
   Progression Agent
          │
          ▼
    Task Generator
          │
          ▼
        Ticket
          │
          ▼
    Participante
          │
          ▼
Validação determinística + AI Code Review
          │
          ▼
      Evidências
          │
          └──────────► Skill Profile
```
