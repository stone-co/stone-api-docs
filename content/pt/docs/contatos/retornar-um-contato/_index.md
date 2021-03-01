---
title: "Retornar Um Contato"
slug: "retornar-um-contato"
hidden: false
date: 2019-04-01T20:05:26.106Z
lastmod: 2019-12-02T22:56:58.183Z
weight: 4
---

```http
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

```http
200 ok
content-type: application/json
```
Body
```JSON
{
  "bank_accounts": [
    {
      "account_code": "4567864",
      "branch_code": "1234",
      "id": "9145a75a-f86b-4cc5-bcfe-64b658c610b6",
      "institution_code": "00000000"
    },
    {
      "account_code": "106497993",
      "branch_code": "1",
      "id": "f125f6ff-4f63-4735-92c4-f89754ed2826",
      "institution_code": "16501555"
    }
  ],
  "email": null,
  "id": "93305585-0576-4ca0-aeac-3a75f9cc3c18",
  "mobile": null,
  "name": "Mauro Frederico",
  "tax_id": "58515428881"
}
```
