# Arquitetura Inicial

## Objetivo

Definir uma arquitetura mínima para o MVP do simulador sem antecipar componentes que ainda não são necessários.

## Decisão arquitetural do MVP

O MVP será executado localmente pelo participante e terá como interface principal uma Web UI local.

A arquitetura mínima aprovada é:

```text
Browser
   │
   ▼
Local Web UI
   │
   ▼
Lab Engine (Python)
   ├── Onboarding / Journey State
   ├── PROBE
   ├── Learner Model
   ├── Challenge Selector
   ├── Ticket Generator
   ├── Validator
   └── Evidence Engine
   │
   ├── PostgreSQL do laboratório
   └── Persistência local do participante
```

O GitHub permanece como repositório de desenvolvimento, versionamento e distribuição do produto, mas não é parte obrigatória do fluxo operacional do participante no MVP.

Fork, branch, Pull Request e GitHub Actions podem ser utilizados no desenvolvimento do projeto, mas não são requisitos para o aluno executar uma jornada, enviar uma solução ou receber validação.

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
participante resolve
   ↓
validar SQL
   ↓
registrar evidências
   ↓
atualizar Learner Model
   ↓
selecionar próximo ticket
```

Esse fluxo é o núcleo do produto. Funcionalidades adicionais devem ser introduzidas apenas quando contribuírem para validar ou melhorar esse ciclo.

## Lab Engine

O Lab Engine é o núcleo de aplicação do MVP. Ele coordena regras de negócio e componentes da experiência, sem depender da Web UI para implementar lógica pedagógica.

Responsabilidades iniciais:

- iniciar e retomar uma jornada;
- registrar objetivo profissional;
- conduzir o PROBE;
- persistir e atualizar o Learner Model;
- selecionar o próximo desafio;
- disponibilizar tickets à interface;
- executar validações determinísticas;
- registrar evidências e telemetria;
- controlar assistência, `skip` e recalibração;
- acionar geração assistida de desafios quando aplicável.

A Web UI deve consumir essas capacidades sem duplicar regras centrais.

No MVP, não é necessário criar uma API de rede independente. A separação entre UI e Lab Engine deve ocorrer em código e contratos internos, permitindo que uma API seja introduzida posteriormente se a evolução para plataforma exigir.

## Web UI local

A Web UI é a interface operacional do participante no MVP.

Ela deve permitir, progressivamente:

- iniciar ou retomar a jornada;
- informar objetivo profissional;
- responder ao PROBE;
- visualizar o ticket corrente;
- informar ou apontar a solução SQL conforme o contrato definido;
- executar a validação;
- receber feedback;
- solicitar assistência;
- pular desafios;
- visualizar progresso qualitativo quando aplicável.

A UI não deve conter lógica de avaliação ou progressão que pertença ao Lab Engine.

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
             ticket qualificado
```

O gerador deverá trabalhar sobre um contrato estruturado e respeitar as convenções pedagógicas do projeto.

O lifecycle mínimo continua sendo:

`candidate -> validated -> trialed -> published`

A existência do gerador não implica Skill Graph, perfil centralizado ou Progression Agent no MVP. Inicialmente, nível e conceitos-alvo podem ser informados explicitamente ou derivados do Learner Model mínimo.

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
Developer / Learner Environment
│
├── Browser
├── aplicação local
│   ├── Web UI
│   └── Lab Engine
└── Docker Compose
    └── PostgreSQL
        ├── schemas
        ├── tabelas
        └── dados iniciais
```

No MVP, evitar dependências externas obrigatórias para execução das soluções e validações determinísticas. Recursos de IA devem ser desacoplados do ambiente técnico mínimo quando possível, de forma que falhas ou ausência do provedor de IA não impeçam validações determinísticas básicas.

## Persistência local

O MVP deve persistir localmente, no mínimo:

- estado da jornada;
- objetivo profissional;
- Learner Model;
- evidências;
- telemetria relevante;
- estado dos desafios gerados, quando aplicável.

A tecnologia exata de persistência deve permanecer simples. O PostgreSQL do laboratório pode ser reutilizado quando isso reduzir complexidade, desde que dados do participante e dados usados nos desafios permaneçam logicamente separados.

Persistência centralizada, contas e sincronização entre dispositivos pertencem à evolução para plataforma e não são requisitos do MVP.

## Estrutura inicial do repositório

A estrutura deve evoluir conforme os contratos forem implementados. Uma direção mínima é:

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
│   └── BACKLOG.md
│
├── app/
│   ├── web/
│   └── lab_engine/
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
│   └── ...
│
└── tests/
    ├── ticket-001/
    └── ...
```

Os nomes finais de módulos e diretórios devem ser definidos durante a implementação, evitando antecipar abstrações sem necessidade concreta.

Tickets usam identificador numérico de três dígitos. Soluções e testes, quando persistidos em arquivos, devem manter associação inequívoca ao ticket.

## Separação entre produto, conteúdo e solução

`tickets/` pertence ao produto e contém desafios qualificados ou artefatos versionados do catálogo.

`solutions/` representa uma possível área local de trabalho do participante quando o contrato de entrega exigir arquivos. A Web UI também pode receber ou referenciar a solução sem exigir operações Git do aluno.

O repositório GitHub contém o código e o conteúdo oficial do produto. O participante não precisa receber todo o histórico de desenvolvimento nem utilizar fork para operar o MVP.

## Banco de dados

Inicialmente:

- PostgreSQL;
- executado via Docker;
- schema versionado;
- seed determinístico;
- reconstrução completa do ambiente por comando;
- volume suficiente para tornar os desafios realistas sem prejudicar máquinas pessoais.

## Validação local

O Lab Engine deverá:

1. garantir que o ambiente necessário esteja disponível;
2. preparar ou resetar o estado do banco quando necessário;
3. identificar o ticket associado à entrega;
4. executar a solução em ambiente controlado;
5. executar testes e verificações do ticket;
6. produzir evidências objetivas;
7. retornar feedback claro à Web UI;
8. atualizar o estado da jornada quando aplicável.

GitHub Actions pode continuar existindo posteriormente para validar o próprio repositório do produto, mas não substitui o validador local do MVP.

## Segurança dos testes

No MVP, testes e critérios determinísticos podem permanecer no pacote local para simplificar a implementação.

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
Lab Engine
    ├── Journey
    ├── Learner Model
    ├── Challenge Engine
    ├── Validator
    └── Evidence Engine
    │
    ├── persistência centralizada
    └── ambientes de execução
```

Autenticação, mensalidade, contas, persistência centralizada, execução remota e multiusuário somente devem ser introduzidos após validação do produto local.

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
