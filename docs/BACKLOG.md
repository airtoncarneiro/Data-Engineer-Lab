# Backlog Inicial

Backlog do MVP SQL organizado para validar primeiro o ciclo adaptativo ponta a ponta. A ordem poderá mudar conforme evidências de implementação, mas componentes de plataforma não devem ser antecipados.

## Épico 1 — Fundação do produto

- [ ] Definir nome e segmento da empresa fictícia.
- [ ] Definir narrativa mínima da empresa.
- [ ] Definir departamentos que solicitarão demandas.
- [ ] Definir sistemas fonte iniciais.
- [ ] Criar glossário de negócio.
- [ ] Criar regras de negócio iniciais.
- [ ] Consolidar convenções de tickets e metadados.

## Épico 2 — PostgreSQL do laboratório

- [ ] Definir domínio inicial adequado aos tickets SQL.
- [ ] Modelar PostgreSQL.
- [ ] Criar migrations/init scripts.
- [ ] Criar massa de dados determinística.
- [ ] Incluir casos de borda necessários aos desafios.
- [ ] Criar processo simples de reset.
- [ ] Criar dicionário de dados.
- [ ] Garantir separação lógica entre dados do laboratório e persistência da jornada, caso compartilhem a mesma instância.

## Épico 3 — Ambiente local

- [ ] Criar `docker-compose.yml`.
- [ ] Configurar PostgreSQL.
- [ ] Criar `.env.example`.
- [ ] Criar comando/documentação de inicialização.
- [ ] Criar healthcheck.
- [ ] Validar execução em ambiente limpo.
- [ ] Garantir que o ciclo determinístico básico não dependa obrigatoriamente de serviços externos.

## Épico 4 — Lab Engine mínimo

- [ ] Definir estrutura inicial do módulo Python.
- [ ] Definir contratos internos entre Web UI e Lab Engine.
- [ ] Criar modelo de estado da jornada.
- [ ] Criar modelo mínimo de Learner Model por competência.
- [ ] Criar registro de evidências.
- [ ] Criar registro de telemetria relevante.
- [ ] Implementar persistência e retomada da jornada.
- [ ] Manter regras pedagógicas fora da camada de UI.

## Épico 5 — PROBE SQL

- [ ] Definir contrato das questões do PROBE.
- [ ] Criar conjunto inicial de questões discriminativas.
- [ ] Implementar seleção adaptativa curta, usando aproximadamente cinco perguntas quando suficientes.
- [ ] Cobrir escrita e compreensão conceitual.
- [ ] Permitir execução real no PostgreSQL quando aumentar a confiança da avaliação.
- [ ] Converter respostas em evidências para o Learner Model.
- [ ] Produzir resultado qualitativo para o participante.

## Épico 6 — Framework de tickets

- [ ] Definir template estruturado de ticket.
- [x] Definir convenção de IDs.
- [ ] Definir níveis de dificuldade.
- [ ] Definir pré-requisitos e dependências.
- [ ] Definir competências-alvo como metadados internos.
- [ ] Definir critérios de aceite verificáveis.
- [x] Definir estrutura de arquivos para solução quando aplicável.
- [ ] Definir contrato para Learning Resources relacionados.

## Épico 7 — Validador SQL local

- [ ] Definir contrato da solução SQL.
- [ ] Criar executor de soluções.
- [ ] Criar framework de testes por ticket.
- [ ] Validar resultado, não apenas texto SQL.
- [ ] Produzir mensagens de erro úteis.
- [ ] Garantir isolamento entre execuções.
- [ ] Avaliar timeout de queries.
- [ ] Produzir evidências objetivas consumíveis pelo Lab Engine.

## Épico 8 — Challenge Selector e Evidence Engine

- [ ] Definir regras auditáveis para seleção do próximo desafio.
- [ ] Considerar objetivo profissional, pré-requisitos, mastery, confidence e evidências necessárias.
- [ ] Implementar atualização do Learner Model a partir das evidências.
- [ ] Diferenciar entrega tecnicamente concluída de domínio demonstrado.
- [ ] Registrar nível de assistência direcionada.
- [ ] Implementar `skip` sem evidência automática negativa.
- [ ] Implementar sinalização de desafio muito fácil/difícil.
- [ ] Definir gatilhos mínimos de recalibração.

## Épico 9 — Web UI local

- [ ] Escolher a solução mínima de Web UI compatível com Python e execução local.
- [ ] Criar inicialização/retomada da jornada.
- [ ] Coletar objetivo profissional.
- [ ] Implementar experiência do PROBE.
- [ ] Exibir ticket corrente.
- [ ] Permitir submissão ou referência da solução SQL.
- [ ] Executar validação e exibir feedback.
- [ ] Permitir assistência e `skip`.
- [ ] Exibir progresso qualitativo quando aplicável.
- [ ] Evitar duplicação de lógica do Lab Engine na interface.

## Épico 10 — Vertical slice adaptativo

Objetivo: provar o núcleo do produto antes de expandir o catálogo.

- [ ] Iniciar o Lab localmente.
- [ ] Registrar objetivo profissional.
- [ ] Executar o PROBE SQL.
- [ ] Criar Learner Model persistente.
- [ ] Selecionar um ticket compatível.
- [ ] Receber uma solução do participante.
- [ ] Validar a solução localmente.
- [ ] Registrar evidências.
- [ ] Atualizar o Learner Model.
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

## Épico 14 — Feedback por IA

- [ ] Integrar feedback por IA sobre evidências determinísticas quando viável.
- [ ] Evitar uso do LLM como autoridade única para critérios verificáveis.
- [ ] Implementar perguntas pós-entrega quando úteis para compreensão e trade-offs.
- [ ] Garantir degradação graciosa quando o recurso de IA estiver indisponível.

## Épico 15 — Validação do produto

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

## Fora do fluxo obrigatório do MVP

Os itens abaixo podem ser usados no desenvolvimento do produto, mas não fazem parte do fluxo operacional obrigatório do participante:

- fork do repositório;
- branch por ticket;
- Pull Request como entrega;
- GitHub Actions como validador da solução do aluno;
- sincronização manual de fork com `upstream`.

O GitHub continua sendo utilizado para desenvolvimento, versionamento e distribuição do produto.

## Depois do MVP

- [ ] Definir próxima trilha com base no feedback.
- [ ] Avaliar Python/ETL.
- [ ] Avaliar Airflow.
- [ ] Avaliar gamificação.
- [ ] Avaliar backend/API e persistência centralizada.
- [ ] Avaliar autenticação e modelo comercial.
- [ ] Avaliar execução remota e testes privados.
- [ ] Evoluir agentes para geração, progressão e revisão de desafios.
