# Discovery do Produto

## 1. Contexto

Pessoas que desejam ingressar em Engenharia de Dados conseguem estudar SQL, Python, Airflow, modelagem e outras tecnologias por diversas fontes. Entretanto, muitas não trabalham na área e não possuem oportunidade de aplicar esses conhecimentos em um ambiente integrado.

Exercícios tradicionais normalmente isolam a tecnologia do contexto. O aluno recebe instruções como "faça um SELECT com JOIN" ou "crie uma DAG", mas não vivencia o processo de entender por que aquilo precisa ser feito, quais dados utilizar, quais restrições existem e como a entrega seria validada.

## 2. Problema

Existe uma lacuna entre **saber utilizar uma ferramenta** e **saber resolver uma demanda de Engenharia de Dados utilizando essa ferramenta**.

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

O repositório representa uma empresa fictícia e contém seu ambiente, sistemas, dados, documentação e desafios. Cada desafio representa uma demanda da empresa e é apresentado como um **ticket**.

A jornada não segue necessariamente uma sequência fixa de dificuldade. O laboratório deve manter um modelo de competências baseado em evidências e selecionar desafios adequados ao estágio atual, de forma que participantes com níveis iniciais diferentes sejam desafiados desde o início.

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
- dependências;
- competências técnicas e profissionais alvo, mantidas como metadados internos durante a execução quando revelá-las produzir pistas;
- dificuldade estimada;
- pré-requisitos;
- Learning Resources relacionados.

### 6.1 Tipos de ticket

Tipo e dificuldade são dimensões independentes. Taxonomia inicial:

- `feature`: construir nova capacidade, transformação ou entrega;
- `bugfix`: corrigir comportamento incorreto;
- `refactoring`: melhorar implementação preservando comportamento esperado;
- `performance`: investigar e melhorar desempenho;
- `legacy`: compreender e modificar solução herdada ou pouco conhecida;
- `incident`: investigar e recuperar falha operacional ou degradação.

A taxonomia poderá evoluir conforme novos cenários sejam introduzidos, evitando tipos sem benefício educacional claro.

### 6.2 Cenários greenfield e brownfield

O simulador deve representar trabalho greenfield e brownfield.

Em cenários greenfield, o participante constrói uma solução nova. Em cenários brownfield, parte da solução já existe e precisa ser compreendida antes da alteração. O participante pode receber código, SQL, pipeline, configuração, testes ou documentação existentes, incluindo situações plausíveis como documentação parcial, regras implícitas, testes insuficientes, gargalos e comportamento que precisa ser preservado.

Esses cenários devem treinar leitura, investigação, manutenção segura e tomada de decisão, não exposição artificial a código propositalmente ruim.

### 6.3 Learning Resources e assistência

Learning Resources permitem adquirir ou revisar conceitos necessários sem transformar o simulador em curso.

Diretrizes:

- consulta opcional;
- priorizar documentação oficial e fontes técnicas confiáveis;
- ensinar conceitos, não a solução específica;
- preferir materiais autocontidos, reutilizáveis e organizados por domínio ou conceito;
- evitar duplicar explicações extensas nos tickets.

Quando o participante tiver dificuldade, o Lab pode oferecer investigação/autocorreção, pistas graduais, decomposição e Learning Resources. Pistas devem possuir uma base validada e podem ter sua apresentação adaptada por IA dentro de limites definidos.

O uso de assistência direcionada não invalida a entrega, mas pode reduzir a força da evidência de domínio. Pesquisa, documentação e IA utilizadas livremente como ferramentas profissionais não devem ser tratadas como infração.

A seleção adaptativa de Learning Resources permanece uma decisão em aberto.

### 6.4 Geração e catálogo de tickets

O catálogo é evolutivo. O mecanismo deve priorizar desafios já qualificados quando houver cobertura adequada e pode gerar um novo candidato por IA quando o Learner Model exigir uma combinação de competências/dificuldade não atendida pelo catálogo.

O gerador recebe informações estruturadas, como domínio, competências-alvo, dificuldade, pré-requisitos, objetivo da jornada e restrições do ambiente. O candidato deve representar demanda profissional plausível, evitar revelar a solução, incluir critérios verificáveis e respeitar tecnologias e dados disponíveis.

**Gerado não significa publicado.** O lifecycle conceitual é:

`candidate -> validated -> trialed -> published`

Antes do primeiro uso, candidatos passam por validações automáticas. Revisão humana é necessária quando subjetividade, risco ou baixa confiança impedirem validação automática suficiente. Tickets integralmente verificáveis podem entrar em trial sem revisão humana obrigatória.

A promoção para `published` exige um número mínimo de execuções reais e evidências de qualidade; o valor exato será definido na implementação. Tickets publicados continuam acumulando telemetria e podem ser sinalizados para revisão quando surgirem ambiguidades, dificuldade mal calibrada ou falhas inesperadas.

## 7. Jornada do participante

