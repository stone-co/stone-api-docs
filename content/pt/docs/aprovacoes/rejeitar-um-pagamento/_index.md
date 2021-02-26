---
title: "Rejeitar um Pagamento"
slug: "rejeitar-um-pagamento"
draft: false
weight: 3
date: "2019-04-01T19:45:56.253Z"
lastmod: "2019-12-02T22:56:58.163Z"
---
---

```http 
POST https://sandbox-api.openbank.stone.com.br/api/v1/payments/payment_id/reject
```
---

##### **BODY PARAMS**

---

**payment_id***  `string`
<br> Identificador do pagamento.

<br>

##### **Response**

```JSON
204 No Content
