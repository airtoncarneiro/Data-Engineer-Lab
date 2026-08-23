# Backlog Inicial

Backlog do MVP SQL organizado para validar primeiro o ciclo adaptativo ponta a ponta. A ordem poderá mudar conforme evidências de implementação, mas componentes de plataforma não devem ser antecipados.

## Decisões técnicas já concluídas

As decisões abaixo estão aprovadas para o MVP e devem orientar a implementação:

- [x] Python 3.11.
- [x] FastAPI + Jinja2 + HTMX para a Web UI local.
- [x] CodeMirror e assets frontend servidos localmente pelo FastAPI.
- [x] CSS próprio mínimo, sem framework frontend ou build Node.js.
- [x] PostgreSQL 16 via Docker Compose.
- [x] Aplicação Python executada localmente via `uv` no primeiro momento.
- [x] PostgreSQL único com schemas `lab` e `company`.
- [x] SQLAlchemy 2.x + psycopg 3 para persistência interna.
- [x] Alembic para o schema `lab` e scripts SQL versionados para `company`.
- [x] `uv` + `pyproject.toml` para ambiente, dependências e configuração das ferramentas.
- [x] Arquitetura `domain` / `application` / `infrastructure` com Web UI separada.
- [x] `Protocol` apenas nas fronteiras externas relevantes.
- [x] Entidades de domínio separadas dos models SQLAlchemy.
- [x] `dataclasses` no domínio e Pydantic para DTOs/contratos.
- [x] Unit of Work mínima via `Protocol`, controlando transações por caso de uso.
- [x] pytest + fakes in-memory + testes de integração específicos.
- [x] Ruff + mypy.
- [x] `pydantic-settings`, `.env`, `.env.example` e feature flags explícitas.
- [x] Logging padrão do Python, `request_id`, `/health` e `/ready`.
- [x] GitHub Actions para CI do próprio produto.
- [x] Tickets Markdown com YAML front matter como fonte de verdade.
- [x] Catálogo central de competências versionado em `skills/catalog.yaml`.
- [x] Catálogos carregados e validados no startup, read-only em runtime.
- [x] PROBE versionado fora do código com tipos `multiple_choice`, `free_text` e `sql`.
- [x] Avaliação híbrida por tipo, priorizando validação determinística.
- [x] Editor SQL direto na Web UI no primeiro vertical slice.
- [x] Execução inicial somente leitura, com usuário PostgreSQL restrito ao schema `company`.
- [x] Validação por resultado e query de referência em `expected.sql` quando aplicável.
- [x] Provider de IA atrás de `AIProvider`, usando SDK oficial OpenAI com `base_url` configurável.
- [x] IA opcional e degradação graciosa quando indisponível.
- [x] Um único perfil local, sem login, com UUID interno.
- [x] Várias jornadas históricas, mas no máximo uma ativa.
- [x] Estados explícitos da jornada via `Enum` e regras de domínio.
- [x] `mastery` e `confidence` como value objects e `NUMERIC` no PostgreSQL.
- [x] Learner Model atualizado por regras determinísticas e auditáveis.
- [x] Evidências persistidas com componentes do cálculo e histórico separado do Learner Model.
- [x] Telemetria em tabela própria com `event_version` e `payload JSONB`.
- [x] Repositório privado durante a validação da hipótese comercial, sem licença pública neste estágio.

## Épico 1 — Fundação do produto

- [ ] Definir nome e segmento da empresa fictícia.
- [ ] Definir narrativa mínima da empresa.
- [ ] Definir departamentos que solicitarão demandas.
- [ ] Definir sistemas fonte iniciais.
- [ ] Criar glossário de negócio.
- [ ] Criar regras de negócio iniciais.
- [ ] Consolidar convenções finais de tickets e metadados.

## Épico 2 — PostgreSQL do laboratório

