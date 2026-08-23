# Data Engineer Lab

Laboratório educacional de Engenharia de Dados baseado em **learning by doing**, com cenários próximos aos encontrados em ambientes profissionais.

O projeto simula uma empresa fictícia com dados, documentação, demandas contextualizadas e validação automatizada. O participante recebe desafios em formato de tickets e evolui de acordo com evidências de competência, não apenas pela conclusão de uma sequência fixa de exercícios.

## Estado atual

O projeto está pronto para iniciar a implementação da fundação e do primeiro vertical slice do MVP SQL.

A arquitetura aprovada para o MVP é local:

```text
Browser
   │
   ▼
FastAPI + Jinja2 + HTMX
   │
   ▼
Application / Domain
   │
   ├── PostgreSQL 16 via Docker
   │   ├── schema lab
   │   └── schema company
   └── provider de IA compatível com OpenAI, quando habilitado
```

A aplicação Python roda localmente via `uv`; no primeiro momento, somente o PostgreSQL é executado em Docker. A Web UI utiliza assets locais, incluindo CodeMirror para edição SQL, sem exigir Node.js ou build frontend.

O GitHub é utilizado para desenvolvimento, versionamento, distribuição e CI do produto. Fork, Pull Request e GitHub Actions não fazem parte do fluxo operacional obrigatório do participante no MVP.

## Stack mínima aprovada

- Python 3.11;
- FastAPI + Jinja2 + HTMX;
- CodeMirror e CSS próprio servidos localmente pelo FastAPI;
- PostgreSQL 16 via Docker Compose;
- SQLAlchemy 2.x + psycopg 3;
- Alembic para o schema `lab`;
- scripts SQL versionados para criação e seed do schema `company`;
- `uv` + `pyproject.toml`;
- Pydantic + `pydantic-settings`;
- pytest, Ruff e mypy;
- SDK Python oficial da OpenAI por trás de um contrato `AIProvider`, com `base_url` configurável;
- GitHub Actions para CI do próprio produto.

Detalhes, fronteiras arquiteturais e convenções estão em [Arquitetura](docs/ARCHITECTURE.md).

## Experiência principal do MVP

O primeiro vertical slice deve provar o ciclo adaptativo ponta a ponta:

```text
iniciar Lab
   ↓
informar objetivo profissional
   ↓
PROBE SQL
   ↓
Learner Model
   ↓
seleção de desafio
   ↓
solução do participante
   ↓
validação determinística
   ↓
registro de evidências
   ↓
atualização do Learner Model
   ↓
seleção do próximo desafio
```

A jornada SQL deverá usar aproximadamente 10 desafios como referência de duração, com adaptação baseada nas competências demonstradas.

## Princípios

- problemas profissionais antes de exercícios artificiais;
- validação determinística sempre que possível;
- IA como complemento, não como autoridade única para critérios objetivos;
- progressão baseada em evidências;
- autonomia do participante;
- ambiente reproduzível;
- simplicidade antes de complexidade;
- evolução incremental para uma possível plataforma somente após validação do produto local.

## Documentação

- [Discovery](docs/DISCOVERY.md)
- [Princípios](docs/PRINCIPLES.md)
- [Arquitetura](docs/ARCHITECTURE.md)
- [Roadmap](docs/ROADMAP.md)
- [Backlog](docs/BACKLOG.md)

## Escopo inicial

O MVP começa com SQL e PostgreSQL. Evoluções possíveis incluem modelagem, Python, ETL/ELT, Airflow, plataforma de dados, cloud, operação e cenários de incidentes.

Autenticação, backend centralizado, multiusuário, mensalidade, execução remota e portal hospedado pertencem a uma eventual evolução para plataforma e não são requisitos do MVP local.
