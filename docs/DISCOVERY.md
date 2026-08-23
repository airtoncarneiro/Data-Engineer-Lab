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

Se disponibilizarmos uma empresa fictícia com ambiente técnico reproduzível, dados, documentação e demandas contextualizadas, permitindo que o participante resolva problemas, receba feedback automatizado e seja desafiado de acordo com as competências que demonstra, então ele poderá desenvolver experiência prática mais próxima do cotidiano profissional.

## 4. Público inicial

Principalmente:

- estudantes de Engenharia de Dados;
- profissionais migrando para a área;
- pessoas buscando a primeira oportunidade;
- profissionais que conhecem determinada tecnologia, mas ainda não a utilizaram em projetos próximos do mundo real;
- profissionais experientes que desejam praticar ou aprofundar competências específicas sem percorrer obrigatoriamente desafios introdutórios.

## 5. O que estamos construindo

Um **simulador de trabalho de Engenharia de Dados**, baseado inicialmente em GitHub e containers locais.

O repositório representa uma empresa fictícia e contém seu ambiente, sistemas, dados, documentação e desafios.

Cada desafio representa uma demanda da empresa e é apresentado como um **ticket**.

A jornada do participante não precisa seguir uma sequência fixa de dificuldade. O laboratório deve selecionar desafios adequados à proficiência demonstrada, de forma que participantes com níveis iniciais diferentes continuem sendo desafiados desde o início.

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
- competências ou conceitos-alvo;
- dificuldade estimada;
- pré-requisitos, quando aplicável;
- Learning Resources relacionados, quando aplicável.

### 6.1 Tipos de ticket

Os tickets podem representar diferentes naturezas de trabalho. Tipo de ticket e dificuldade são dimensões independentes: um `bugfix`, por exemplo, pode ser introdutório ou avançado.

Taxonomia inicial:

- `feature`: construir uma nova capacidade, transformação ou entrega;
- `bugfix`: corrigir comportamento incorreto;
- `refactoring`: melhorar uma implementação preservando seu comportamento esperado;
- `performance`: investigar e melhorar desempenho;
- `legacy`: compreender e modificar uma solução herdada ou pouco conhecida;
- `incident`: investigar e recuperar uma falha operacional ou degradação de serviço.

A taxonomia poderá evoluir conforme novos cenários sejam introduzidos, evitando criar tipos sem benefício educacional claro.

### 6.2 Cenários greenfield e brownfield

O simulador deve representar tanto trabalho greenfield quanto brownfield.

Em cenários greenfield, o participante constrói uma solução nova a partir de uma demanda.

Em cenários brownfield, parte da solução já existe e precisa ser compreendida antes de qualquer alteração. O participante pode receber código, SQL, pipeline, configuração, testes ou documentação existentes, incluindo situações plausíveis como:

- documentação parcial ou desatualizada;
- nomes pouco claros;
- lógica complexa ou acoplada;
- testes insuficientes;
- regras de negócio implícitas;
- gargalos de performance;
- comportamento correto que precisa ser preservado durante a mudança.

Esses cenários devem treinar leitura, investigação, manutenção segura e tomada de decisão, não apenas exposição artificial a código propositalmente ruim.

### 6.3 Learning Resources e material de apoio

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

### 6.4 Geração de tickets por IA

A geração assistida de tickets por IA faz parte da direção do MVP.

O gerador deverá receber informações estruturadas, como nível, domínio, competências ou conceitos-alvo e restrições do ambiente, e produzir uma proposta de ticket compatível com as convenções do projeto.

A proposta gerada deverá preservar os princípios pedagógicos do simulador:

- representar uma demanda profissional plausível;
- evitar indicar diretamente a solução técnica;
- incluir contexto, objetivo, requisitos, critérios de aceite e entregáveis;
- relacionar Learning Resources quando aplicável;
- respeitar dificuldade, pré-requisitos e tecnologias disponíveis;
- permitir validação objetiva sempre que possível.

**Geração por IA não significa publicação autônoma.** Tickets oficiais continuam sujeitos a validação antes da publicação no catálogo do simulador.

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

### Diagnóstico inicial

Antes da jornada principal, o laboratório obtém evidências suficientes para estimar as competências relevantes do participante.