- [ ] Definir domínio inicial adequado aos tickets SQL.
- [ ] Modelar o schema `company`.
- [ ] Modelar o schema `lab` e suas constraints.
- [ ] Criar migrations Alembic do schema `lab`.
- [ ] Criar scripts de init/seed versionados do schema `company`.
- [ ] Criar massa de dados determinística.
- [ ] Incluir casos de borda necessários aos desafios.
- [ ] Criar processo simples de reset do schema `company`.
- [ ] Criar dicionário de dados.
- [ ] Criar usuários/roles separados para aplicação e execução do participante.
- [ ] Configurar `search_path`, read-only e `statement_timeout` para execução do participante.

## Épico 3 — Ambiente local

- [ ] Criar `docker-compose.yml` com PostgreSQL 16.
- [ ] Criar `pyproject.toml` e `uv.lock`.
- [ ] Criar `.env.example`.
- [ ] Criar `Makefile` com comandos operacionais mínimos.
- [ ] Criar configuração central via `pydantic-settings`.
- [ ] Criar `/health` e `/ready`.
- [ ] Criar configuração de logging e `request_id`.
- [ ] Validar execução em ambiente limpo.
- [ ] Garantir que o ciclo determinístico básico não dependa obrigatoriamente de serviços externos.

## Épico 4 — Lab Engine mínimo

- [x] Definir estrutura inicial das camadas e diretórios.
- [x] Definir estratégia de portas/repositories e Unit of Work.
- [x] Definir modelo conceitual de estado explícito da jornada.
- [ ] Implementar entidades e value objects do domínio.
- [ ] Implementar contratos internos entre Web UI e application.
- [ ] Implementar modelo persistente da jornada.
- [ ] Implementar modelo mínimo de Learner Model por competência.
- [ ] Implementar registro de evidências e histórico do Learner Model.
- [ ] Implementar telemetria persistente.
- [ ] Implementar persistência e retomada da jornada.
- [ ] Manter regras pedagógicas fora da camada de UI.

## Épico 5 — PROBE SQL

- [ ] Definir contrato Pydantic definitivo das questões do PROBE.
- [ ] Criar estrutura `probe/sql/` e loaders.
- [ ] Criar conjunto inicial de questões discriminativas.
- [ ] Implementar `multiple_choice`, `free_text` e `sql`.
- [ ] Implementar seleção adaptativa curta, usando aproximadamente cinco perguntas quando suficientes.
- [ ] Cobrir escrita e compreensão conceitual.
- [ ] Executar questões SQL no PostgreSQL quando necessário.
- [ ] Implementar rubrica de `free_text` com IA opcional.
- [ ] Persistir pergunta, resposta e evidências derivadas.
- [ ] Converter respostas em evidências para o Learner Model.
- [ ] Produzir resultado qualitativo para o participante.

## Épico 6 — Framework de tickets

- [ ] Definir contrato Pydantic definitivo do YAML front matter.
- [x] Definir Markdown + YAML front matter como formato do ticket.
- [x] Definir convenção de IDs numéricos de três dígitos.
- [x] Definir catálogo central de skills com IDs estáveis.
- [ ] Definir níveis de dificuldade.
- [ ] Definir pré-requisitos e dependências.
- [ ] Definir critérios de aceite verificáveis.
- [x] Definir `expected.sql` separado quando houver query de referência.
- [x] Definir validação híbrida: declarativa + Python quando necessário.
- [ ] Definir contrato para Learning Resources relacionados.
- [ ] Implementar loader e validação fail-fast do catálogo no startup.

## Épico 7 — Validador SQL local

- [x] Definir editor SQL direto na Web UI para o vertical slice.
- [x] Restringir o vertical slice inicial a `SELECT`.
- [x] Definir comparação por resultado, não por texto SQL.
- [ ] Implementar executor com usuário restrito do PostgreSQL.
- [ ] Definir contrato final de normalização de result sets.
- [ ] Tratar colunas, valores, tipos, `NULL` e ordenação configurável.
- [ ] Implementar `statement_timeout` e tratamento de erros.
- [ ] Criar framework declarativo de validação por ticket.
- [ ] Criar suporte a validadores Python adicionais.
- [ ] Produzir mensagens de erro úteis.
- [ ] Produzir evidências objetivas consumíveis pelo Lab Engine.