### Entrada e onboarding

O participante encontra o projeto, prepara seu ambiente e executa o onboarding para conhecer a empresa, documentação, banco e fluxo de trabalho.

### Objetivo profissional

Antes do PROBE, o participante informa seu objetivo profissional. O objetivo pode influenciar a profundidade do diagnóstico e a priorização posterior de competências, sem substituir evidências de proficiência nem eliminar fundamentos essenciais.

### PROBE técnico

Cada nova jornada possui seu próprio PROBE técnico. Para SQL, ele avalia escrita e compreensão conceitual; competências profissionais são observadas principalmente durante os tickets.

O PROBE deve ser curto, discriminativo e adaptativo, usando aproximadamente cinco perguntas quando forem suficientes: começa com questões que diferenciem níveis, aumenta rapidamente a dificuldade diante de domínio aparente e investiga pré-requisitos quando encontra lacunas.

O diagnóstico é híbrido: pode usar perguntas conversacionais, análise de SQL e respostas abertas, recorrendo à execução real no PostgreSQL quando isso aumentar a confiança da inferência.

O resultado apresentado ao participante é qualitativo. Scores internos não precisam ser expostos.

### Learner Model

O Lab mantém um Learner Model persistente e genérico por competência, reutilizável por futuras jornadas. O modelo mínimo do MVP registra:

- `skill`;
- categoria da competência: técnica ou profissional;
- `mastery`;
- `confidence`;
- quantidade de evidências.

Uma resposta correta isolada não comprova domínio. Múltiplas evidências e aplicação em contextos diferentes aumentam a confiança. O modelo pode evoluir futuramente com misconceptions, recência, diversidade de contextos e Skill Graph.

### Seleção do desafio

O próximo desafio considera Learner Model, objetivo profissional, pré-requisitos, competências prioritárias e evidências ainda necessárias.

O mecanismo é híbrido: regras determinísticas e auditáveis definem prioridades e restrições; IA pode apoiar seleção, adaptação ou geração do desafio dentro desses limites.

As competências-alvo não são apresentadas antes do ticket quando isso puder induzir a solução. O participante recebe a demanda profissional.

### Trabalho e autonomia

O participante pode utilizar documentação, pesquisa e IA livremente.

Pode também:

- pular um ticket; o `skip` é informação operacional e não evidência automática de falta de competência;
- sinalizar que um desafio está muito fácil; isso é autoavaliação e precisa ser confirmada por desempenho posterior;
- sinalizar dificuldade excessiva e escolher receber pista, Learning Resource ou decomposição antes de trocar de desafio.

### Entrega e validação

A entrega técnica é validada prioritariamente por testes determinísticos. IA pode complementar com feedback contextualizado e perguntas sobre decisões, comportamento da solução, edge cases e trade-offs.

Uma entrega pode estar tecnicamente concluída enquanto determinada competência permanece sem evidências suficientes de domínio.

### Evidências e adaptação

A avaliação produz evidências associadas às competências exercitadas. O peso/confiança da evidência pode considerar o nível de assistência direcionada utilizado.

Tempo gasto é telemetria, não evidência de proficiência no MVP.

Após evidências relevantes, o Learner Model é atualizado e alimenta a seleção do próximo desafio. A adaptação deve fortalecer lacunas prioritárias e também revisitar competências fortes para confirmar consistência e transferência.

O participante pode solicitar um PROBE curto de recalibração. O próprio Lab também pode iniciá-lo quando detectar má calibração persistente ou baixa confiança. A recalibração automática ocorre depois da conclusão do ticket corrente e antes do próximo.

### Continuidade

Learner Model, evidências e estado da jornada são persistentes. O participante pode interromper e continuar posteriormente de onde parou. No MVP, existe uma jornada ativa por vez.

### Evolução e conclusão

A jornada SQL possui aproximadamente 10 desafios como referência de duração, não como quantidade fixa nem critério de conclusão.

A evolução é medida tanto pela mudança nas competências demonstradas quanto pela capacidade de aplicá-las em problemas progressivamente mais exigentes e em contextos diferentes.

A jornada é considerada concluída quando houver evidências suficientes de evolução nas competências-alvo e transferência. Lacunas remanescentes permanecem explícitas e podem originar uma extensão adaptativa opcional.

Ao final, o participante recebe um perfil qualitativo por competência, mostrando evolução entre entrada e saída sem reduzir tudo a um único nível. Detalhes de competências e evidências podem ser consultados sob demanda.

A próxima jornada é recomendada com base no perfil final, lacunas, pré-requisitos e objetivo profissional; a escolha final permanece com o participante.

## 8. Modelo Git

### Repositório principal

É mantido pelo projeto e contém a versão oficial do simulador.

### Fork do participante

Cada participante possui seu próprio fork, permitindo histórico e CI próprios sem receber PRs de participantes no repositório principal.

### Sincronização