O diagnóstico deve ser curto e discriminativo: aumentar rapidamente a dificuldade quando houver domínio aparente e investigar pré-requisitos quando surgirem lacunas. Senioridade declarada e autoavaliação podem ser usadas como sinais auxiliares, mas não substituem evidências de desempenho.

No MVP, esse diagnóstico pode ser simples e não exige um modelo sofisticado de Skill Graph.

### Trabalho

O laboratório seleciona um desafio compatível com as competências já demonstradas e com as evidências ainda necessárias. O participante cria sua implementação.

Participantes diferentes podem receber desafios distintos no mesmo estágio da jornada. "Ticket 1" significa o primeiro desafio daquele participante, não necessariamente o ticket mais fácil do catálogo.

### Entrega

Abre uma Pull Request no próprio fork.

### Validação

GitHub Actions executa testes automatizados e informa se os critérios verificáveis foram atendidos.

Quando aplicável, a validação poderá combinar evidências determinísticas com análise assistida por IA para produzir feedback técnico mais contextualizado.

A revisão por IA deve complementar o CI com perguntas e observações sobre decisões técnicas, legibilidade, manutenibilidade, possíveis edge cases e trade-offs. Critérios objetivos continuam sendo responsabilidade prioritária das validações determinísticas.

### Evidências e adaptação

O resultado da validação produz evidências relacionadas às competências exercitadas pelo desafio. Essas evidências alimentam a seleção do próximo ticket.

Uma resposta correta isolada não deve ser tratada automaticamente como domínio. Sempre que viável, competências importantes devem ser demonstradas mais de uma vez e em contextos diferentes.

A adaptação do MVP deve ser simples e auditável, utilizando metadados dos tickets, diagnóstico inicial, pré-requisitos e evidências acumuladas. Inferência contínua por LLM, Skill Graph sofisticado e Progression Agent autônomo permanecem evoluções pós-MVP.

### Evolução

A jornada SQL inicial é composta por aproximadamente 10 desafios selecionados adaptativamente conforme a proficiência demonstrada. O número representa o tamanho esperado da experiência individual, não a quantidade total de tickets disponíveis no catálogo.

Concluir a jornada não significa automaticamente dominar todas as competências avaliadas. O histórico de evidências deve permitir identificar competências demonstradas, parciais e lacunas.

A evolução pós-MVP é tratada como hipótese no [ROADMAP](ROADMAP.md).

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

A progressão deve considerar três dimensões complementares.

### 9.1 Complexidade tecnológica

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

### 9.2 Natureza do trabalho

O participante também deve evoluir no tipo de problema enfrentado, por exemplo:

1. construir;
2. modificar;
3. corrigir;
4. refatorar;
5. otimizar;
6. investigar;
7. operar e realizar troubleshooting.

Essas dimensões podem ser combinadas. Um ticket pode ser, por exemplo, `SQL + feature`, `SQL + legacy`, `Python + refactoring` ou `Airflow + incident`.

### 9.3 Proficiência demonstrada

A dificuldade adequada é relativa às competências que o participante já demonstrou, e não apenas à ordem de uma lista de tickets.

A progressão deve:

- evitar obrigar participantes experientes a percorrer desafios claramente introdutórios;
- evitar avançar participantes apenas porque um conteúdo foi apresentado ou um único ticket foi concluído;
- utilizar evidências produzidas pelas soluções e validações;
- considerar pré-requisitos e lacunas identificadas;
- revisitar competências quando as evidências forem insuficientes ou contraditórias;
- quando viável, verificar retenção e transferência em problemas diferentes que dependam dos mesmos princípios.

O MVP pode representar proficiência de forma simples, sem depender de senioridade profissional ou de um Skill Graph completo. Modelos mais ricos de mastery, confidence, histórico e diversidade de evidências são possibilidades pós-MVP registradas no [ROADMAP](ROADMAP.md).

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

A avaliação poderá evoluir para um modelo híbrido:

1. testes e verificações determinísticas produzem evidências objetivas;
2. IA analisa essas evidências e, quando necessário, aspectos menos determinísticos;
3. o participante recebe feedback técnico contextualizado;
4. evidências relevantes são associadas às competências exercitadas e podem influenciar a seleção dos próximos desafios.

O LLM não deve ser a única autoridade para critérios objetivos que possam ser verificados deterministicamente.

O histórico de evidências de competência deve começar de forma simples no MVP, sem exigir um modelo sofisticado de Skill Graph.

