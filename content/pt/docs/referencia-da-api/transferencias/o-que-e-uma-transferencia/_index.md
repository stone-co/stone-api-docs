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

{{< alert title="Horário de funcionamento" >}}
<br>

No ambiente de _sandbox_, a API de transferência externa fica disponível de 6:30 às 17:23 todos os dias, inclusive nos fins de semana e feriados, para facilitar os testes.		
{{< /alert >}}

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
##### **Porque uma transferência é reembolsada?**

Temos vários motivos para que uma transferência retorne, sendo os casos mais comuns conta, agência ou documento do destino errados e saldo insuficiente na conta de origem.
O reembolso de uma transferência somente é realizado quando ela ocorre para contas que não sejam Contas Stone, ou seja, quando ocorrem transferências externas.

<br>

##### **Quando pode ocorrer um reembolso**


###### **Saldo insuficiente**

Através da nossa API é possível agendar uma transferência. Ocorre refund nesses casos quando, na data agendada para a transferência, a conta origem não possuir saldo suficiente em conta.



###### **Dados da transferência incorretos**

Ao realizar uma transferência o usuário precisará enviar os dados da conta destino. Caso os dados de agência, conta ou documento do destino estejam incorretos ou inexistentes, a transferência retorna indicando esse erro.





###### **Tipo de transação ou finalidade inválida**

Caso a conta destinatária não seja do tipo especificado na transferência ou algum dado do destino é inválido. Exemplo: conta destinatária é corrente e o tipo informado era conta poupança ou envio no nome fantasia do destino enquanto era esperado o nome da razão social.



###### **Dados ausentes ou inválidos**

Quando uma transferência é realizada sem um dado obrigatório para a finalização da mesma, como código verificador, agência não informada ou quando o formato de um dado é inválido.
Alguns bancos utilizam códigos verificadores com letras no número da conta ao invés de números, nesses casos, a Conta Stone solicita que a conta origem digite ‘0’ no lugar dessa letra, para que a transferência ocorra com sucesso.



###### **CPF/CNPJ inapto junto à Receita Federal**

Nesse caso, a transferência é retornada para a conta de origem, porém, caso a mesma pessoa tenha acesso a outra conta com outro documento, ela poderá receber a transferência. Exemplo: A pessoa possui o CPF inapto junto à Receita Federal então não poderá receber a transferência em sua conta de pessoa física, porém, se essa mesma pessoa for sócia de uma empresa, nada impede que a transferência seja realizada para conta de pessoa jurídica, a não ser que o CNPJ também esteja inapto.




##### **Códigos de Reembolsos**

Ocorre somente em casos de transferências externas.

| Código | Descrição                                                                                                                                                            |
| ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0      | Ocorreu um erro de processamento no sistema de origem durante a transferência.                                                                                       |
| 1      | A conta destino é inexistente.                                                                                                                                       |
| 2      | A conta ou agência destino é inexistente.                                                                                                                            |
| 3      | O documento do destino está incorreto.                                                                                                                               |
| 4      | Conta destinatária do crédito inválida para o tipo de transação ou finalidade.                                                                                       |
| 5      | Erro de processamento no sistema de origem durante a transferência.                                                                                                  |
| 6      | Transferência supera limite para o tipo de conta destino / Conta destinatária do crédito inválida para o tipo de transação ou finalidade.                            |
| 7      | Não conformidade no pagamento. Exemplo: pagamento a um fornecedor com o valor diferente que o devido.                                                                |
| 8      | Os dados informados estão incorretos: Código Identificador de Transferência Inválido / Campo obrigatório ausente / Formato do dado inválido / Agência não informada. |
| 9      | CPF/CNPJ inapto junto à Receita Federal do Brasil.                                                                                                                   |
| 10     | A instituição financeira do destino não é válida.                                                                                                                    |
| 11     | A conta destino não pode ter mais de 13 dígitos para o tipo de conta escolhido. Por favor, confira os dados e tente novamente.                                       |
| 12     | Por solicitação de cliente da instituição participante recebedora.                                                                                                   |
| 13     | Devolução de ordem bancária pelo agente financeiro.                                                                                                                  |
| 14     | Beneficiário não identificado - Documentos com código de barras.                                                                                                     |
