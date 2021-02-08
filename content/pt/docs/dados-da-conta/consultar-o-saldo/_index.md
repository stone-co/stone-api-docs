---
title: "Consultar o Saldo"
slug: "consultar-o-saldo"
hidden: false
createdAt: "2019-04-01T19:02:42.862Z"
updatedAt: "2019-12-02T22:56:58.118Z"
weight: 6
---

---

```http 
GET https://sandbox-api.openbank.stone.com.br/api/v1/accounts/account_id/balance
```
---

**PATH PARAMS**

---

**account_id***  `string`

Identificador da Conta.


{{% pageinfo %}}
**Atenção**

Note que a variável  _balance_ retornou um total de **9998**, isso corresponde a **R$ 99,98** reais da conta da usuária.