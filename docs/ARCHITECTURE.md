# Arquitetura Inicial

## Objetivo

Definir a arquitetura mínima aprovada para o MVP local do simulador, suficiente para iniciar a implementação sem antecipar componentes de plataforma.

## Decisão arquitetural do MVP

O MVP será executado localmente pelo participante e terá como interface principal uma Web UI local.

A arquitetura aprovada é:

```text
Browser
   │
   ▼
FastAPI + Jinja2 + HTMX
   │
   ▼
Application
   │
   ▼
Domain
   │
   ├──────────────► Infrastructure / PostgreSQL
   │                  ├── schema lab
   │                  └── schema company
   │
   └──────────────► Infrastructure / AIProvider
                      └── API compatível com OpenAI, quando habilitada
```

O GitHub permanece como repositório de desenvolvimento, versionamento e distribuição do produto, mas não é parte obrigatória do fluxo operacional do participante no MVP.

Fork, branch, Pull Request e GitHub Actions podem ser utilizados no desenvolvimento do projeto, mas não são requisitos para o aluno executar uma jornada, enviar uma solução ou receber validação.

## Stack mínima aprovada

### Runtime e Web UI

- Python 3.11;
- FastAPI;
- Jinja2;
- HTMX;
- CodeMirror servido localmente;
- CSS próprio mínimo;
- assets em `app/web/static/`;
- templates e routers organizados por feature.

Não haverá Node.js, bundler ou framework SPA no MVP inicial.

### Dependências e configuração

- `uv` para dependências e ambiente virtual;
- `pyproject.toml` como arquivo central de metadados e configuração;
- Pydantic para DTOs e contratos;
- `pydantic-settings` para configuração;
- `.env` local ignorado pelo Git;
- `.env.example` versionado;
- `APP_ENV` com ambientes `development`, `test` e `production-like`;
- feature flags explícitas, começando por `AI_ENABLED`;
- fail-fast no startup para configurações obrigatórias.

### Persistência

- PostgreSQL 16 via Docker Compose;
- aplicação Python executada localmente via `uv` no primeiro momento;
- SQLAlchemy 2.x;
- psycopg 3;
- Alembic para migrations do schema `lab`;
- scripts SQL versionados para criação e seed do schema `company`.

A mesma instância PostgreSQL será usada com separação lógica:

```text
PostgreSQL
├── lab
│   └── persistência interna da aplicação
└── company
    └── dados técnicos usados nos desafios
```

### Qualidade

- pytest;
- Ruff para lint e format;
- mypy com configuração moderada;
- GitHub Actions para CI do próprio produto;
- `Makefile` simples para comandos operacionais.

## Estrutura arquitetural do código

A aplicação adotará separação explícita entre `domain`, `application` e `infrastructure`, sem adotar uma Clean Architecture cerimonial.

```text
web
 ↓
application
 ↓
domain

infrastructure
 ↑
application
```

Regras:

- `domain` não conhece FastAPI, SQLAlchemy, PostgreSQL ou SDKs externos;
- `application` coordena casos de uso e define portas necessárias;
- `infrastructure` implementa persistência, loaders, validadores técnicos e integrações externas;
- `web` contém apenas apresentação, entrada HTTP e tradução de erros para a UI;
- lógica pedagógica não deve ser duplicada na Web UI.

## Estrutura inicial do repositório

```text
.
├── app/
│   ├── main.py
│   ├── web/
│   │   ├── routes/
│   │   ├── templates/
│   │   └── static/
│   ├── domain/
│   │   ├── catalog/
│   │   ├── journey/
│   │   ├── learner/
│   │   ├── challenge/
│   │   └── evidence/
│   ├── application/
│   │   ├── ports/
│   │   ├── onboarding/
│   │   ├── probe/
│   │   ├── challenge_selection/
│   │   └── validation/
│   └── infrastructure/
│       ├── ai/
│       ├── catalog/
│       ├── database/
│       │   ├── models/
│       │   ├── repositories/
│       │   ├── mappers/
│       │   └── sqlalchemy_unit_of_work.py
│       └── validators/
├── database/
│   ├── migrations/
│   ├── company/
│   │   ├── init/
│   │   └── seed/
│   └── validators/
├── tickets/
├── probe/
├── skills/
├── journeys/
├── tests/
│   ├── fakes/
│   ├── unit/
│   │   ├── domain/
│   │   └── application/
│   ├── integration/
│   │   ├── database/
│   │   ├── validators/
│   │   └── web/
│   └── fixtures/
├── docs/
├── .github/workflows/
├── docker-compose.yml
├── pyproject.toml
├── uv.lock
├── Makefile
└── .env.example
```

