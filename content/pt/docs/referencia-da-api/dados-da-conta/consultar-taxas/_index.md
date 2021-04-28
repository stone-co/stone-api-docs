---
title: "Consultar Taxas"
slug: "consultar-taxas"
hidden: false
date: 2019-04-01T19:09:32.363Z
lastmod: 2020-03-30T14:45:05.877Z
weight: 11
---

---

```http
GET https://sandbox-api.openbank.stone.com.br/api/v1/accounts/account_id/fees/fee_type
```

<br>

**PATH PARAMS**

---

<br>

**account_id**  `string`<br>
Identificador da conta.

<br>

**fee_type**  `string`<br>
Tipo de taxa. Valores possíveis: `internal_transfer`, `external_transfer`, `barcode_payment`, `outbound_stone_prepaid_card_payment`, `outbound_stone_prepaid_card_withdrawal` e `barcode_payment_invoice`.

<br>

{{% pageinfo %}}
**Outros Campos**

No caso de `external_transfer` serão também retornados os campos `billing_exempition_participant`, `original_fee`, `max_free_transfers` e `remaining_free_transfers`.

No caso de `barcode_payment_invoice` também serão retornardos os campos `billing_exempition_participant`, `original_fee`, `max_free` e `remaining_free`.
{{% /pageinfo %}}

<br>

##### Response
---

```http
201 OK
content-type: application/json
```
<br>

##### Body
---

```JSON

{
  "amount": 130,
  "fee_type": "internal_transfer"
}
```
