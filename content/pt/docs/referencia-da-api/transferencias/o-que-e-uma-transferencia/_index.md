---
title: "O Que É Uma Transferência"
slug: "o-que-é-uma-transferência"
draft: false
weight: 1
---

---
<br>

### Conceito
---

<br>

Oferecemos uma API de Transferências, na qual permite-se efetuar a movimentação de fundos entre contas bancárias, podendo ser:

<br>

* [Transferência interna](/docs/referencia-da-api/transferencias/transferencias-internas): Transferência entre duas Contas Stone. O valor transferido é creditado instantaneamente na conta destinatária, independente do horário e dia da efetuação da transação.

* [Transferência externa](/docs/referencia-da-api/transferencias/transferencias-externas): TED (Transferência Eletrônica Disponível) para outros bancos. Nos dias úteis, entre 6:30 e 17:23, a transação é processada de forma assíncrona e o valor é creditado na conta destino em poucas horas. Caso a operação seja efetuada fora do horário citado e/ou em dias não úteis, a transação será agendada automaticamente para o dia útil seguinte.


<br>

#### Status:
<br>

##### Segue abaixo os status possíveis de uma **transferência externa**: 
<br>

![status_TED](/docs/referencia-da-api/transferencias/o-que-e-uma-transferencia/1b90b91-Transfrncia_Externa.png)

<br>

A transferência externa criada pelo parceiro aguardará a [aprovação](/docs/guias/integracao/aprovacao) do usuário da conta no estado `CREATED`. Essa transferência pode ser rejeitada pelo usuário, concluindo no estado `REJECTED`, e não será efetuada. Caso ela seja uma transferência agendada, é possível que o prazo do agendamento expire antes dela obter aprovação, encerrando em `EXPIRED`.

Caso ela seja agendada e aprovada dentro do prazo, seguirá para o estado `SCHEDULED`, e será efetuada  na data do agendamento. É importante observar que caso a criação da transferência externa, tanto pelo parceiro quanto pelo usuário, seja feita fora do horário de 6:30 às 17:23, ela seguirá para um estado de `DELAYED_TO_NEXT_BUSINESS_DAY`, em que ela será agendada para a próxima janela de execução. É possível que o usuário cancele a transferência antes dela ser efetuada, encerrando no estado `CANCELLED`.

Quando é o próprio usuário que cria a transação, o fluxo já se inicia no estado `APPROVED` ou `SCHEDULED`, caso tenha sido criada com agendamento. A transferência poderá falhar apenas caso não haja fundos e terminará no estado `FAILED`. Caso tenha sido aprovada e haja fundos, a Stone realizará a transferência para o banco externo, obtendo o estado `FINISHED`. Caso haja algum problema como, por exemplo, dados incorretos, ele será reembolsado e irá  finalizar no estado `REFUNDED`.

Para a transferência interna o fluxo é similar. Neste caso não haverá o estado `REFUNDED`, já que antes de realizar a transferência já conferimos a existência da conta destino. Não haverá também o estado `DELAYED_TO_NEXT_BUSINESS_DAY`, porque não há limites de horário para a realização de transferências para outras contas Stone.

É possível consultar o status de uma transação a qualquer momento para saber em qual estado ela está.

<br>


##### Segue abaixo os status possíveis de uma **transferência interna**: 

![status_TransfInterna](/docs/referencia-da-api/transferencias/o-que-e-uma-transferencia/0d9c77f-Transferncia_Interna.png)

<br>

{{% pageinfo %}}
No ambiente de _sandbox_, a API de transferência externa fica disponível de 6:30 às 17:23 todos os dias, inclusive nos fins de semana e feriados, para facilitar os testes.
{{% /pageinfo %}}

<br>

#### Falhas em transferências
---
<br>

Falha é qualquer erro que ocorra entre a criação e a movimentação do dinheiro na conta. Ou seja, qualquer condição que era válida no momento da criação da transferência, mas que mudou nas etapas seguintes.

A seguir listamos algumas das falhas possíveis para transações de transferência, tanto para interna quanto para externa.

<br>


| Código | Descrição                                                            |
| ------ | -------------------------------------------------------------------- |
| 0      | Ocorreu um erro durante a transferência. Por favor, tente novamente. |
| 1      | Saldo insuficiente.                                                  |
| 2      | A operação falhou por uma restrição em uma das contas.               |
| 409	 | É recebido esse erro quando é realizado o envio de uma nova TED anteriormente enviada com sucesso, porém, com a mesma chave de idempotência. |

<br>

#### Reembolsos em transferências
---
<br>

**Reembolsos ocorrem apenas em transferências para outros bancos**, já que para transferências internas conferimos a existência da conta destino antes de realizar a transferência.<br>
Abaixo listamos algumas das razões possíveis para ocorrer reembolsos, como também seus códigos correspondentes.

<br>

| Código | Descrição                                                                                           |
| ------ | --------------------------------------------------------------------------------------------------- |
| 0      | Ocorreu um erro durante a transferência. Por favor, tente novamente.                                |
| 1      | A conta destino não existe mais. Por favor, entre em contato com o titular.                         |
| 2      | A agência ou conta do destino estão incorretas. Por favor, confira os dados e tente novamente.      |
| 3      | O CPF/CNPJ do destino está incorreto. Por favor, confira os dados e tente novamente.                |
| 4      | Mensagem Inválida para o Tipo de Transação ou Finalidade.                                           |
| 5      | Ocorreu um problema devido ao grande volume de transações. Tente novamente.                         |
| 6      | A conta destino não está apta a receber o valor enviado. Por favor, entre em contato com o titular. |
| 7      | Não conformidade no pagamento.                                                                      |
| 8      | Os dados informados estão incorretos. Por favor, confira e tente novamente.                         |
| 9      | CPF/CNPJ inapto junto à Receita Federal do Brasil.                                                  |
| 10     | Por solicitação de cliente da instituição participante recebedora.                                  |