## Épico 8 — Challenge Selector e Evidence Engine

- [ ] Definir regras auditáveis mínimas para seleção do próximo desafio.
- [ ] Considerar objetivo profissional, pré-requisitos, mastery, confidence e evidências necessárias.
- [ ] Definir fórmula exata do `LearnerModelUpdater`.
- [ ] Implementar atualização do Learner Model a partir das evidências.
- [ ] Persistir evidência, estado corrente e histórico na mesma transação.
- [ ] Diferenciar entrega tecnicamente concluída de domínio demonstrado.
- [ ] Implementar categorias/pesos de força, valência e assistência.
- [ ] Implementar `skip` sem evidência automática negativa.
- [ ] Implementar sinalização de desafio muito fácil/difícil.
- [ ] Definir gatilhos mínimos de recalibração.

## Épico 9 — Web UI local

- [x] Escolher FastAPI + Jinja2 + HTMX.
- [x] Escolher CodeMirror local para edição SQL.
- [x] Definir templates e routers organizados por feature.
- [ ] Criar base visual e CSS mínimo.
- [ ] Criar inicialização/retomada da jornada.
- [ ] Coletar objetivo profissional estruturado + contexto opcional.
- [ ] Implementar experiência do PROBE.
- [ ] Exibir ticket corrente.
- [ ] Implementar editor e submissão SQL.
- [ ] Executar validação e exibir feedback.
- [ ] Permitir assistência e `skip`.
- [ ] Exibir progresso qualitativo quando aplicável.
- [ ] Implementar handlers para exceções tipadas.
- [ ] Evitar duplicação de lógica da application/domain na interface.

## Épico 10 — Vertical slice adaptativo

Objetivo: provar o núcleo do produto antes de expandir o catálogo.

- [ ] Iniciar o Lab localmente.
- [ ] Registrar objetivo profissional.
- [ ] Executar o PROBE SQL.
- [ ] Criar Learner Model persistente.
- [ ] Selecionar um ticket compatível.
- [ ] Receber uma solução SQL pelo editor Web.
- [ ] Validar a solução localmente.
- [ ] Registrar evidências.
- [ ] Atualizar o Learner Model e seu histórico.
- [ ] Selecionar o próximo ticket com base no estado atualizado.
- [ ] Retomar a jornada após reinício da aplicação.

Esse épico deve ser concluído antes de ampliar significativamente o catálogo ou introduzir componentes avançados de IA.

## Épico 11 — Catálogo SQL do MVP

Criar catálogo suficiente para compor jornadas distintas de aproximadamente 10 desafios, cobrindo progressivamente combinações de:

- [ ] filtros e regras de negócio;
- [ ] joins;
- [ ] agregações;
- [ ] subqueries/CTEs;
- [ ] tratamento de datas;
- [ ] window functions;
- [ ] qualidade/inconsistências;
- [ ] análise investigativa;
- [ ] performance básica;
- [ ] desafios integradores e de transferência.

Os tickets não devem corresponder necessariamente 1:1 a esses tópicos. A demanda de negócio deve determinar quais técnicas serão necessárias.

## Épico 12 — Assistência e Learning Resources

- [ ] Definir pistas-base validadas.
- [ ] Implementar níveis graduais de assistência.
- [ ] Registrar assistência direcionada utilizada.
- [ ] Associar Learning Resources reutilizáveis aos conceitos relevantes.
- [ ] Permitir decomposição de desafios difíceis antes da troca, conforme escolha do participante.
- [ ] Preservar pesquisa, documentação e IA como ferramentas profissionais permitidas.

## Épico 13 — Geração assistida e catálogo evolutivo

