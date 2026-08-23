# Tasks ativas

Este diretório contém especificações de trabalho prontas para execução por agente.

Cada task deve ser pequena, verificável e complementar ao backlog sem duplicá-lo.

Estrutura recomendada:

```markdown
# <Título da task>

## Objetivo
<resultado esperado>

## Contexto
<informação mínima necessária>

## Escopo
- ...

## Critérios de aceite
- [ ] ...

## Fora de escopo
- ...

## Validações esperadas
- `make test`
- `make lint`
```

Regras:

- use nomes como `001-bootstrap-application.md`;
- não inclua solução detalhada quando a intenção for deixar decisões de implementação para o agente;
- explicite restrições arquiteturais somente quando relevantes;
- critérios de aceite devem ser observáveis;
- uma task não deve reabrir decisão documentada sem declarar isso explicitamente;
- após conclusão e validação, mova a especificação para `../completed/` somente conforme o workflow acordado.
