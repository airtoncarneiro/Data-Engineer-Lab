# Princípios do Data Engineer Lab

## 1. Learning by doing

O aprendizado acontece principalmente pela resolução de problemas contextualizados, não pela exposição passiva a conteúdo.

O participante deve interpretar demandas, investigar dados, tomar decisões e construir soluções.

## 2. Realismo profissional

Os desafios devem se aproximar de situações encontradas no trabalho de Engenharia de Dados.

Isso inclui:

- requisitos incompletos ou distribuídos em artefatos diferentes;
- regras de negócio;
- dados imperfeitos;
- restrições técnicas;
- manutenção de soluções existentes;
- investigação e troubleshooting;
- necessidade de justificar decisões e trade-offs.

Realismo não significa introduzir complexidade artificial. Cada elemento deve possuir função educacional ou representar uma restrição plausível do problema.

## 3. Demanda antes da técnica

Tickets devem descrever problemas e necessidades, não instruções sobre qual construção técnica usar.

Evitar:

> Use uma window function para obter o resultado.

Preferir:

> O time precisa identificar, para cada cliente, a compra mais recente e o valor correspondente.

A técnica necessária deve ser consequência do problema.

## 4. Progressão baseada em evidências

O participante não progride apenas porque concluiu uma quantidade fixa de conteúdo.

A progressão deve considerar evidências acumuladas sobre competências técnicas e profissionais, incluindo aplicação em contextos diferentes.

Uma evidência isolada pode indicar desempenho pontual; múltiplas evidências aumentam a confiança sobre domínio e transferência.

## 5. Adaptação simples e auditável

O MVP deve adaptar a experiência sem depender de mecanismos opacos ou excessivamente sofisticados.

Regras determinísticas devem definir restrições, prioridades e pré-requisitos sempre que possível. IA pode complementar seleção, geração e feedback dentro desses limites.

Skill Graph completo, Progression Agent autônomo e inferência irrestrita por LLM não são requisitos iniciais.

## 6. Avaliação determinística primeiro

Critérios objetivos devem ser verificados por mecanismos objetivos.

Para SQL, isso pode incluir:

- execução sem erro;
- resultado esperado;
- regras de negócio;
- presença ou ausência de registros;
- estrutura exigida;
- limites de performance quando aplicáveis.

IA deve complementar a avaliação em aspectos como raciocínio, legibilidade, decisões, edge cases e trade-offs, sem substituir testes quando estes forem viáveis.

## 7. Entrega técnica não é sinônimo de domínio

Uma solução pode passar nas verificações técnicas e ainda produzir evidências insuficientes para afirmar domínio de determinada competência.

O Lab deve separar:

- conclusão técnica do ticket;
- evidências produzidas;
- confiança no domínio das competências relacionadas.

## 8. Autonomia do participante

Pesquisa, documentação e IA fazem parte do trabalho profissional e são permitidas.

O produto não deve tentar impedir artificialmente o uso dessas ferramentas.

Assistência direcionada fornecida pelo próprio Lab — pistas, decomposição ou Learning Resources — pode ser registrada para ponderar a força da evidência, sem invalidar automaticamente a entrega.

## 9. Dificuldade relativa ao participante

Dificuldade não deve ser tratada apenas como propriedade fixa do ticket.

Um mesmo desafio pode ser trivial para um participante e exigente para outro. O Lab deve utilizar dificuldade estimada, pré-requisitos e Learner Model para selecionar problemas adequados ao estágio atual.

## 10. Greenfield e brownfield

O trabalho real inclui construir soluções novas e modificar sistemas existentes.

O laboratório deve incluir progressivamente:

- implementação nova;
- correção de bugs;
- refatoração;
- otimização;
- investigação;
- manutenção de código ou SQL legado;
- incidentes e recuperação operacional.

Brownfield deve exercitar compreensão e manutenção segura, não expor código artificialmente ruim apenas para aumentar dificuldade.

## 11. Persistência e continuidade

O participante deve poder interromper e retomar uma jornada sem perder seu estado.

No MVP, persistência local é suficiente para:

- jornada ativa;
- objetivo profissional;
- Learner Model;
- evidências;
- telemetria necessária.

Centralização, contas e sincronização remota são evoluções posteriores.

## 12. Web UI como interface; Lab Engine como núcleo

No MVP, a Web UI local é a interface principal do participante.

A lógica de jornada, avaliação, progressão e evidências pertence ao Lab Engine e não deve ficar acoplada à camada visual.

Essa separação deve existir em código e contratos internos mesmo sem uma API de rede independente.

## 13. Local primeiro

O MVP deve validar o valor educacional e o ciclo adaptativo em ambiente local antes de introduzir infraestrutura de plataforma.

A solução inicial deve priorizar:

- execução reproduzível;
- baixo custo operacional;
- simplicidade de instalação e diagnóstico;
- independência de serviços externos para validações determinísticas básicas;
- capacidade de evoluir posteriormente sem exigir arquitetura distribuída desde o início.

Autenticação, backend centralizado, execução remota, multiusuário e monetização somente devem ser introduzidos quando houver necessidade comprovada.

## 14. GitHub é infraestrutura de desenvolvimento, não requisito pedagógico

O GitHub é a fonte de verdade do código e documentação do produto e pode hospedar CI do próprio projeto.

Fork, branch por ticket, Pull Request e GitHub Actions não fazem parte do fluxo operacional obrigatório do participante no MVP.

O aluno deve poder executar uma jornada, resolver desafios e receber validação pela aplicação local sem depender de operações Git.

## 15. Catálogo evolutivo e geração controlada

O catálogo deve crescer conforme necessidades reais de cobertura de competências e faixas de proficiência.

Quando não houver desafio adequado, IA pode gerar um candidato dentro de um contrato estruturado.

Gerado não significa publicado. O lifecycle mínimo é:

`candidate -> validated -> trialed -> published`

Validação automática deve anteceder o primeiro uso. Revisão humana é necessária quando risco, subjetividade ou baixa confiança impedirem qualificação automática suficiente.

## 16. Learning Resources não são soluções

Learning Resources devem ensinar conceitos necessários sem entregar diretamente a solução de um ticket.

Devem ser:

- opcionais;
- objetivos;
- reutilizáveis;
- preferencialmente autocontidos;
- organizados por domínio ou conceito;
- independentes da implementação específica do desafio.

## 17. Simplicidade antes de sofisticação

Componentes devem ser introduzidos quando resolvem uma necessidade concreta do estágio atual.

Evitar antecipar:

- microserviços;
- múltiplos bancos sem necessidade;
- API remota apenas por abstração arquitetural;
- agentes autônomos complexos;
- infraestrutura cloud;
- sistemas avançados de proteção de testes;
- mecanismos de gamificação sem evidência de valor.

## 18. Vertical slice antes de amplitude

A primeira implementação deve provar o ciclo principal ponta a ponta:

`objetivo -> PROBE -> Learner Model -> ticket -> solução -> validação -> evidência -> atualização -> próximo ticket`

Somente depois desse fluxo funcionar de forma reproduzível deve haver expansão significativa do catálogo ou aumento da sofisticação adaptativa.

## 19. Evolução incremental

Cada fase deve produzir algo utilizável e avaliável.

O produto deve evoluir a partir de feedback de participantes reais, evitando construir uma plataforma ampla antes de comprovar que o núcleo da experiência entrega valor.
