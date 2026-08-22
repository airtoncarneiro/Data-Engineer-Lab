# Discovery do Produto

## 1. Contexto

Pessoas que desejam ingressar em Engenharia de Dados conseguem estudar SQL, Python, Airflow, modelagem e outras tecnologias por diversas fontes. Entretanto, muitas não trabalham na área e, portanto, não possuem oportunidade de aplicar esses conhecimentos em um ambiente integrado.

Exercícios tradicionais normalmente isolam a tecnologia do contexto. O aluno recebe instruções como "faça um SELECT com JOIN" ou "crie uma DAG", mas não vivencia o processo de entender por que aquilo precisa ser feito, quais dados utilizar, quais restrições existem e como a entrega seria validada.

## 2. Problema

Existe uma lacuna entre:

**saber utilizar uma ferramenta**

 e

**saber resolver uma demanda de Engenharia de Dados utilizando essa ferramenta**.

Essa lacuna é especialmente relevante para quem busca a primeira oportunidade profissional.

## 3. Hipótese

Se disponibilizarmos uma empresa fictícia com ambiente técnico reproduzível, dados, documentação e demandas contextualizadas, permitindo que o participante resolva problemas e receba feedback automatizado, então ele poderá desenvolver experiência prática mais próxima do cotidiano profissional.

## 4. Público inicial

Principalmente:

- estudantes de Engenharia de Dados;
- profissionais migrando para a área;
- pessoas buscando a primeira oportunidade;
- profissionais que conhecem determinada tecnologia, mas ainda não a utilizaram em projetos próximos do mundo real.

## 5. O que estamos construindo

Um **simulador de trabalho de Engenharia de Dados**, baseado inicialmente em GitHub e containers locais.

O repositório representa uma empresa fictícia e contém seu ambiente, sistemas, dados, documentação e desafios.

Cada desafio representa uma demanda da empresa e é apresentado como um **ticket**.

## 6. Ticket como unidade de trabalho

O ticket não deve ser apenas um exercício técnico.

Em vez de:

> "Faça uma consulta utilizando GROUP BY."

Preferir:

> "O time comercial precisa identificar clientes ativos há mais de dez anos para uma campanha de relacionamento. Disponibilize a consulta solicitada seguindo os critérios descritos no ticket."

Tickets mais avançados poderão ser deliberadamente menos prescritivos, exigindo investigação e tomada de decisão.

Cada ticket poderá conter:

- contexto;
- solicitante fictício;
- problema ou necessidade;
- critérios de aceite;
- restrições conhecidas;
- artefatos relacionados;
- dependências, quando existirem;
- Learning Resources relacionados, quando aplicável.

### 6.1 Learning Resources e material de apoio

Os tickets podem indicar materiais de apoio para permitir que o participante adquira ou revise conceitos necessários para resolver a demanda sem transformar o simulador em um curso.

Diretrizes:

- a consulta aos materiais é opcional;
- priorizar documentação oficial e fontes técnicas confiáveis;
- os recursos devem ensinar conceitos, não entregar a solução específica do ticket;
- preferir materiais autocontidos e reutilizáveis por diferentes tickets;
- evitar duplicar explicações extensas dentro dos tickets;
- um mesmo Learning Resource pode ser referenciado por vários tickets;
- quando possível, organizar Learning Resources por domínio ou conceito.

Exemplo: se uma demanda exige conhecimento de PostgreSQL Window Functions, o ticket pode referenciar um material sobre Window Functions, mas não deve indicar qual função, particionamento ou ordenação resolve especificamente aquela demanda.

A intenção é reproduzir um comportamento profissional: diante de uma demanda que exige conhecimento ainda não dominado, o participante identifica a lacuna, consulta documentação ou material técnico e aplica o conhecimento ao problema.

## 7. Jornada do participante

### Entrada

O participante encontra o projeto e faz fork do repositório.

### Onboarding

Executa um ticket inicial para:

- conhecer a empresa;
- ler a documentação;
- subir o ambiente;
- conectar-se ao banco;
- executar verificações básicas.

### Trabalho

Seleciona um ticket disponível e cria sua implementação.

### Entrega

Abre uma Pull Request no próprio fork.

### Validação

GitHub Actions executa testes automatizados e informa se os critérios verificáveis foram atendidos.

### Evolução

Após concluir tickets iniciais, o participante recebe problemas progressivamente mais complexos e envolvendo novas tecnologias.

## 8. Modelo Git

### Repositório principal

É mantido pelo projeto e contém a versão oficial do simulador.

