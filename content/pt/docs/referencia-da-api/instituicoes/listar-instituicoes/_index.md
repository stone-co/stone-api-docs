---
title: "Listar Instituições"
linkTitle: "Listar Instituições"
slug: "listar-instituições"
draft: false
weight: 2
date: 2020-09-17T18:00:00-03:00
lastmod: 2020-09-17T18:00:00-03:00
description: >
---

---
<br>

```
GET https://sandbox-api.openbank.stone.com.br/api/v1/institutions
```

---

#### **PATH PARAMS**

---

**context**  `string`
<br> Pode ser "spi", "str", ou "all". O default se nada for passado é "str".

* "str" - Retornamos as instituições participantes do STR. Útil para operaçõs de TED
* "spi" - Retornamos as instituições participantes do SPI. Útil para operaçõs de PIX
* "all" - Retornamos todas as instituições

<br>

#### **Response**
---


```
201 Created
content-type: application/json
```
<br>

Body
```json
[
  {
    "ispb_code": "16501555",
    "name": "Stone Pagamentos S.A.",
    "number_code": "197",
    "short_name": "STONE PAGAMENTOS S.A."
  },
  {
    "ispb_code": "00000000",
    "name": "Banco do Brasil S.A.",
    "number_code": "001",
    "short_name": "BCO DO BRASIL S.A."
  },
  {
    "ispb_code": "00360305",
    "name": "Caixa Econômica Federal",
    "number_code": "104",
    "short_name": "CAIXA ECONOMICA FEDERAL"
  },
  {
    "ispb_code": "90400888",
    "name": "Banco Santander (Brasil) S. A.",
    "number_code": "033",
    "short_name": "BCO SANTANDER (BRASIL) S.A."
  },
  {
    "ispb_code": "60746948",
    "name": "Banco Bradesco S.A.",
    "number_code": "237",
    "short_name": "BCO BRADESCO S.A."
  },
  {
    "ispb_code": "60701190",
    "name": "Itaú Unibanco  S.A.",
    "number_code": "341",
    "short_name": "ITAÚ UNIBANCO BM S.A."
  },
  {
    "ispb_code": "18236120",
    "name": "Nu Pagamentos S.A.",
    "number_code": "260",
    "short_name": "NU PAGAMENTOS S.A."
  },
  {
    "ispb_code": "00416968",
    "name": "Banco Inter S.A.",
    "number_code": "077",
    "short_name": "BANCO INTER"
  }
]
```
