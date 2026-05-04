# A história por trás do Feature Knowledge Agent System

## O problema invisível

Toda equipa de desenvolvimento vive a mesma ilusão:

> "O código está no Git, então o conhecimento está seguro."

Mas isso quase nunca é verdade.

O código guarda **o que foi feito**.

Raramente guarda **por que foi feito**, **o que não pode mudar**,
**quais regras de negócio estão escondidas ali** e **quais efeitos
colaterais existem**.

E é aí que nasce o problema.

Imagine um hospital.

Um sistema de marcação de consultas foi evoluído durante dois anos.

Vários developers tocaram nele.

Mas houve um developer específico --- Miguel --- que passou seis meses
construindo a lógica de agendamento.

Miguel aprendeu, na prática, coisas que não estavam em documento nenhum:

-   pacientes oncológicos têm prioridade especial
-   determinados seguros exigem autorização prévia
-   alguns médicos não podem ser agendados em blocos consecutivos por
    regulamentação interna
-   certos tipos de consultas exigem preparação mínima de 24 horas

Nada disso estava completamente documentado.

Porque o prazo era curto.

Porque a prioridade era entregar.

Porque o conhecimento foi ficando embutido no código.

O código funcionava.

Até que Miguel saiu do projeto.

------------------------------------------------------------------------

## O incidente

Três meses depois, uma nova developer, Sofia, recebeu uma task simples:

> "Melhorar performance do agendamento."

Ela identificou uma validação aparentemente redundante:

``` java
if (patient.hasPriorityCondition()) {
   validateSpecialSchedulingRules();
}
```

Parecia custosa.

Parecia desnecessária.

Parecia duplicada.

Removeu.

Todos os testes passaram.

Code review aprovado.

Deploy realizado.

Dois dias depois:

-   pacientes prioritários começaram a ser agendados incorretamente
-   hospitais reclamaram
-   auditorias foram abertas
-   o SLA foi quebrado

O problema?

Aquela validação representava uma regra crítica de negócio.

Mas ninguém sabia.

Miguel sabia.

E Miguel não estava mais lá.

------------------------------------------------------------------------

## O padrão se repete em bancos

Agora imagine um banco.

Joana implementou a feature de autorização de transferências.

Durante meses, aprendeu nuances como:

-   certas contas premium possuem limites dinâmicos
-   transferências internacionais precisam de antifraude adicional
-   transações acima de certos thresholds exigem dupla autorização
-   operações repetidas precisam ser idempotentes

Essas regras estavam espalhadas em:

-   services
-   validators
-   interceptors
-   listeners
-   testes

Joana entendia.

A equipa não.

Meses depois, alguém alterou uma regra de retry.

Sem perceber, quebrou a idempotência.

O sistema debitou duas vezes.

O cliente abriu reclamação.

O banco teve prejuízo.

------------------------------------------------------------------------

## O verdadeiro problema

Não é código.

Não é documentação.

Não é code review.

É a fragilidade do conhecimento humano.

Hoje o conhecimento crítico vive em três lugares:

1.  na cabeça de quem implementou
2.  em decisões não documentadas
3.  em comportamentos inferidos pelos testes

E isso cria dependência humana.

O sistema fica refém de especialistas.

O negócio fica refém da memória.

A manutenção vira arqueologia.

------------------------------------------------------------------------

## A mudança de paradigma

E se cada funcionalidade pudesse "explicar a si mesma"?

E se cada feature tivesse um guardião?

E se toda regra descoberta durante a implementação fosse capturada?

E se o conhecimento tácito fosse convertido em conhecimento operacional?

Nasce então um novo conceito:

**Feature Knowledge Agent**

Não um agente de IA genérico.

Mas um agente especialista naquele domínio.

Um agente que conhece:

-   fronteiras da feature
-   contratos de entrada e saída
-   invariantes
-   regras de negócio
-   dependências
-   efeitos colaterais
-   testes comportamentais

------------------------------------------------------------------------

## Como funciona na prática

Quando um developer implementa uma feature, ele não entrega apenas
código.

Entrega conhecimento.

O sistema extrai:

-   intenção funcional
-   contratos
-   invariantes
-   exemplos
-   fluxos
-   decisões

Esse conhecimento é versionado junto ao código.

E um agente local aprende aquilo.

Depois disso:

Quando alguém altera a feature:

o agente revisa.

Pergunta:

> Isso quebra alguma regra?

> Isso altera algum contrato?

> Isso viola algum comportamento esperado?

> Isso impacta integrações?

> Isso remove uma proteção crítica?

Se sim:

o merge falha.

------------------------------------------------------------------------

## O agente documentador

Mas há mais.

O mesmo conhecimento alimenta outro agente.

O agente documentador.

Ele observa:

-   implementação
-   testes
-   contratos
-   fluxos

E gera documentação viva.

Não documentação manual.

Mas documentação derivada do comportamento real.

------------------------------------------------------------------------

## O resultado

Antes:

Pessoa → Conhecimento → Código → Perda de contexto

Depois:

Pessoa → Conhecimento → Estrutura → Agente → Proteção → Documentação →
Continuidade

------------------------------------------------------------------------

## O impacto organizacional

Isso muda a forma de construir software.

Antes:

"Quem mexeu nisso?"

Depois:

"O agente desse domínio sabe."

Antes:

"Precisamos falar com quem implementou."

Depois:

"O conhecimento já foi capturado."

Antes:

"Vamos descobrir no código."

Depois:

"Vamos consultar o agente."

------------------------------------------------------------------------

## O objetivo final

Construir sistemas onde o conhecimento não morre com a rotatividade.

Onde regras críticas não ficam escondidas.

Onde code review entende negócio.

Onde documentação nasce da implementação.

Onde manutenção deixa de ser adivinhação.

Porque no fim:

o maior risco de um sistema não é bug.

É conhecimento perdido.

E conhecimento perdido é dívida operacional invisível.
