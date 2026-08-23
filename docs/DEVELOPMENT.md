# Desenvolvimento

## Objetivo

Este documento define o workflow operacional de desenvolvimento do Data Engineer Lab. A arquitetura e as decisões técnicas permanecem em `ARCHITECTURE.md`; este arquivo concentra setup, comandos, validações e troubleshooting.

## Pré-requisitos

- Python 3.11.
- `uv`.
- Docker com Docker Compose.
- Git.

O PostgreSQL roda em Docker. A aplicação Python roda localmente via `uv` no primeiro momento.

## Setup inicial

Quando a fundação estiver implementada, o fluxo esperado será:

```bash
cp .env.example .env
uv sync
make db-up
make db-migrate
make dev
```

O arquivo `.env` é local e não deve ser versionado.

## Configuração

A aplicação usa `pydantic-settings` e valida configuração no startup.

Variáveis previstas para o MVP incluem:

```dotenv
APP_ENV=development
DATABASE_URL=
LOG_LEVEL=INFO
AI_ENABLED=false
AI_BASE_URL=
AI_API_KEY=
AI_MODEL=
AI_TIMEOUT_SECONDS=30
```

Quando `AI_ENABLED=false`, recursos determinísticos devem continuar operando sem dependência de serviço externo.

Quando `AI_ENABLED=true`, as configurações obrigatórias do provider devem falhar cedo se estiverem ausentes ou inválidas.

## Ambientes

Valores suportados inicialmente:

- `development` — execução local e logs legíveis.
- `test` — testes automatizados.
- `production-like` — validação de comportamento próximo de execução futura, incluindo logs estruturados quando aplicável.

## Comandos do projeto

O `Makefile` deve fornecer uma interface operacional simples. A direção aprovada é:

```bash
make dev
make test
make lint
make format
make db-up
make db-down
make db-migrate
make db-reset
```

Os comandos só devem ser considerados disponíveis depois que forem implementados no repositório.

### Desenvolvimento

`make dev` deve iniciar a aplicação FastAPI localmente via `uv`.

Direção esperada:

```bash
uv run fastapi dev app/main.py
```

### PostgreSQL

`make db-up` inicia o PostgreSQL 16 via Docker Compose.

`make db-down` encerra o ambiente local.

`make db-migrate` aplica as migrations Alembic do schema `lab`.

`make db-reset` reconstrói os dados do schema `company` de forma determinística. O reset do cenário técnico não deve apagar silenciosamente o estado da jornada persistido no schema `lab`.

## Banco de dados

Uma única instância PostgreSQL contém separação lógica:

```text
PostgreSQL
├── lab
│   └── persistência interna da aplicação
└── company
    └── dados utilizados pelos desafios SQL
```

### Schema `lab`

- gerenciado por SQLAlchemy 2.x e Alembic;
- persistência de learner, journey, evidências, Learner Model, histórico e telemetria;
- migrations devem ser versionadas e reversíveis quando razoável.

### Schema `company`

- criado e populado por scripts SQL versionados;
- seed determinístico;
- representa o ambiente técnico da empresa fictícia;
- deve ser reconstruível por comando.

## Validação SQL do participante

No vertical slice inicial:

- apenas `SELECT` é aceito;
- a execução usa usuário PostgreSQL dedicado e restrito ao schema `company`;
- `search_path` aponta para `company`;
- a conexão de validação deve ser read-only;
- `statement_timeout` deve limitar queries;
- a aplicação nunca deve executar SQL do participante usando a conexão administrativa do schema `lab`.

A validação deve comparar o resultado normalizado com a referência definida pelo ticket. Arquivos `expected.sql` podem permanecer locais no MVP; proteção real de testes pertence a uma eventual arquitetura remota.

## Migrations

Migrations Alembic pertencem ao schema `lab`.

Fluxo esperado após uma mudança persistente:

```bash
uv run alembic revision --autogenerate -m "descricao"
uv run alembic upgrade head
```

Revise migrations autogeradas antes de commitá-las. Não assuma que o autogenerate representa corretamente toda intenção de domínio.

Mudanças no schema `company` devem usar scripts SQL explícitos e manter compatibilidade com o mecanismo de reset e com tickets existentes, salvo mudança intencional documentada.

## Testes

A estrutura aprovada é:

```text
tests/
├── fakes/
├── unit/
│   ├── domain/
│   └── application/
├── integration/
│   ├── database/
│   ├── validators/
│   └── web/
└── fixtures/
```

