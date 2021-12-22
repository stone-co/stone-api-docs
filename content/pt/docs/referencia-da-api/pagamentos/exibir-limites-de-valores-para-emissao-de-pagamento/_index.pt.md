---
title: "Exibir Limites De Valores Para Emissão De Pagamento"
linkTitle: "Exibir Limites De Valores Para Emissão De Pagamento"
slug: "exibir-limites-de-pagamento"
date: 2021-12-09T18:21:13-03:00
lastmod: 2021-12-09T18:21:13-03:00
weight: 4
---

```
GET https://sandbox-api.openbank.stone.com.br/api/v1/barcode_payment_invoices/limits/:account_id
```

---

#### **QUERY PARAMS**

---

<br>

**account_id*** `string`

Identificador da conta.

---

<br>

##### **Response**

```json
200 OK
```

Body

```json
{
  "account_id": "477f8576-ca82-462b-be73-dc28cc6490c3",
  "maximum_amount": 2000000,
  "minimum_amount": 2000
}
```
