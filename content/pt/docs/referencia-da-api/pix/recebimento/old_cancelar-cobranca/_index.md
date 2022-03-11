---
title: "Old_Cancelar Cobrança"
linkTitle: "Old_Cancelar Cobrança"
date: 2020-11-06T15:16:43-03:00
lastmod: 2020-11-06T15:16:43-03:00
weight: 6
draft: true
description: >

---

##### **Request**
```
DELETE /api/v1/pix_payment_invoices/:id
```

##### **Response**
Cobrança cancelada com sucesso
```
204 NO CONTENT
```

Pix Já foi pago e não pode ser mais cancelado
```
422 DOMAIN ERROR
```

```json
{
  "type": "srn:error:already_paid"
}
```