Diretórios adicionais só devem ser criados quando houver necessidade concreta.

## Domain, DTOs e persistência

Entidades de domínio serão separadas dos models SQLAlchemy.

- entidades do domínio: `dataclasses`;
- DTOs e contratos de entrada/saída: Pydantic;
- models ORM: apenas em `infrastructure/database/models`;
- conversão ORM ↔ domínio: mappers explícitos;
- um arquivo por model e por repository.

Value objects leves serão usados quando houver invariantes relevantes, como `Mastery` e `Confidence`, ambos limitados a `0.0..1.0`.

No PostgreSQL, `mastery` e `confidence` serão persistidos como `NUMERIC` com constraint de faixa.

## Ports, repositories e Unit of Work

Dependências externas relevantes serão representadas por `Protocol` na camada `application`.

Portas iniciais previstas:

- `JourneyRepository`;
- `LearnerModelRepository`;
- `EvidenceRepository`;
- `ChallengeRepository`, se necessário;
- `AIProvider`;
- `UnitOfWork`.

Não serão criadas interfaces para todas as classes.

A `UnitOfWork` será mínima, implementada como context manager e responsável por coordenar a transação. Repositories não executam `commit()`.

O caso de uso controla a operação completa:

```text
use case
  ↓
with uow
  ↓
repositories
  ↓
commit ou rollback
```

No MVP monousuário não será introduzido locking específico para `learner_skill`.

## Casos de uso

Casos de uso serão classes pequenas e explícitas, com método `execute()`, orientadas a uma ação do usuário ou do sistema.

Exemplos:

- `StartJourney`;
- `ResumeJourney`;
- `SubmitProbeAnswer`;
- `SelectNextChallenge`;
- `SubmitSolution`;
- `ValidateSolution`;
- `RecordEvidence`;
- `CompleteJourney`.

DTOs Pydantic devem ficar próximos da feature correspondente, não em um diretório global genérico.

## Jornada

O MVP terá um único perfil local, sem login, identificado internamente por UUID.

O banco poderá manter várias jornadas históricas, porém no máximo uma jornada ativa por participante.

O estado da jornada será explícito e controlado pelo domínio, usando `Enum` e regras de transição. Estados iniciais previstos:

```text
NEW
ONBOARDING
PROBE
CHALLENGE
VALIDATING
COMPLETED
```

Biblioteca externa de state machine não é necessária no MVP.

O objetivo profissional será composto por uma opção estruturada com ID estável e contexto livre opcional. As opções serão versionadas em arquivo, por exemplo `journeys/goals.yaml`.

## Learner Model e evidências

O Learner Model mínimo permanece genérico por competência e registra:

- `skill_id`;
- `mastery`;
- `confidence`;
- quantidade de evidências.

A atualização de `mastery` e `confidence` será determinística, simples e auditável no MVP. A regra ficará no domínio, por exemplo em `LearnerModelUpdater`.

A evidência registra componentes auditáveis do cálculo, incluindo:

- origem;
- valência categórica e magnitude;
- força categórica e peso numérico;
- confiança da avaliação;
- nível de assistência e fator correspondente;
- impacto calculado;
- metadata adicional.

Origens iniciais previstas:

```text
PROBE
CHALLENGE_VALIDATION
POST_DELIVERY_QUESTION
SELF_ASSESSMENT
RECALIBRATION
```

A assistência será representada por categoria e fator numérico, sem invalidar automaticamente uma entrega.

O estado corrente ficará em `lab.learner_skill`. A evolução ficará em uma tabela histórica separada, `lab.learner_skill_history`, ligada à evidência que provocou a mudança.

Registro da evidência, atualização de `learner_skill` e criação do histórico ocorrerão na mesma transação.

## Identidade e convenções de persistência

- UUID para entidades persistidas como `learner`, `journey`, `evidence` e `telemetry`;
- IDs legíveis e estáveis para conteúdo versionado como `ticket_id`, `skill_id` e `probe_question_id`;
- tabelas e colunas em `snake_case`;
- tabelas no singular;
- FKs explícitas;
- todos os timestamps em UTC com `TIMESTAMPTZ`;
- Python usando `datetime` timezone-aware;
- DTOs expondo strings estáveis para enums e IDs.

## Catálogo de competências

Competências terão catálogo central versionado, inicialmente em:

```text
skills/catalog.yaml
```

Tickets e questões do PROBE referenciam IDs estáveis, por exemplo:

```text
sql.filtering
sql.join
sql.aggregation
professional.business_rules
```