### Fork do participante

Cada participante possui seu próprio fork. Dessa forma:

- milhares de pessoas podem trabalhar no mesmo ticket;
- o repositório principal não recebe PRs de participantes;
- cada participante possui seu próprio histórico;
- CI pode executar no fork;
- o fluxo de Pull Request continua sendo praticado.

### Sincronização

Novos tickets e evoluções são publicados no repositório principal.

Participantes sincronizam seus forks com o `upstream` para receber novas versões.

Alterações devem minimizar conflitos com áreas destinadas às soluções dos participantes.

## 9. Progressão

O projeto deverá evoluir em camadas de complexidade.

Possível sequência:

1. SQL e exploração de dados;
2. SQL avançado e performance;
3. modelagem de dados;
4. Python para Engenharia de Dados;
5. ETL/ELT;
6. Airflow;
7. qualidade e observabilidade;
8. Data Lake/Lakehouse;
9. cloud e infraestrutura;
10. incidentes, otimização e arquitetura.

Essa sequência é indicativa e deverá ser refinada após o MVP.

## 10. Validação automática

A validação não deverá depender apenas da comparação textual com uma resposta oficial.

Sempre que possível, deve verificar comportamento e resultado.

Exemplos para SQL:

- consulta executa sem erro;
- resultado contém registros esperados;
- resultado não contém registros inválidos;
- colunas obrigatórias existem;
- regras de negócio foram respeitadas;
- práticas explicitamente proibidas não foram utilizadas;
- eventualmente, limites de performance.

Isso permite múltiplas implementações corretas.

## 11. Gamificação

Gamificação é uma possibilidade, não requisito do MVP.

Evoluções possíveis:

- pontos;
- níveis;
- badges;
- sequência de tickets concluídos;
- especializações;
- ranking.

A gamificação não deve substituir a qualidade técnica nem incentivar soluções artificiais apenas para maximizar pontos.

## 12. Uso de IA e agentes

IA poderá reduzir o custo de criação e manutenção do simulador.

Possíveis papéis futuros:

- gerar propostas de tickets;
- gerar massas de dados;
- criar casos de teste;
- atuar como revisor técnico;
- avaliar aspectos não determinísticos;
- identificar ambiguidades em tickets;
- simular solicitantes e stakeholders;
- produzir variações de cenários;
- validar desafios antes da publicação.

Uma arquitetura multiagente poderá separar responsabilidades, por exemplo:

**Ticket Designer → Data Generator → Test Designer → Reviewer → Publisher**.

Conteúdo gerado por IA deverá passar por validação antes de se tornar parte oficial do simulador.

## 13. MVP

### Objetivo

Validar se o formato "empresa fictícia + tickets + ambiente local + PR + CI" produz uma experiência útil de prática.

### Escopo

- uma empresa fictícia;
- PostgreSQL;
- Docker Compose;
- base populada;
- documentação mínima da empresa;
- ticket 000 de onboarding;
- aproximadamente 10 tickets SQL;
- progressão de dificuldade;
- estrutura para soluções;
- Pull Request no fork;
- GitHub Actions;
- testes automáticos;
- Learning Resources relacionados aos tickets, quando aplicável.

### Fora do MVP

- backend próprio;
- autenticação própria;
- portal web;
- ranking global;
- pagamento;
- infraestrutura cloud obrigatória;
- agentes autônomos publicando tickets;
- Airflow e demais trilhas.

## 14. Questões em aberto

As seguintes decisões serão tratadas durante o detalhamento:

- modelo exato de versionamento dos tickets;
- formato dos arquivos de solução;
- como impedir exposição trivial dos testes esperados;
- estratégia para atualização do fork sem sobrescrever soluções;
- critérios de progressão entre tickets;
- possibilidade de dependências entre tickets;
- estrutura e localização dos Learning Resources no repositório;
- política para uso de LLMs pelos participantes;
- modelo futuro de pontuação;
- identidade e domínio da empresa fictícia;
- licença do projeto.

## 15. Critério de pronto do Discovery v1

O Discovery v1 é considerado suficiente para iniciar o projeto quando permite responder claramente:

- qual problema estamos resolvendo;
- para quem;
- qual experiência queremos proporcionar;
- qual é o diferencial;
- como funciona o fluxo principal;
- o que pertence ao MVP;
- o que explicitamente não pertence ao MVP.

Esses pontos estão definidos neste documento. Questões de implementação deverão ser resolvidas nas fases seguintes sem alterar a visão sem justificativa explícita.