- [ ] Definir contrato estruturado para geração de desafios.
- [ ] Gerar candidato quando o catálogo não cobrir adequadamente a necessidade.
- [ ] Implementar lifecycle `candidate -> validated -> trialed -> published`.
- [ ] Criar validações automáticas antes do primeiro uso.
- [ ] Definir critérios para revisão humana quando necessária.
- [ ] Definir número mínimo de execuções reais antes de promoção a `published`.
- [ ] Registrar telemetria dos desafios publicados.
- [ ] Sinalizar ambiguidades, falhas ou dificuldade mal calibrada para revisão.

## Épico 14 — Feedback e IA

- [ ] Implementar `AIProvider` em `application/ports`.
- [ ] Implementar provider compatível com OpenAI usando SDK oficial e `base_url` configurável.
- [ ] Implementar `AI_ENABLED` e validação condicional de configuração.
- [ ] Integrar feedback por IA sobre evidências determinísticas quando viável.
- [ ] Evitar uso do LLM como autoridade única para critérios verificáveis.
- [ ] Implementar perguntas pós-entrega quando úteis para compreensão e trade-offs.
- [ ] Garantir degradação graciosa quando o recurso de IA estiver indisponível.

## Épico 15 — Qualidade e CI

- [ ] Configurar Ruff.
- [ ] Configurar mypy.
- [ ] Configurar pytest.
- [ ] Criar fakes in-memory para testes unitários.
- [ ] Criar testes de integração PostgreSQL onde necessário.
- [ ] Criar GitHub Actions com `uv sync`, Ruff, mypy e pytest.

## Épico 16 — Validação do produto

- [ ] Selecionar pequeno grupo de usuários iniciais.
- [ ] Medir taxa de onboarding concluído sem ajuda.
- [ ] Medir tempo até a primeira entrega validada.
- [ ] Medir taxa de conclusão e abandono de tickets.
- [ ] Registrar número de intervenções do mantenedor.
- [ ] Avaliar capacidade de interpretar feedback.
- [ ] Coletar percepção de realismo.
- [ ] Avaliar qualidade da adaptação para níveis iniciais distintos.
- [ ] Verificar retomada da jornada e persistência.
- [ ] Decidir se o formato merece expansão.

## Pendências de definição para o primeiro vertical slice

Estas decisões devem ser fechadas durante a implementação da fundação, sem reabrir a arquitetura-base:

- [ ] modelo completo das tabelas/constraints do schema `lab`;
- [ ] contrato Pydantic definitivo dos tickets;
- [ ] contrato Pydantic definitivo das questões do PROBE;
- [ ] conjunto inicial de skills;
- [ ] fórmula determinística exata de `mastery` e `confidence`;
- [ ] regras mínimas do Challenge Selector;
- [ ] campos e transições finais de `journey_ticket`;
- [ ] contrato final de normalização e erros do validador SQL;
- [ ] empresa fictícia, domínio inicial e dataset;
- [ ] composição do primeiro PROBE e dos primeiros tickets do vertical slice.

## Fora do fluxo obrigatório do MVP

Os itens abaixo podem ser usados no desenvolvimento do produto, mas não fazem parte do fluxo operacional obrigatório do participante:

- fork do repositório;
- branch por ticket;
- Pull Request como entrega;
- GitHub Actions como validador da solução do aluno;
- sincronização manual de fork com `upstream`.

O GitHub continua sendo utilizado para desenvolvimento, versionamento, distribuição e CI do produto.

## Depois do MVP

- [ ] Definir próxima trilha com base no feedback.
- [ ] Avaliar Python/ETL.
- [ ] Avaliar Airflow.
- [ ] Avaliar gamificação.
- [ ] Avaliar backend/API e persistência centralizada.
- [ ] Avaliar autenticação e modelo comercial.
- [ ] Avaliar execução remota e testes privados.
- [ ] Evoluir agentes para geração, progressão e revisão de desafios.