### Unitários

- priorizam domínio e casos de uso;
- usam repositories in-memory em `tests/fakes/` quando possível;
- não sobem PostgreSQL sem necessidade.

### Integração

Cobrem fronteiras reais, principalmente:

- SQLAlchemy/PostgreSQL;
- Unit of Work e repositories;
- migrations relevantes;
- validador SQL;
- routes e integração Web quando aplicável.

### Execução

```bash
make test
```

ou, diretamente:

```bash
uv run pytest
```

## Lint, format e tipagem

Ferramentas aprovadas:

- Ruff para lint;
- Ruff para formatação;
- mypy para tipagem estática com configuração moderada.

Fluxo esperado:

```bash
make lint
make format
```

Uma direção possível para `make lint` é:

```bash
uv run ruff check .
uv run ruff format --check .
uv run mypy app
```

Não habilitar `mypy --strict` automaticamente no bootstrap. A rigidez pode evoluir conforme o código estabilizar.

## Health e readiness

A Web UI deve expor:

```text
GET /health
GET /ready
```

`/health` verifica apenas se o processo está vivo.

`/ready` verifica dependências essenciais, especialmente PostgreSQL e catálogos carregados no startup. Quando a aplicação não estiver pronta, deve responder com status apropriado, por exemplo HTTP 503.

## Startup

O lifespan do FastAPI deve executar validações antes de aceitar tráfego:

1. validar `Settings`;
2. validar conexão PostgreSQL;
3. carregar catálogo de objetivos;
4. carregar `skills/catalog.yaml`;
5. carregar e validar tickets Markdown/YAML;
6. carregar e validar catálogo do PROBE;
7. validar referências internas;
8. marcar a aplicação como pronta.

Erros de catálogo ou configuração obrigatória devem interromper o startup com mensagem clara.

## Logs

- `development`: texto legível.
- `production-like`: formato estruturado JSON.
- cada requisição HTTP recebe `request_id`.
- quando disponíveis, inclua `journey_id` e `ticket_id` como contexto, sem duplicar telemetria pedagógica.

Logs técnicos e `lab.telemetry` têm responsabilidades diferentes. Telemetria registra eventos relevantes da experiência; logging registra operação e diagnóstico da aplicação.

## CI

GitHub Actions é usado para qualidade do próprio produto, não para validar soluções do participante.

Pipeline mínimo esperado:

```text
uv sync
  ↓
ruff check
  ↓
ruff format --check
  ↓
mypy
  ↓
pytest
```

Mudanças não devem ser declaradas validadas quando comandos aplicáveis não puderem ser executados.

## Workflow agent-first

O desenvolvimento pode ser realizado majoritariamente por agentes como Codex.

Antes de implementar uma task, o agente deve:

1. ler `AGENTS.md`;
2. ler a task em `tasks/active/`, quando existir;
3. consultar apenas os documentos de arquitetura/produto necessários;
4. inspecionar o código afetado antes de propor mudanças;
5. implementar somente o escopo necessário;
6. atualizar testes e documentação impactados;
7. executar validações aplicáveis;
8. registrar objetivamente o que foi alterado e validado.

Uma task deve ser pequena o suficiente para que critérios de aceite sejam verificáveis em uma execução de agente.

## Troubleshooting

### PostgreSQL não está disponível

Verifique:

```bash
docker compose ps
docker compose logs postgres
```

Depois valide `.env` e `DATABASE_URL`.

### Migration falha

- confirme que PostgreSQL está pronto;
- verifique a revisão atual do Alembic;
- inspecione a migration antes de tentar recriar dados;
- não use reset do schema `company` para corrigir problema no schema `lab`.

### Aplicação inicia, mas `/ready` falha

Verifique, nesta ordem:

1. configuração obrigatória;
2. PostgreSQL;
3. migrations do schema `lab`;
4. arquivos de catálogo;
5. referências de skills, tickets e PROBE.

### IA indisponível

Com `AI_ENABLED=false`, o core determinístico deve continuar operando.

Com `AI_ENABLED=true`, valide `AI_BASE_URL`, `AI_API_KEY`, `AI_MODEL` e timeout. Falha do provider não deve corromper jornada, evidências ou estado transacional.

## Princípio operacional

O setup local deve permanecer simples e reproduzível. Introduza infraestrutura adicional apenas quando um requisito concreto do MVP exigir.
