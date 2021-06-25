---
title: "Retornar Um Contato"
slug: "retornar-um-contato"
hidden: false
date: 2019-04-01T20:05:26.106Z
lastmod: 2021-06-25T20:01:46.027Z
weight: 4
---

```
GET https://sandbox-api.openbank.stone.com.br/api/v1/accounts/account_id/contacts/contact_id
```

---

#### **PATH PARAMS**

---

**account_id**  `string`

Identificador da conta.

---

**contact_id**  `string`

Identificador do contato.

<br>

---

#### **Response**

```
200 ok
content-type: application/json
```
Body
```json
{
  "bank_accounts": [
    {
      "account_code": "4567864",
      "account_type": "PG",
      "branch_code": "1234",
      "id": "9145a75a-f86b-4cc5-bcfe-64b658c610b6",
      "institution_code": "00000000",
      "pix_key": null
    },
    {
      "account_code": "106497993",
      "account_type": "PG",
      "branch_code": "0001",
      "id": "f125f6ff-4f63-4735-92c4-f89754ed2826",
      "institution_code": "16501555",
      "institution": {
        "compe": "197",
        "ispb": "16501555",
        "name": "Stone Pagamentos S.A.",
        "spi_participant": true,
        "str_participant": true
      },
      "pix_key": null
    },
    {
      "account_code": null,
      "account_type": null,
      "branch_code": null,
      "id": "acc162c9-0850-478f-98cc-cb73b834941c",
      "institution_code": null,
      "pix_key": "dff85252-88ed-4ceb-8ced-4bdecd3f0d39"
    }
  ],
  "email": null,
  "id": "93305585-0576-4ca0-aeac-3a75f9cc3c18",
  "mobile": null,
  "name": "Mauro Frederico",
  "tax_id": "58515428881"
}
```