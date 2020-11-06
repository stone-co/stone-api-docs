---
title: "Cancelar Cobrança"
linkTitle: "Cancelar Cobrança"
date: 2020-11-06T15:16:43-03:00
lastmod: 2020-11-06T15:16:43-03:00
weight: 1
description: >
  
---

##### **Request**
```http request
DELETE - /api/v1/pix_payment_invoices/:id
```

##### **Response**
Cobrança cancelada com sucesso
```text
204 NO CONTENT
```

PIX Já foi pago e não pode ser mais cancelado
```text
422

{
  "type": "srn:error:already_paid"
}
```