## 11. Gamificação

Gamificação é uma possibilidade, não requisito do MVP. Eventuais evoluções de gamificação estão registradas no [ROADMAP](ROADMAP.md) e não fazem parte do escopo atual.

## 12. Uso de IA e agentes

IA poderá reduzir o custo de criação e manutenção do simulador e melhorar personalização e feedback.

No MVP, o uso prioritário é:

- gerar propostas estruturadas de tickets a partir de nível, domínio, competências ou conceitos-alvo;
- apoiar a criação de critérios de aceite e entregáveis;
- apoiar feedback técnico sobre entregas, preferencialmente baseado em evidências produzidas por validações determinísticas.

A seleção adaptativa simples do MVP não precisa depender de IA. Quando regras, metadados e evidências determinísticas forem suficientes, devem ser preferidos por serem mais previsíveis e auditáveis.

Possibilidades adicionais de IA, adaptação e automação são hipóteses pós-MVP mantidas no [ROADMAP](ROADMAP.md). Conteúdo gerado por IA deverá passar por validação antes de se tornar parte oficial do simulador.

## 13. MVP

### Objetivo

Validar se o formato "empresa fictícia + tickets + ambiente local + PR + CI" produz uma experiência útil de prática para participantes com níveis iniciais distintos, incluindo seleção simples de desafios baseada em evidências e geração assistida de tickets por IA sem comprometer a qualidade pedagógica.

### Escopo

- uma empresa fictícia;
- PostgreSQL;
- Docker Compose;
- base populada;
- documentação mínima da empresa;
- ticket 000 de onboarding;
- diagnóstico inicial simples e discriminativo;
- catálogo de tickets SQL suficiente para compor jornadas distintas;
- jornada individual de aproximadamente 10 desafios SQL selecionados adaptativamente conforme a proficiência demonstrada;
- metadados mínimos de competências, dificuldade e pré-requisitos nos tickets;
- estrutura para soluções;
- Pull Request no fork;
- GitHub Actions;
- testes automáticos;
- Learning Resources relacionados aos tickets, quando aplicável;
- geração assistida de propostas de tickets por IA;
- estrutura mínima para registrar evidências produzidas pela avaliação e relacioná-las às competências exercitadas;
- seleção simples e auditável do próximo desafio a partir de diagnóstico, metadados e evidências;
- avaliação híbrida entre verificações determinísticas e feedback por IA quando viável.

A taxonomia de tickets e a possibilidade de cenários brownfield fazem parte do modelo do produto, mas não exigem que todos os tipos estejam representados no conjunto inicial do MVP.

### Fora do MVP

- backend próprio;
- autenticação própria;
- portal web;
- ranking global;
- pagamento;
- infraestrutura cloud obrigatória;
- publicação totalmente autônoma de tickets por agentes;
- Skill Graph sofisticado;
- Learner Model avançado com inferência contínua de mastery/confidence;
- inferência automática contínua de nível por LLM;
- Progression Agent decidindo autonomamente a próxima competência;
- geração dinâmica individualizada de todos os desafios;
- Airflow e demais trilhas.

## 14. Questões em aberto

As seguintes decisões serão tratadas durante o detalhamento:

- modelo exato de versionamento dos tickets;
- formato dos arquivos de solução;
- como impedir exposição trivial dos testes esperados;
- estratégia para atualização do fork sem sobrescrever soluções;
- formato e critérios do diagnóstico inicial;
- modelo mínimo de proficiência utilizado no MVP;
- algoritmo/regra de seleção do próximo desafio;
- quantidade e cobertura necessárias do catálogo para suportar jornadas distintas de aproximadamente 10 desafios;
- critérios para considerar evidências suficientes sobre uma competência;
- estratégia de retenção e transferência aplicável ao MVP ou fases posteriores;
- possibilidade de dependências entre tickets;
- schema final para representar tipo de ticket, competências, dificuldade, pré-requisitos e demais metadados;
- quais tipos de ticket estarão presentes no MVP SQL;
- estrutura e localização dos Learning Resources no repositório;
- política para uso de LLMs pelos participantes;
- contrato/schema de entrada e saída do gerador de tickets;
- processo de revisão e aprovação de tickets gerados por IA;
- formato mínimo para armazenar evidências de competência;
- critérios e limites do feedback produzido pelo AI Code Reviewer;
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
