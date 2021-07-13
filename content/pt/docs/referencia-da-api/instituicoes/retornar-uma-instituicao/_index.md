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

---

<br>

```
GET https://sandbox-api.openbank.stone.com.br/api/v1/institutions/code
```

<br>

#### **PATH PARAMS**

---
<br>

**code** `string`<br>
Código da Instituição

Example: `197`

<br><br> 



#### **Response**
---

```
201 Created
content-type: application/json
```
<br>

Body
```json
{
  "ispb_code": "16501555",
  "name": "Stone Pagamentos S.A.",
  "number_code": "197",
  "short_name": "STONE PAGAMENTOS S.A."
}
```