Novos tickets e evoluções são publicados no repositório principal. Participantes sincronizam seus forks com o `upstream`. Alterações devem minimizar conflitos com áreas destinadas às soluções.

## 9. Progressão

A progressão considera três dimensões complementares.

### 9.1 Complexidade tecnológica

Possível sequência: SQL e exploração; SQL avançado e performance; modelagem; Python; ETL/ELT; Airflow; qualidade/observabilidade; Data Lake/Lakehouse; cloud/infraestrutura; incidentes, otimização e arquitetura.

### 9.2 Natureza do trabalho

O participante evolui também no tipo de problema: construir, modificar, corrigir, refatorar, otimizar, investigar e operar/troubleshooting.

### 9.3 Proficiência demonstrada

A dificuldade adequada é relativa às competências demonstradas, não à ordem de uma lista.

A progressão deve evitar desafios claramente introdutórios para participantes experientes, evitar avanço por simples conclusão de conteúdo, considerar pré-requisitos/lacunas, acumular múltiplas evidências e verificar transferência em contextos diferentes.

Competências técnicas e profissionais são dimensões distintas do Learner Model e podem participar da seleção do próximo ticket. Um participante pode dominar SQL técnico e ainda precisar desenvolver investigação, debugging, interpretação de requisitos ou raciocínio sobre trade-offs.

## 10. Validação automática

A validação não deve depender apenas da comparação textual com uma resposta oficial. Sempre que possível, deve verificar comportamento e resultado.

Para SQL, exemplos incluem execução sem erro, registros esperados/invalidos, colunas obrigatórias, regras de negócio, restrições explícitas e limites de performance quando aplicáveis.

A avaliação híbrida segue a prioridade:

1. testes e verificações determinísticas produzem evidências objetivas;
2. IA analisa evidências e aspectos menos determinísticos quando necessário;
3. perguntas pós-entrega podem verificar compreensão;
4. evidências são associadas às competências e atualizam o Learner Model.

O LLM não deve ser autoridade única para critérios verificáveis deterministicamente.

## 11. Gamificação

Gamificação é possibilidade, não requisito do MVP. Evoluções permanecem no [ROADMAP](ROADMAP.md).

## 12. Uso de IA e agentes

No MVP, IA pode apoiar geração controlada de candidatos, adaptação de pistas, seleção/construção de desafios dentro de restrições e feedback técnico.

Regras e validações determinísticas devem ser preferidas quando suficientes por serem mais previsíveis e auditáveis. Skill Graph sofisticado, Progression Agent autônomo e arquitetura multiagente permanecem evoluções pós-MVP.

## 13. MVP

### Objetivo

Validar se o formato de simulador profissional consegue desafiar participantes com níveis iniciais distintos por meio de um ciclo adaptativo baseado em evidências, sem exigir uma plataforma sofisticada.

### Escopo

- empresa fictícia e PostgreSQL local reproduzível;
- ticket 000 de onboarding;
- objetivo profissional + PROBE SQL curto e adaptativo;
- Learner Model mínimo, genérico e persistente;
- competências técnicas e profissionais separadas;
- catálogo SQL suficiente para jornadas distintas;
- jornada de aproximadamente 10 desafios, com conclusão por evidências de evolução/transferência;
- seleção híbrida e auditável do próximo desafio;
- testes determinísticos e feedback assistido por IA;
- perguntas pós-entrega quando necessárias para verificar compreensão;
- assistência progressiva e registro de seu impacto na força das evidências;
- persistência e retomada da jornada;
- perfil final qualitativo e recomendação da próxima jornada;
- geração de desafios candidatos e lifecycle controlado até publicação;
- Learning Resources relacionados aos tickets quando aplicável;
- teste com primeiros usuários.

### Fora do MVP

- backend/autenticação próprios;
- pagamento, ranking global e infraestrutura cloud obrigatória;
- múltiplas jornadas simultâneas;
- Skill Graph sofisticado;
- Progression Agent autônomo;
- inferência irrestrita por LLM;
- arquitetura multiagente;
- Airflow e demais trilhas.

## 14. Questões em aberto

Permanecem para detalhamento:

- modelo exato de versionamento dos tickets;
- formato dos arquivos de solução e proteção dos testes esperados;
- estratégia de atualização do fork sem sobrescrever soluções;
- taxonomia e lista inicial de competências técnicas/profissionais do MVP;
- fórmula inicial de atualização de `mastery` e `confidence`;
- thresholds de evidência para progressão e conclusão;
- regras determinísticas do Challenge Engine;
- quantidade/cobertura inicial do catálogo;
- valor mínimo de execuções reais para `candidate -> published`;
- critérios objetivos de risco que exigem revisão humana;
- estrutura e localização dos Learning Resources;
- se e como Learning Resources serão selecionados adaptativamente;
- schema do gerador e do lifecycle de tickets;
- critérios e limites do AI Code Reviewer;
- identidade e domínio da empresa fictícia;
- licença do projeto.
