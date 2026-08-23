# Data Engineer Lab

Laboratório educacional de Engenharia de Dados baseado em **learning by doing**, com cenários próximos aos encontrados em ambientes profissionais.

O projeto simula uma empresa fictícia com dados, documentação, demandas contextualizadas e validação automatizada. O participante recebe desafios em formato de tickets e evolui de acordo com evidências de competência, não apenas pela conclusão de uma sequência fixa de exercícios.

## Estado atual

O projeto está na fase de definição e implementação do MVP SQL.

A arquitetura aprovada para o MVP é local:

```text
Browser
   │
   ▼
Local Web UI
   │
   ▼
Lab Engine (Python)
   │
   ├── PostgreSQL via Docker
   └── persistência local da jornada
```

O GitHub é utilizado para desenvolvimento, versionamento e distribuição do produto. Fork, Pull Request e GitHub Actions não fazem parte do fluxo operacional obrigatório do participante no MVP.

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
