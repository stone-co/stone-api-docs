---
title: "Rejeitar uma Transferência Externa"
slug: "rejeitar-uma-transferência-externa"
draft: false
weight: 7
date: "2019-04-01T19:53:34.566Z"
lastmod: "2019-12-02T22:56:58.170Z"
---
---

```http 
POST https://sandbox-api.openbank.stone.com.br/api/v1/external_transfers/external_transfer_id/reject
```
---

#### **BODY PARAMS**

---

**external_transfer_id***  `string`
<br> Identificador da transferência externa.

<br>

#### **Response**

```JSON
204 No Content
