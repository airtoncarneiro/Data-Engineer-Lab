# Backlog Inicial

Backlog preliminar para iniciar o MVP. A ordem poderá mudar conforme decisões técnicas.

## Épico 1 — Empresa fictícia

- [ ] Definir nome e segmento da empresa.
- [ ] Definir narrativa mínima da empresa.
- [ ] Definir departamentos que solicitarão demandas.
- [ ] Definir sistemas fonte iniciais.
- [ ] Criar glossário de negócio.
- [ ] Criar regras de negócio iniciais.

## Épico 2 — Modelo de dados

- [ ] Definir domínio inicial adequado aos tickets SQL.
- [ ] Modelar PostgreSQL.
- [ ] Criar migrations/init scripts.
- [ ] Criar massa de dados determinística.
- [ ] Incluir casos de borda necessários aos desafios.
- [ ] Criar processo simples de reset.
- [ ] Criar dicionário de dados.

## Épico 3 — Ambiente local

- [ ] Criar `docker-compose.yml`.
- [ ] Configurar PostgreSQL.
- [ ] Criar `.env.example`.
- [ ] Criar comando/documentação de inicialização.
- [ ] Criar healthcheck.
- [ ] Validar execução em ambiente limpo.

## Épico 4 — Framework de tickets

- [ ] Definir template de ticket.
- [ ] Definir convenção de IDs.
- [ ] Definir níveis de dificuldade.
- [ ] Definir estrutura de dependências entre tickets.
- [ ] Definir critérios de aceite.
- [ ] Definir estrutura de arquivos para solução.

## Épico 5 — Onboarding

- [ ] Criar ticket `000`.
- [ ] Orientar fork do projeto.
- [ ] Orientar clone do fork.
- [ ] Orientar configuração do `upstream`.
- [ ] Subir ambiente local.
- [ ] Validar conexão ao PostgreSQL.
- [ ] Executar primeira consulta de diagnóstico.
- [ ] Explicar fluxo branch → PR → CI.

## Épico 6 — Tickets SQL

Criar aproximadamente 10 tickets cobrindo progressivamente:

- [ ] filtros e regras de negócio;
- [ ] joins;
- [ ] agregações;
- [ ] subqueries/CTEs;
- [ ] tratamento de datas;
- [ ] window functions;
- [ ] qualidade/inconsistências;
- [ ] análise investigativa;
- [ ] performance básica;
- [ ] desafio integrador.

Os tickets não devem necessariamente corresponder 1:1 a esses tópicos. A demanda de negócio deve determinar quais técnicas serão necessárias.

## Épico 7 — Validador

- [ ] Definir contrato da solução SQL.
- [ ] Criar executor de soluções.
- [ ] Criar framework de testes por ticket.
- [ ] Validar resultado, não apenas texto SQL.
- [ ] Produzir mensagens de erro úteis.
- [ ] Garantir isolamento entre testes.
- [ ] Avaliar timeout de queries.

## Épico 8 — GitHub Workflow

- [ ] Criar Pull Request template.
- [ ] Criar workflow de CI.
- [ ] Subir PostgreSQL no CI.
- [ ] Carregar dataset.
- [ ] Executar testes.
- [ ] Exibir resultado claramente na PR.
- [ ] Documentar execução no fork.

## Épico 9 — Sincronização

- [ ] Documentar `origin` versus `upstream`.
- [ ] Documentar sincronização do fork.
- [ ] Garantir que soluções não sejam sobrescritas por releases futuras.
- [ ] Definir política de alteração de tickets publicados.
- [ ] Definir versionamento/releases.

## Épico 10 — Validação do produto

- [ ] Selecionar pequeno grupo de usuários iniciais.
- [ ] Medir taxa de onboarding concluído sem ajuda.
- [ ] Medir tempo até a primeira entrega.
- [ ] Medir taxa de conclusão de tickets.
- [ ] Registrar número de intervenções do mantenedor.
- [ ] Avaliar capacidade de interpretar feedback do CI.
- [ ] Coletar percepção de realismo.
- [ ] Decidir se o formato merece expansão.

## Depois do MVP

- [ ] Definir próxima trilha com base no feedback.
- [ ] Avaliar Airflow.
- [ ] Avaliar Python/ETL.
- [ ] Avaliar gamificação.
- [ ] Avaliar backend de progresso.
- [ ] Prototipar agentes para geração e revisão de desafios.
