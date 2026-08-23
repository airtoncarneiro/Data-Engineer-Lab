# Princípios do Projeto

Estes princípios orientam decisões de produto, conteúdo e arquitetura.

## 1. Prática antes de ensino

O simulador fornece contexto, problema, ambiente e feedback. Não pretende substituir cursos ou documentação técnica.

## 2. Demandas, não exercícios

O participante recebe tickets representando necessidades de uma empresa fictícia. A tecnologia aparece como meio para resolver o problema.

## 3. Ambiente próximo do trabalho real

Sempre que o custo for razoável, utilizar práticas e ferramentas encontradas no cotidiano profissional: Git, Pull Requests, containers, banco de dados, testes e CI/CD.

## 4. Progressão de complexidade

Os primeiros tickets devem permitir adaptação ao ambiente. Os seguintes aumentam gradualmente ambiguidade, volume, dependências e responsabilidade técnica.

A progressão deve considerar tanto a complexidade tecnológica quanto a natureza do trabalho executado: construir, modificar, corrigir, refatorar, otimizar, investigar e operar.

## 5. Validar comportamento, não resposta textual

Sempre que possível, testar o resultado produzido pela solução em vez de exigir uma implementação idêntica à solução de referência.

## 6. Múltiplas soluções podem estar corretas

Problemas reais possuem trade-offs. O simulador deve aceitar alternativas tecnicamente válidas quando os critérios de aceite forem atendidos.

## 7. Contexto acumulativo

A empresa fictícia deve possuir continuidade. Sistemas, tabelas, regras e decisões anteriores reaparecem em novos tickets.

## 8. O participante é responsável pela investigação

Nem toda informação necessária precisa estar no enunciado. Documentação, schema, código e dados fazem parte da investigação.

## 9. Orientar sem ensinar a solução

O simulador não é um curso. Os desafios podem fornecer Learning Resources e referências técnicas para que o participante adquira ou revise o conhecimento necessário, mas esses materiais não devem revelar diretamente a solução da atividade.

Os recursos devem priorizar conceitos reutilizáveis e fontes confiáveis, especialmente documentação oficial. O participante decide se precisa consultá-los.

## 10. Nem todo trabalho começa do zero

O laboratório deve representar cenários greenfield e brownfield.

Tickets podem exigir compreensão, correção, refatoração, otimização ou evolução de código e pipelines existentes, inclusive quando houver documentação incompleta, nomenclatura ruim, lógica confusa, testes insuficientes ou decisões legadas.

O objetivo não é produzir código ruim artificialmente, mas reproduzir situações plausíveis em que o participante precisa entender o estado atual antes de alterá-lo com segurança.

## 11. Feedback automatizado primeiro

O projeto deve escalar sem depender de revisão humana para cada participante.

Quando houver revisão assistida por IA, ela deve complementar a validação determinística com feedback sobre legibilidade, manutenibilidade, trade-offs, edge cases e decisões técnicas. A IA não deve substituir testes objetivos quando o comportamento puder ser verificado deterministicamente.

## 12. Conteúdo é o principal ativo

Infraestrutura deve permanecer simples sempre que possível. A qualidade da empresa simulada, dos dados, dos tickets e dos critérios de validação é mais importante que uma plataforma sofisticada.

## 13. MVP antes de plataforma

Não construir portal, backend, ranking ou arquitetura distribuída antes de validar que a experiência básica gera valor.

## 14. IA aumenta escala, não reduz qualidade

Agentes poderão apoiar geração e revisão de conteúdo, mas desafios oficiais precisam ser coerentes, reproduzíveis e tecnicamente verificáveis.
