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

## Geração assistida de tickets

O MVP deverá permitir geração assistida de propostas de tickets por IA sem tornar a publicação autônoma.

```text
Perfil / nível / domínio / conceitos-alvo
                   │
                   ▼
           Task Generator (IA)
                   │
                   ▼
          proposta estruturada
                   │
                   ▼
         validação / revisão
                   │
                   ▼
             ticket oficial
```

O gerador deverá trabalhar sobre um contrato estruturado e respeitar as convenções pedagógicas do projeto.

A existência do gerador não implica Skill Graph, perfil centralizado ou Progression Agent no MVP. Inicialmente, nível e conceitos-alvo podem ser informados explicitamente.

## Avaliação híbrida

A avaliação deverá priorizar verificações determinísticas sempre que o critério puder ser testado objetivamente.

```text
Entrega do participante
          │
          ▼
testes / validações determinísticas
          │
          ├── execução
          ├── resultado
          ├── regras de negócio
          ├── restrições
          └── performance, quando aplicável
          │
          ▼
     evidências objetivas
          │
          ▼
 análise/feedback por IA
          │
          ▼
 feedback contextualizado
```

O LLM não deve substituir testes objetivos quando esses testes forem possíveis.

O MVP pode armazenar evidências de forma simples e local. Um modelo sofisticado de competências é uma evolução posterior.

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

No MVP, evitar dependências externas obrigatórias para execução das soluções e validações determinísticas. Recursos de IA podem ser desacoplados do ambiente técnico mínimo do participante quando necessário.

## Estrutura do repositório

```text
.
├── README.md
├── docker-compose.yml
├── .env.example
│
├── docs/
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
│   ├── ticket-001/
│   ├── ticket-002/
│   └── ...
│
└── .github/
    ├── workflows/
    │   └── validate.yml
    └── pull_request_template.md
```

A estrutura do repositório segue a convenção de IDs e caminhos definida para o MVP: tickets usam o identificador numérico de três dígitos no nome do arquivo; soluções e testes usam o formato `ticket-NNN/`.

Componentes específicos para geração de tickets e registro de evidências deverão ser introduzidos apenas quando seus contratos forem definidos, evitando antecipar diretórios ou serviços sem necessidade concreta.

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

Resultados do CI poderão servir como evidências para feedback assistido por IA.

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
