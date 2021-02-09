---
title: "Consultar Extrato"
slug: "consultar-extrato"
hidden: false
createdAt: "2019-04-01T19:05:11.368Z"
updatedAt: "2020-04-20T20:28:41.079Z"
weight: 8
---

---

```http 
GET https://sandbox-api.openbank.stone.com.br/api/v1/accounts/account_id/statement
```
---


**PATH PARAMS**

---

**account_id***  `string`

Identificador da Conta.

<br>

**QUERY PARAMS**

---

**limit**  `int32`


---

**before**  `string`

Traz a página anterior ao cursor.

---

**after**  `string`

Traz a página posterior ao cursor.


---

**start_datetime**  `string`

Format: ISO8601 - "YYYY-MM-DDThh:mm:ssZ"


---

**end_datetime**  `string`

Format: ISO8601 - "YYYY-MM-DDThh:mm:ssZ"


---

**type**  `string`

Filtra o extrato por um ou mais tipos de registro.

Valores possíveis: `internal`, `external`, `external_refund`, `payment`, `payment_refund`, `balance_block`, `card_payment`, `salary_portability`, `salary_portability_refund`, `salary_portability_employer_refund` e `instant_payment`.

Para escolher mais de um type, basta incluir no final da requisição os types, exemplo:  `/statement?type[]=external&type[]=internal`


---
{{% pageinfo %}}
**Valor da Operação**

Também repare que, quando se faz uma transferência de R$100,00, por exemplo, o campo operation_amount terá valor de 10000 centavos. Já o campo amount será a soma do valor da operação com a taxa cobrada (fee_amount).
{{% /pageinfo %}}


---
{{% pageinfo %}}
**Tipos diferentes de extratos**

O extrato é dividido por tipos de movimentação. É possível consultar qual foi a movimentação pelo type da resposta. No exemplo acima, podemos notar que tivemos duas movimentações: uma transferência interna (type:internal) e uma transferência externa (type:external), ambas com campos de resposta diferentes. Veja neste link para mais informações sobre o JSON Schema de cada tipo de operação.
{{% /pageinfo %}}

Note que, na resposta acima, foram feitas duas transferências, uma interna e uma externa, ambas com as suas particularidades de retorno.

Em cada extrato há duas informações: {balance before} e {balance after}. O balance before registra o saldo do usuário antes da operação, e o balance after registra o saldo após a operação dado o balance before menos o valor da operação.