O MVP não exige Skill Graph.

## Catálogo de tickets

Tickets em Markdown com YAML front matter serão a fonte de verdade do catálogo.

Diretrizes:

- identificador numérico de três dígitos;
- metadados estruturados no front matter;
- corpo Markdown como demanda apresentada ao participante;
- skills referenciadas por IDs do catálogo central;
- validação declarativa quando simples;
- validador Python adicional quando necessário;
- `expected.sql` separado por ticket quando a comparação usar query de referência.

O fato de `expected.sql` permanecer no pacote local é uma limitação aceita do MVP. Proteção real de validadores pertence a uma eventual arquitetura remota.

No startup, o Lab Engine deverá:

1. varrer `tickets/**/*.md`;
2. extrair e validar o front matter com Pydantic;
3. validar referências a skills, validadores e arquivos esperados;
4. montar um `TicketCatalog` read-only em memória;
5. falhar a inicialização se houver ticket inconsistente.

Classes de catálogo e invariantes ficarão em `domain/catalog`; loaders YAML/Markdown ficarão em `infrastructure/catalog`.

## PROBE SQL

As perguntas do PROBE serão conteúdo versionado separado do código, organizado inicialmente em `probe/sql/`.

Tipos suportados desde o início:

- `multiple_choice`;
- `free_text`;
- `sql`.

Estratégia de avaliação:

- `multiple_choice`: determinística;
- `sql`: determinística por execução e validação de resultado;
- `free_text`: rubrica estruturada, checagens simples e IA opcional.

Cada pergunta, resposta e evidência derivada será persistida para auditoria e recalibração.

## Submissão e validador SQL

No primeiro vertical slice, o participante escreve a solução diretamente na Web UI usando CodeMirror.

A execução inicial será somente leitura (`SELECT`).

O PostgreSQL terá um usuário dedicado para execução do participante, separado da conexão administrativa da aplicação, com:

- acesso controlado ao schema `company`;
- `search_path = company`;
- `default_transaction_read_only`;
- `statement_timeout`.

A validação deverá comparar comportamento/resultado, não o texto SQL.

Quando aplicável, o resultado da solução será normalizado e comparado com o resultado produzido por uma query de referência em `expected.sql`. A comparação deverá tratar explicitamente:

- colunas;
- valores;
- `NULL`;
- tipos quando relevantes;
- ordem apenas quando fizer parte do critério do ticket.

O contrato definitivo de normalização e erros será fechado durante a implementação do validador.

## Execução de tickets na jornada

Cada atribuição de ticket terá registro próprio, permitindo histórico e retomada. Status explícitos iniciais:

```text
ASSIGNED
IN_PROGRESS
SUBMITTED
VALIDATED
SKIPPED
COMPLETED
```

Uma direção de persistência é `lab.journey_ticket`, com UUID próprio, `journey_id`, `ticket_id`, status e timestamps relevantes.

## IA

A camada `application` definirá `AIProvider` como porta explícita.

A primeira implementação concreta usará o SDK Python oficial da OpenAI com `base_url` configurável, permitindo integração com APIs compatíveis com OpenAI.

Configurações iniciais:

```text
AI_ENABLED
AI_BASE_URL
AI_API_KEY
AI_MODEL
AI_TIMEOUT_SECONDS
```

A IA é opcional. Se `AI_ENABLED=false`, o ciclo determinístico deve continuar funcionando. Indisponibilidade do provider não deve impedir validações objetivas básicas.

O acesso ao PostgreSQL e o Lab Engine serão síncronos inicialmente. FastAPI pode usar handlers assíncronos na borda sem propagar uma stack async desnecessária pelo domínio e persistência.

## Web UI

A Web UI utilizará:

```text
FastAPI
├── routers por feature
├── Jinja2
├── HTMX
└── static
    ├── css
    ├── js
    └── vendor/codemirror
```

Templates serão organizados por fluxo, por exemplo `onboarding/`, `probe/`, `challenge/` e `progress/`.

A aplicação utilizará exceções tipadas no domínio/application e handlers FastAPI para transformá-las em feedback apropriado à interface.

## Startup, configuração e catálogos

O lifespan do FastAPI será responsável por validar a aplicação antes de aceitar requisições:

```text
Settings válidos?
    ↓
PostgreSQL disponível?
    ↓
SkillCatalog válido?
    ↓
TicketCatalog válido?
    ↓
ProbeCatalog válido?
    ↓
GoalCatalog válido?
    ↓
READY
```

Os catálogos serão montados como objetos read-only e injetados nos casos de uso. Não serão usados dicionários globais mutáveis nem reload de arquivos em cada operação.

