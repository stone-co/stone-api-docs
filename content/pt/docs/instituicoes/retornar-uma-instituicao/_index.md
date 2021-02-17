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
GET https://sandbox-api.openbank.stone.com.br/api/v1/institutions/<code>

200 OK
```

---

#### PATH PARAMS

---

##### code

- Type: `string`
- Código da Instituição
- Example: `197`

---

#### RESPONSE

---

- Sucesso:
  - 200 OK
  - Example:

```json
{
  "ispb_code": "16501555",
  "name": "Stone Pagamentos S.A.",
  "number_code": "197",
  "short_name": "STONE PAGAMENTOS S.A."
}
```
