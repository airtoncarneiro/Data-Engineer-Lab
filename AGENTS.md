# AGENTS.md

Este arquivo orienta agentes de programação que trabalham neste repositório.

## Fonte de verdade

- A branch `main` é a fonte de verdade do projeto.
- Antes de alterar arquitetura, contratos, persistência, fluxo pedagógico ou experiência do participante, leia os documentos relevantes em `docs/`.
- Em divergências entre instruções antigas, chats e o repositório, prevalece o estado atual da `main`.

## Documentos principais

- `docs/ARCHITECTURE.md` — arquitetura, stack e convenções técnicas.
- `docs/DISCOVERY.md` — problema, hipótese, público e experiência do produto.
- `docs/PRINCIPLES.md` — princípios de Engenharia de Dados, Software e aprendizado.
- `docs/ROADMAP.md` — evolução planejada e limites de escopo.
- `docs/BACKLOG.md` — trabalho pendente do MVP.
- `docs/DEVELOPMENT.md` — setup, comandos, validações e workflow de desenvolvimento.

Leia apenas os documentos necessários ao escopo da tarefa, mas nunca contradiga decisões documentadas sem que a tarefa peça explicitamente sua revisão.

## Stack aprovada do MVP

- Python 3.11.
- FastAPI + Jinja2 + HTMX.
- CodeMirror servido localmente.
- PostgreSQL 16 via Docker Compose.
- schemas `lab` e `company` na mesma instância PostgreSQL.
- SQLAlchemy 2.x + psycopg 3.
- Alembic para migrations do schema `lab`.
- scripts SQL versionados para criação e seed do schema `company`.
- `uv` + `pyproject.toml`.
- Pydantic + `pydantic-settings`.
- pytest, Ruff e mypy.
- SDK Python oficial da OpenAI por trás de `AIProvider`, com `base_url` configurável.

Não introduza framework, serviço, banco, broker, container adicional ou dependência relevante sem necessidade concreta e sem verificar a arquitetura existente.

## Arquitetura de código

A separação principal é:

```text
web -> application -> domain
          ^
          |
   infrastructure
```

Regras:

- `domain` não depende de FastAPI, SQLAlchemy, PostgreSQL ou SDKs externos.
- `application` coordena casos de uso e define portas via `Protocol` quando houver fronteira externa real.
- `infrastructure` implementa repositories, Unit of Work, mappers, loaders, validadores técnicos e providers externos.
- `web` trata HTTP, templates, apresentação e tradução de erros; não contém regras pedagógicas.
- entidades de domínio são separadas de models ORM.
- DTOs Pydantic ficam próximos dos respectivos casos de uso.
- casos de uso devem ser pequenos, orientados a uma ação e expor `execute()`.
- transações pertencem à camada `application` por meio de `UnitOfWork`; repositories não fazem `commit()`.

Evite criar abstrações sem uso concreto.

## Regras de implementação

- Priorize clareza, legibilidade, testabilidade e baixo acoplamento.
- Preserve comportamento existente salvo quando a tarefa pedir mudança.
- Prefira mudanças pequenas e coerentes ao escopo da tarefa.
- Não duplique configuração ou documentação.
- Não use `requirements.txt`; dependências pertencem ao `pyproject.toml`.
- Não exponha segredos. `.env` é local; `.env.example` contém apenas exemplos seguros.
- Timestamps persistidos usam UTC e `TIMESTAMPTZ`.
- Python segue PEP 8.
- Banco usa `snake_case`, tabelas no singular e FKs explícitas.

## Conteúdo pedagógico

- Tickets são Markdown com YAML front matter e IDs estáveis.
- `skills/catalog.yaml` é a fonte de verdade das competências.
- Catálogos versionados são carregados e validados no startup.
- Ticket inválido deve falhar cedo.
- Validação objetiva deve ser determinística sempre que possível.
- No vertical slice inicial, submissões SQL são somente leitura e executadas com usuário PostgreSQL restrito ao schema `company`.
- A validação compara resultado, não a forma textual da SQL, salvo requisito explícito do ticket.
- IA complementa critérios subjetivos; não substitui validações determinísticas objetivas.

## Testes e qualidade

Antes de concluir uma mudança, execute as validações aplicáveis definidas em `docs/DEVELOPMENT.md` e no `Makefile`.

Como regra geral, espere executar:

```text
make test
make lint
```

Quando comandos específicos ainda não existirem no estágio atual do bootstrap, implemente ou documente somente o necessário para a tarefa em andamento; não invente resultados de validação.

Testes unitários devem evitar infraestrutura real quando repositories in-memory forem suficientes. Testes de integração devem cobrir fronteiras reais, especialmente PostgreSQL, validators e Web UI.

## Documentação

Atualize documentação quando uma mudança alterar arquitetura, contrato, convenção, operação ou comportamento relevante do produto.

Não transforme documentos conceituais em logs de implementação. Preserve a distinção entre:

- implementado;
- decidido;
- planejado;
- hipótese futura.

## Tasks de desenvolvimento

Quando a tarefa tiver especificação em `tasks/active/`, trate esse arquivo como contrato de execução complementar ao backlog.

- Respeite objetivo, escopo, critérios de aceite e fora de escopo.
- Não expanda silenciosamente a tarefa.
- Ao concluir e validar uma task, mova seu arquivo para `tasks/completed/` apenas quando isso fizer parte da solicitação ou do workflow explícito da tarefa.

## Git

- Não reescreva histórico nem force push.
- Não modifique trabalho não relacionado.
- Se a `main` mudar durante uma operação de publicação, reavalie antes de atualizar a branch.
- Commits devem ser pequenos, coerentes e descrever a mudança realizada.
