---
title: "Transferir para Outros Bancos"
slug: "transferir-para-outros-bancos"
draft: false
weight: 7
---

---

<br>

Faz transferências monetárias para outra instituição (TED). Não é permitido realizar uma TED de uma conta Stone para outra conta Stone.

<br>

{{< alert title="Horário de funcionamento" >}}
<br>

A **API de Transferência Externa** fica disponível em dias úteis, das 6h30 às 17h20, a transação é processada de forma assíncrona e o valor é creditado na conta destino em poucas horas.
{{< /alert >}}


<br>

Caso a transferência seja criada em um dia não útil ou fora do horário de funcionamento de TEDs, a transferência será agendada automaticamente para o dia seguinte. Nesse caso seu status será `DELAYED_TO_NEXT_BUSINESS_DAY`, como também a flag `delayed_to_next_business_day = true`. O campo `scheduled_to_effective` conterá a data para a qual a TED foi agendada.

A transferência também pode ser agendada através do campo `scheduled_to`. A data usada no campo `scheduled_to` deve estar entre a data `next_available_execution_date` e a data limite retornada no campo `execution_limit_date` da [API de calendário de agendamento](/docs/referencia-da-api/agendamento/calendario-de-agendamento/) chamada com o parâmetro `operation_type=external_transfer`. Caso a data escolhida seja menor do que `next_available_execution_date`, a transferência será executada imediatamente. Caso a data seja maior que `execution_limit_date` será retornado um erro 422.

Caso a data escolhida não seja um dia útil, a transferência será automaticamente agendada para o próximo dia útil depois do escolhido. O dia útil requisitado (que veio na request) e o efetivo (em que de fato o agendamento vai ocorrer) são representados pelos campos `scheduled_to_requested` e `scheduled_to_effective`.

A data usada no campo `scheduled_to` deve obedecer a data limite retornada na [API de calendario de agendamento](/docs/referencia-da-api/agendamento/calendario-de-agendamento/). Caso contrário, será retornado um erro 422 na criação.

<br>

---

```
POST https://sandbox-api.openbank.stone.com.br/api/v1/external_transfers
```
---

#### **BODY PARAMS**
---
<br>

**amount*** `int32`
<br>Valor da transferência em centavos de Real, ou seja, um real fica 100.

---
<br>

**account_id*** `string`
<br>Identificador da conta que está enviando a transferência.

---
<br>

**target** `object`
	<br><br>
&nbsp; &nbsp; **account** `object`
		<br><br>
		 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**account_code** `string` _(obrigatório)_
		<br>
		&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Número da conta. Padrão: `^[1-9]\d{1,19}$`
		<br><br>
		 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**branch_code** `string`
		<br>
		&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Número da agência. Padrão: `^\d{1,4}$`
		<br><br>
		 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**institution_code** `string` _(obrigatório)_
		<br>
		&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Código ISPB da instituição ou número do banco. Padrão: `^(\d{8}|\d{3})$`.
		<br><br>
		 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**account_type** `string`
		<br>
		&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Tipo de conta destino (verifique mais abaixo os tipos disponíveis).
		
---
<br>

**entity** `object`
	<br><br>
		 &nbsp;&nbsp;**name** `string` _(obrigatório)_
		<br>
		&nbsp;&nbsp;Nome do dono da conta alvo.
		<br><br>
		 &nbsp;&nbsp;**document** `string` _(obrigatório)_
		<br>
		&nbsp;&nbsp;Número do documento sem pontos ou caracteres espaciais do dono da conta alvo.
		<br><br>
		 &nbsp;&nbsp;**document_type** `string`
		<br>
		&nbsp;&nbsp;Tipo do documento do dono da conta alvo. Pode ser `CPF` ou `CNPJ`.
		
---
<br>

**scheduled_to** `string`
<br>Formato: `yyyy-mm-dd`

<br>

#### **HEADERS**
---
<br>

**x-stone-idempotency-key** `string`
<br>Chave de idempotência

<br>


{{% pageinfo %}}
**Request Body**<br>
O corpo da requisição deve conter todos os dados da transferência.<br>
Observe que os "0"s que prefixam o `account_code` são removidos. Por exemplo, "00012345" é armazenado como "12345" e vai ser retornado assim nas APIs de consulta.<br>
Essa transformação é aplicada pela API antes dos dados serem armazenados.
{{% /pageinfo %}}
{{% pageinfo %}}
**Tipos de conta ( target.account.account_type )**
<br>Através deste campo, é possível enviar o tipo de conta destino. Os valores aceitos são:
<br>"CC" - Conta Corrente
<br>"CD" - Conta de Depósito
<br>"CG" - Conta garantida
<br>"PG" - Conta de Pagamento
<br>"PP" - Poupança
<br><br>Este campo possui regras especiais para utilização:
<br>Se o tipo de conta for PG, a agência (branch_code) é removida.
<br>Se o tipo de conta for CC ou nulo, mas o número da conta (account_code) possuir mais de 13 dígitos, o tipo de conta é convertido para PG e a agência (branch_code) é removida.
<br>Se o tipo de conta for CC ou nulo, mas a agência (branch_code) não vier preenchida, o tipo de conta é convertido para PG.
<br>Se o tipo de conta é nulo e não cai nos casos acima, o tipo de conta usado é CC."
{{% /pageinfo %}}
{{% pageinfo %}}
**Sobre o objeto target**
<br>Quando a conta alvo pertence a uma pessoa jurídica, usar `CNPJ` ao invés de `CPF` no objeto `target.entity`."
{{% /pageinfo %}}
{{% pageinfo %}}
**Agendamento**
<br>Em _sandbox_, a transferência externa está disponível de 6:30 às 17:23 todos os dias. 
<br>Em produção, só está habilitada em dias úteis de 6:30 até 17:23. Após este horário a transferência será agendada para o próximo dia útil.",
{{% /pageinfo %}}


<br>

##### **Response**

```
202 Accepted
content-type: application/json
```
Body
```json
{
    "amount": 100,
    "approval_expired_at": null,
    "approved_at": "2019-08-02T18:14:34Z",
    "approved_by": "user:08807157-f8e1-439e-a2ec-154ecb4bee13",
    "cancelled_at": null,
    "created_at": "2019-08-02T18:14:34Z",
    "created_by": "user:08807157-f8e1-439e-a2ec-154ecb4bee13",
    "delayed_to_next_business_day": false,
    "failed_at": null,
    "failure_reason_code": null,
    "failure_reason_description": null,
    "fee": 400,
    "finished_at": null,
    "id": "7458c329-c5e9-4cc8-8174-3aa6210a8867",
    "refund_reason_code": null,
    "refund_reason_description": null,
    "refunded_at": null,
    "rejected_at": null,
    "rejected_by": null,
    "scheduled_to_effective": null,
    "scheduled_to_requested": null,
    "settled_at": null,
    "status": "APPROVED",
    "target": {
        "account": {
            "account_code": "58859",
            "branch_code": "1",
            "institution_code": "90400888",
            "institution_ispb": "90400888",
            "institution_name": "Banco Santander (Brasil) S. A.",
            "institution_number_code": "033"
        },
        "entity": {
            "cpf": "62752545053",
            "document": "62752545053",
            "document_type": "cpf",
            "name": "Octacilio Impoluto"
        }
    }
}
