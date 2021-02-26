---
title: "Retornar Uma Instituição"
linkTitle: "Retornar Uma Instituição"
slug: "retornar-uma-instituição"
draft: false
weight: 3
date: 2020-09-17T18:00:00-03:00
lastmod: 2020-09-17T18:00:00-03:00
description: >
---

```http
GET https://sandbox-api.openbank.stone.com.br/api/v1/institutions/code
```

---

##### **PATH PARAMS**

---

**code*** `string`
<br>Código da Instituição
<br>Example: `197`

---

#### **Response**

```JSON
201 Created
content-type: application/json
```
Body
```JSON
{
  "ispb_code": "16501555",
  "name": "Stone Pagamentos S.A.",
  "number_code": "197",
  "short_name": "STONE PAGAMENTOS S.A."
}
```
