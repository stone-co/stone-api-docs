---
title: "Consultar Extrato"
slug: "consultar-extrato"
hidden: false
date: 2019-04-01T19:05:11.368Z
lastmod: 2020-04-20T20:28:41.079Z
weight: 8
---

---

```http
GET https://sandbox-api.openbank.stone.com.br/api/v1/accounts/account_id/statement
```

<br>

**PATH PARAMS**

---
<br>

**account_id**  `string`

Identificador da Conta.

<br> 


**QUERY PARAMS**

---
<br>

**limit**  `int32`

<br>

**before**  `string`<br>
Traz a página anterior ao cursor.

<br>

**after**  `string`<br>
Traz a página posterior ao cursor.

<br>

**start_datetime**  `string`<br>
Format: ISO8601 - "YYYY-MM-DDThh:mm:ssZ"

<br>

**end_datetime**  `string`<br>
Format: ISO8601 - "YYYY-MM-DDThh:mm:ssZ"

<br>

**type**  `string`<br>
Filtra o extrato por um ou mais tipos de registro.

Valores possíveis: `internal`, `external`, `external_refund`, `payment`, `payment_refund`, `balance_block`, `card_payment`, `salary_portability`, `salary_portability_refund`, `salary_portability_employer_refund` e `instant_payment`.

Para escolher mais de um type, basta incluir no final da requisição os types, exemplo:  `/statement?type[]=external&type[]=internal`

<br>

{{% pageinfo %}}
**Valor da Operação**

Também repare que, quando se faz uma transferência de R$100,00, por exemplo, o campo `_operation_amount_` terá valor de 10000 centavos. Já o campo _amount_ será a soma do valor da operação com a taxa cobrada (_fee_amount_).
{{% /pageinfo %}}

---
{{% pageinfo %}}
**Tipos diferentes de extratos**

O extrato é dividido por tipos de movimentação. É possível consultar qual foi a movimentação pelo `type` da resposta. No exemplo acima, podemos notar que tivemos duas movimentações: uma transferência interna (`type:internal`) e uma transferência externa (`type:external`), ambas com campos de resposta diferentes. Veja neste [link](/docs/referencia-da-api/dados-da-conta/objetos-do-extrato/) para mais informações sobre o JSON Schema de cada tipo de operação.
{{% /pageinfo %}}

<br>

##### Response
---

```http
201 Created
content-type: application/json
```
<br>

##### Body

---

```JSON
{
    "cursor": {
        "after": null,
        "before": null,
        "limit": 25
    },
    "data": [
        {
            "amount": -1600,
            "balance_after": 9998300,
            "balance_before": 9999900,
            "counter_party": {
                "account": {
                    "account_code": "58859",
                    "branch_code": "1",
                    "institution": "16501555",
                    "institution_name": "Stone Pagamentos S.A."
                },
                "entity": {
                    "name": "João Amigavel"
                }
            },
            "created_at": "2019-07-31T19:13:56Z",
            "description": "",
            "fee_amount": 0,
            "id": "5357781a-c318-41aa-80eb-269df1b65ba3",
            "operation": "debit",
            "operation_amount": 1600,
            "operation_id": "4aab75b9-c15f-4d27-82e2-ec9c549c1cd8",
            "scheduled_at": null,
            "scheduled_to": null,
            "status": "FINISHED",
            "type": "internal"
        },
        {
            "amount": -100,
            "balance_after": 9999900,
            "balance_before": 10000000,
            "barcode": "89690000000010003139343476533694034641055662",
            "created_at": "2019-07-31T19:12:51Z",
            "details": {
                "bank_name": null,
                "expiration_date": null,
                "recipient_cpf_cnpj": "90890860998",
                "recipient_name": "Sr. Luiz Bulhões",
                "writable_line": "896900000002010003139341347653369400346410556622"
            },
            "fee_amount": 0,
            "id": "4d1d6f7b-187c-4ad4-acb6-4bf573609a6b",
            "operation": "debit",
            "operation_amount": 100,
            "operation_id": "ace4331a-45ef-488a-9fde-c439739b9d4a",
            "scheduled_at": null,
            "scheduled_to": null,
            "status": "FINISHED",
            "type": "payment",
            "writable_line": "896900000002010003139341347653369400346410556622"
        }
    ]
}
```

<br>


{{< alert title="Observação" >}}

<br>

Na resposta acima foram feitas duas transferências, uma interna e uma externa, ambas com as suas particularidades de retorno.

Em cada extrato há duas informações: {balance before} e {balance after}. <br>
O `_balance_before_` registra o saldo do usuário antes da operação, e o `_balance_after_` registra o saldo após a operação dado o `_balance_before_` menos o valor da operação.

{{< /alert >}}

