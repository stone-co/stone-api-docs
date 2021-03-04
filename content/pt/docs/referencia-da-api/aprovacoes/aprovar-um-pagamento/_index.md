---
title: "Aprovar um Pagamento"
slug: "aprovar-um-pagamento"
draft: false
weight: 2
date: "2019-04-01T19:44:06.368Z"
lastmod: "2019-12-02T22:56:58.161Z"
---
---

```http 
POST https://sandbox-api.openbank.stone.com.br/api/v1/payments/payment_id/approve
```
---

#### **BODY PARAMS**

---

**payment_id***  `string`
<br> Identificador do pagamento.

<br>

##### **Response**

```JSON
204 No Content
