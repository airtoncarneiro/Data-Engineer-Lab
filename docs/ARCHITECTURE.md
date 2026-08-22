# Arquitetura Inicial

## Objetivo

Definir uma arquitetura mínima para o MVP do simulador sem antecipar componentes que ainda não são necessários.

## Visão lógica

```text
                    REPOSITÓRIO PRINCIPAL
                           upstream
                              │
                 novos tickets / versões
                              │
                              ▼
                    FORK DO PARTICIPANTE
                              │
                branch → implementação
                              │
                              ▼
                       Pull Request
                              │
                              ▼
                     GitHub Actions
                              │
                   testes automatizados
                              │
                  ┌───────────┴───────────┐
                  ▼                       ▼
                PASS                    FAIL
                  │                       │
          ticket concluído        feedback no CI
```

## Ambiente local

```text
Developer Environment
│
├── Git / GitHub
├── Editor / IDE
└── Docker Compose
    └── PostgreSQL
        ├── schemas
        ├── tabelas
        └── dados iniciais
```

No MVP, evitar dependências externas obrigatórias.

## Estrutura proposta do repositório

```text
.
├── README.md
├── docker-compose.yml
├── .env.example
│
├── docs/
│   ├── VISION.md
│   ├── DISCOVERY.md
│   ├── PRINCIPLES.md
│   ├── ARCHITECTURE.md
│   ├── ROADMAP.md
│   ├── BACKLOG.md
│   └── company/
│       ├── COMPANY.md
│       ├── DATA_DICTIONARY.md
│       └── BUSINESS_RULES.md
│
├── database/
│   ├── migrations/
│   ├── seed/
│   └── init/
│
├── tickets/
│   ├── 000-onboarding.md
│   ├── 001-....md
│   └── ...
│
├── solutions/
│   ├── ticket-001/
│   ├── ticket-002/
│   └── ...
│
├── tests/
│   ├── ticket_001/
│   ├── ticket_002/
│   └── ...
│
└── .github/
    ├── workflows/
    │   └── validate.yml
    └── pull_request_template.md
```

A estrutura é uma proposta inicial e deverá ser validada durante a implementação do MVP.

## Separação entre conteúdo e solução

`tickets/` pertence ao produto e é atualizado pelo upstream.

`solutions/` representa a área de trabalho do participante.

Essa separação reduz conflitos durante sincronizações futuras.

## Banco de dados

Inicialmente:

- PostgreSQL;
- executado via Docker;
- schema versionado;
- seed determinístico;
- reconstrução completa do ambiente por comando;
- volume suficiente para tornar os desafios realistas sem prejudicar máquinas pessoais.

## CI

O GitHub Actions deverá:

1. preparar o ambiente;
2. iniciar PostgreSQL;
3. aplicar schema e seed;
4. identificar o ticket associado à entrega;
5. executar a solução;
6. executar testes do ticket;
7. publicar feedback;
8. retornar sucesso ou falha.

## Segurança dos testes

No MVP, os testes poderão estar no próprio repositório para simplificar a implementação.

Entretanto, isso permite que participantes inspecionem critérios e resultados esperados. Antes de tratar o projeto como sistema competitivo, deverá ser avaliada uma estratégia de testes privados.

Possibilidades futuras:

- workflow reutilizável mantido externamente;
- serviço remoto de avaliação;
- testes públicos + testes privados;
- datasets gerados dinamicamente.

## Versionamento

Sugestão inicial:

- releases semânticos para evolução do simulador;
- tickets com identificador imutável;
- tickets publicados não devem sofrer mudanças incompatíveis;
- correções relevantes devem ser registradas em changelog.

Exemplo:

```text
v0.1.0 → MVP inicial / SQL
v0.2.0 → novos tickets SQL
v0.3.0 → modelagem
v1.0.0 → experiência considerada estável
```

## Arquitetura futura

Somente após validação do MVP poderão ser considerados:

```text
GitHub
   │
   ├── CI Validator
   │
   └── Result Event
          │
          ▼
       API / Backend
          │
          ├── users
          ├── progress
          ├── scores
          └── badges
                 │
                 ▼
               Portal
```

Essa arquitetura **não faz parte do MVP**.
