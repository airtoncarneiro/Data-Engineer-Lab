# Roadmap Inicial

O roadmap descreve hipóteses de evolução e é a fonte única para a evolução pós-MVP. Não representa compromisso com todas as funcionalidades.

A progressão do laboratório deve considerar três dimensões complementares:

- **complexidade tecnológica**: SQL, modelagem, Python, Airflow, plataforma, cloud e operação;
- **natureza do trabalho**: construir, modificar, corrigir, refatorar, otimizar, investigar e operar/troubleshooting;
- **proficiência demonstrada**: evidências acumuladas sobre competências técnicas e profissionais para selecionar desafios adequados ao estágio atual.

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
- incluir tipo, competências-alvo, dificuldade estimada e pré-requisitos no modelo de ticket;
- criar Docker Compose;
- criar PostgreSQL inicial;
- definir mecanismo de reset do ambiente.

## Fase 1 — MVP SQL

Objetivo: validar a experiência principal e o ciclo adaptativo mínimo: diagnóstico, desafio, evidência, atualização do perfil e seleção do próximo desafio.

Entregas:

- ticket 000 de onboarding;
- coleta do objetivo profissional antes do diagnóstico;
- PROBE SQL curto, discriminativo e adaptativo, cobrindo escrita e compreensão conceitual;
- PROBE híbrido, prioritariamente conversacional e com execução real quando necessária para aumentar a confiança;
- Learner Model mínimo e persistente, genérico por competência, com `mastery`, `confidence` e quantidade de evidências;
- separação entre competências técnicas e profissionais, sendo as profissionais inferidas principalmente durante os tickets;
- catálogo SQL suficiente para compor jornadas distintas;
- jornada individual de aproximadamente 10 desafios, usando o número como referência de duração e não como critério de conclusão;
- seleção do próximo desafio por mecanismo híbrido: regras auditáveis definem prioridades/restrições e IA pode apoiar seleção ou construção dentro desses limites;
- competências-alvo mantidas como metadados internos durante a execução do ticket;
- registro de múltiplas evidências por competência e verificação de transferência em contextos diferentes quando aplicável;
- distinção entre entrega tecnicamente concluída e domínio demonstrado;
- perguntas pós-entrega quando úteis para verificar compreensão, decisões e trade-offs;
- pesquisa, documentação e IA permitidas ao participante;
- registro do nível de assistência direcionada utilizado para ponderar a força das evidências;
- tempo de execução registrado apenas como telemetria no MVP;
- possibilidade de `skip` sem inferir automaticamente falta de competência;
- sinalização de desafio muito fácil como autoavaliação, a ser confirmada por evidências posteriores;
- em desafios difíceis, oferta de pistas, decomposição ou Learning Resources antes de troca, conforme escolha do participante;
- pistas-base validadas com adaptação controlada por IA;
- PROBE curto de recalibração quando solicitado pelo participante ou quando o Lab detectar má calibração persistente, sempre após o ticket corrente;
- persistência da jornada e retomada do ponto anterior;
- uma jornada ativa por vez;
- conclusão baseada em evidências suficientes de evolução e transferência, não em quantidade fixa de tickets;
- extensão adaptativa opcional para lacunas remanescentes;
- perfil final qualitativo por competência, mostrando evolução entre entrada e saída sem expor obrigatoriamente scores internos;
- recomendação da próxima jornada com base no perfil, pré-requisitos, lacunas e objetivo profissional;
- área padronizada para soluções;
- Pull Request template;
- testes automáticos e GitHub Actions;
- documentação para fork e sincronização com upstream;
- geração assistida por IA de desafios candidatos quando o catálogo não cobrir adequadamente a necessidade;
- lifecycle mínimo de desafios gerados: `candidate -> validated -> trialed -> published`;
- validações automáticas antes do primeiro uso; revisão humana obrigatória apenas quando o risco, subjetividade ou baixa confiança impedirem validação automática suficiente;
- número mínimo de execuções reais antes da promoção de um candidato a `published`, com valor exato definido durante implementação;
- telemetria contínua de tickets publicados para sinalizar necessidade de revisão;
- feedback por IA sobre entregas quando viável, apoiado por resultados determinísticos;
- teste com primeiros usuários.

A adaptação do MVP deve permanecer simples e auditável. O Learner Model mínimo não implica Skill Graph completo, Progression Agent autônomo ou inferência irrestrita por LLM.

Critério de saída:

Participantes externos com níveis iniciais distintos conseguem executar onboarding, passar por um PROBE curto, receber desafios adequados, evoluir com base em evidências e interpretar feedback sem intervenção constante do mantenedor. A jornada demonstra adaptação real a diferentes perfis e consegue incorporar novos desafios ao catálogo por um processo controlado de qualificação.

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
- cenários brownfield;
- expansão do catálogo para melhorar cobertura de competências e faixas de proficiência;
- melhoria dos critérios de qualificação de desafios gerados;
- desafios de transferência que exercitem princípios já demonstrados em contextos diferentes.

## Fase 3 — Python e ETL/ELT

Possibilidades:

- PROBE técnico próprio da jornada, reutilizando evidências existentes no Learner Model quando aplicável;
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

Objetivo: sofisticar o ciclo adaptativo validado no MVP, sem alterar seus princípios fundamentais.

Possibilidades:

- Learner Model enriquecido com misconceptions, recência e diversidade de contextos;
- Skill Graph e dependências explícitas entre competências;
- inferência contínua mais sofisticada a partir do histórico;
- Progression Agent;
- revisão espaçada e testes sistemáticos de retenção;
- geração altamente individualizada de tickets e datasets;
- agente de testes;
- AI Code Reviewer avançado;
- agente simulando stakeholder;
- avaliação assistida por LLM para critérios subjetivos;
- arquitetura multiagente;
- políticas de promoção e despublicação de desafios baseadas em telemetria acumulada.

### AI Code Reviewer

O AI Code Reviewer deve complementar, e não substituir, as validações determinísticas.

Responsabilidades possíveis:

- comentar legibilidade e manutenibilidade;
- levantar edge cases não cobertos explicitamente;
- questionar decisões técnicas e trade-offs;
- apontar complexidade desnecessária;
- estimular justificativa técnica do participante;
- utilizar evidências produzidas pelo CI como contexto para o feedback.

Critérios objetivos que possam ser testados devem continuar sendo validados por testes e verificações determinísticas.

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

O diagrama abaixo representa uma possível sofisticação do mecanismo validado no MVP, não uma arquitetura aprovada nem um compromisso de implementação.

```text
Learner Model / Skill Graph
          │
          ▼
   Progression Agent
          │
          ▼
    Challenge Engine
          │
          ▼
        Ticket
          │
          ▼
    Participante
          │
          ▼
Validação determinística + AI Review
          │
          ▼
      Evidências
          │
          └──────────► Learner Model
```