## Logging, telemetria e healthchecks

Logging utilizará a biblioteca padrão do Python, com configuração centralizada:

- texto legível em `development`;
- JSON estruturado em `production-like`;
- `request_id` UUID por requisição HTTP propagado nos logs;
- contexto adicional como `journey_id` e `ticket_id` quando disponível.

A aplicação terá:

- `/health` para liveness;
- `/ready` para readiness, verificando ao menos PostgreSQL e estado de inicialização.

Telemetria será persistida em `lab.telemetry`, com:

- UUID;
- `journey_id` quando aplicável;
- `event_type`;
- `event_version`;
- timestamp UTC;
- `payload JSONB`.

Eventos iniciais plausíveis incluem início/retomada de jornada, respostas do PROBE, atribuição/submissão/validação de ticket, uso de assistência, `skip` e sinalizações de dificuldade.

## Testes

Estratégia:

- testes unitários de `domain` e `application` sem PostgreSQL;
- repositories in-memory reutilizáveis em `tests/fakes/`;
- testes de integração específicos para banco, validadores e Web UI;
- PostgreSQL usado somente onde a integração real agrega confiança.

## Makefile e CI

O `Makefile` deverá expor comandos simples como:

```text
make dev
make test
make lint
make format
make db-up
make db-down
make db-migrate
make db-reset
```

GitHub Actions deverá validar o próprio repositório com, no mínimo:

```text
uv sync
ruff check
ruff format --check
mypy
pytest
```

GitHub Actions não será o mecanismo de validação das soluções do participante.

## Vertical slice inicial

A primeira implementação deve validar o ciclo principal ponta a ponta antes da expansão do catálogo ou da sofisticação dos componentes:

```text
iniciar Lab
   ↓
informar objetivo profissional
   ↓
executar PROBE SQL
   ↓
criar / atualizar Learner Model
   ↓
selecionar 1 ticket
   ↓
participante resolve no editor SQL
   ↓
validar SQL localmente
   ↓
registrar evidências
   ↓
atualizar Learner Model
   ↓
selecionar próximo ticket
```

Esse fluxo é o núcleo do produto.

## Decisões ainda abertas para implementação

A arquitetura já está suficientemente definida para iniciar o MVP. Permanecem como decisões de implementação, a serem fechadas ao construir o vertical slice:

- modelo completo das tabelas e constraints do schema `lab`;
- contrato Pydantic definitivo do front matter de tickets;
- contrato definitivo das questões do PROBE;
- conjunto inicial de skills do catálogo;
- fórmula determinística exata de atualização de `mastery` e `confidence`;
- regras mínimas do Challenge Selector;
- campos e transições finais de `journey_ticket`;
- contrato de normalização e mensagens do validador SQL;
- empresa fictícia, domínio inicial e dataset;
- composição exata do primeiro PROBE e dos primeiros tickets do vertical slice.

Esses pontos não bloqueiam o início da implementação da fundação.

## Segurança dos testes

No MVP, testes, validadores e queries de referência permanecem no pacote local para simplificar a implementação.

Isso permite inspeção por participantes com acesso aos arquivos locais. Antes de tratar o produto como sistema competitivo ou comercial com avaliação de alta confiança, deverá ser avaliada uma estratégia de proteção dos validadores.

Possibilidades futuras:

- testes públicos + testes privados;
- serviço remoto de avaliação;
- datasets gerados dinamicamente;
- execução remota de critérios sensíveis.

A segurança dos testes não deve antecipar uma arquitetura cliente-servidor antes de existir necessidade comprovada.

## Evolução para plataforma

A arquitetura local deve permitir evolução sem exigir que o MVP já implemente componentes de plataforma.

Uma evolução possível é:

```text
Web Client
    │
    ▼
Backend / API
    │
    ▼
Application / Domain
    │
    ├── persistência centralizada
    └── ambientes de execução
```

Autenticação, mensalidade, contas, persistência centralizada, execução remota e multiusuário somente devem ser introduzidos após validação do produto local.

## Versionamento

Direção inicial:

- releases semânticos para evolução do simulador;
- tickets com identificador imutável;
- tickets publicados não devem sofrer mudanças incompatíveis;
- correções relevantes devem ser registradas em changelog;
- o repositório permanece privado enquanto a hipótese comercial estiver em validação, sem licença pública definida neste estágio.

Exemplo:

```text
v0.1.0 → MVP inicial / SQL
v0.2.0 → novos tickets SQL
v0.3.0 → modelagem
v1.0.0 → experiência considerada estável
```
