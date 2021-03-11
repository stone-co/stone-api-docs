---
title: "Aprovar uma Transferência Interna"
slug: "aprovar-uma-transferência-interna"
draft: false
weight: 4
date: "2019-04-01T19:47:47.337Z"
lastmod: "2019-12-02T22:56:58.165Z"
---
---

```http 
POST https://sandbox-api.openbank.stone.com.br/api/v1/internal_transfers/internal_transfer_id/approve
```
---

#### **BODY PARAMS**

---

**internal_transfer_id***  `string`
<br> Identificador da transferência interna.

<br>

#### **Response**

```JSON
204 No Content
