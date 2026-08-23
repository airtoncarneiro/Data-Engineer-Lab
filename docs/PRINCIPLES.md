# Princípios do Projeto

Estes princípios orientam decisões de produto, conteúdo e arquitetura.

## 1. Prática antes de ensino

O simulador fornece contexto, problema, ambiente e feedback. Não pretende substituir cursos ou documentação técnica.

## 2. Demandas, não exercícios

O participante recebe tickets representando necessidades de uma empresa fictícia. A tecnologia aparece como meio para resolver o problema.

## 3. Ambiente próximo do trabalho real

Sempre que o custo for razoável, utilizar práticas e ferramentas encontradas no cotidiano profissional: Git, Pull Requests, containers, banco de dados, testes e CI/CD.

Pesquisa, documentação e IA fazem parte das ferramentas disponíveis ao participante. O laboratório deve avaliar a entrega e a compreensão demonstrada, não tentar fiscalizar quais fontes foram utilizadas.

## 4. Progressão baseada em desafio adequado

A progressão deve considerar tanto a complexidade tecnológica quanto a natureza do trabalho executado: construir, modificar, corrigir, refatorar, otimizar, investigar e operar.

O participante deve receber desafios compatíveis com as competências já demonstradas, de forma que a jornada continue exigindo investigação, raciocínio e evolução independentemente do nível inicial.

A posição de um ticket na jornada não deve ser tratada como sinônimo de dificuldade absoluta. Participantes diferentes podem receber desafios distintos no mesmo estágio quando suas evidências de proficiência forem diferentes.

## 5. Evidência antes de classificação

A proficiência deve ser inferida prioritariamente a partir do desempenho demonstrado em problemas e das evidências produzidas pela avaliação.

Senioridade declarada, autoavaliação ou uma única resposta correta podem ser sinais auxiliares, mas não devem constituir prova suficiente de domínio. Sempre que viável, o simulador deve acumular múltiplas evidências e observar aplicação em contextos diferentes antes de considerar uma competência consolidada.

Uma entrega tecnicamente correta e domínio da competência são conceitos distintos. Assistência direcionada pode reduzir a força da evidência sem invalidar a entrega.

## 6. Validar comportamento, não resposta textual

Sempre que possível, testar o resultado produzido pela solução em vez de exigir uma implementação idêntica à solução de referência.

## 7. Múltiplas soluções podem estar corretas

Problemas reais possuem trade-offs. O simulador deve aceitar alternativas tecnicamente válidas quando os critérios de aceite forem atendidos.

## 8. Contexto acumulativo

A empresa fictícia deve possuir continuidade. Sistemas, tabelas, regras e decisões anteriores reaparecem em novos tickets.

## 9. O participante é responsável pela investigação

Nem toda informação necessária precisa estar no enunciado. Documentação, schema, código e dados fazem parte da investigação.

## 10. Orientar sem ensinar a solução

O simulador não é um curso. Os desafios podem fornecer Learning Resources e referências técnicas para que o participante adquira ou revise o conhecimento necessário, mas esses materiais não devem revelar diretamente a solução da atividade.

Os recursos devem priorizar conceitos reutilizáveis e fontes confiáveis, especialmente documentação oficial. O participante decide se precisa consultá-los.

Quando houver dificuldade, o laboratório pode oferecer investigação guiada, pistas progressivas, decomposição e Learning Resources. A assistência deve favorecer autocorreção antes de revelar a solução.

## 11. Nem todo trabalho começa do zero

O laboratório deve representar cenários greenfield e brownfield.

Tickets podem exigir compreensão, correção, refatoração, otimização ou evolução de código e pipelines existentes, inclusive quando houver documentação incompleta, nomenclatura ruim, lógica confusa, testes insuficientes ou decisões legadas.

O objetivo não é produzir código ruim artificialmente, mas reproduzir situações plausíveis em que o participante precisa entender o estado atual antes de alterá-lo com segurança.

## 12. Feedback automatizado primeiro

O projeto deve escalar sem depender de revisão humana para cada participante.

Quando houver revisão assistida por IA, ela deve complementar a validação determinística com feedback sobre legibilidade, manutenibilidade, trade-offs, edge cases, decisões técnicas e compreensão da solução. A IA não deve substituir testes objetivos quando o comportamento puder ser verificado deterministicamente.

## 13. Conteúdo é o principal ativo

Infraestrutura deve permanecer simples sempre que possível. A qualidade da empresa simulada, dos dados, dos tickets e dos critérios de validação é mais importante que uma plataforma sofisticada.

## 14. MVP antes de plataforma

Não construir portal, backend, ranking ou arquitetura distribuída antes de validar que a experiência básica gera valor.

## 15. IA aumenta escala, não reduz qualidade

Agentes poderão apoiar geração, adaptação e revisão de conteúdo. Desafios reutilizáveis precisam ser coerentes, reproduzíveis e tecnicamente verificáveis.

Conteúdo gerado por IA deve ser tratado inicialmente como candidato. Sua promoção ao catálogo deve depender de validações compatíveis com o risco e de evidências de uso real, sem exigir revisão humana quando critérios objetivos e mecanismos automáticos forem suficientes.
