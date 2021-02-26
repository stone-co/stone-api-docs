---
title: "Listar Contatos"
slug: "listar-contatos"
hidden: false
date: 2019-04-01T20:03:25.687Z
lastmod: 2019-12-02T22:56:58.181Z
weight: 3
---

```http
GET https://sandbox-api.openbank.stone.com.br/api/v1/accounts/account_id/contacts
```

---

##### PATH PARAMS

---

**account_id**  `string`

Identificador da conta.

---

##### QUERY PARAMS

---

**tax_id**  `string`

Filtra contatos pelo documento fornecido.

**account_code**  `string`

Filtra contatos pelo código da conta fornecido.

**institution_code**  `string`

Filtra contatos pelo código da instituição fornecido.

---

##### Response

```http
200 ok
content-type: application/json
```

```JSON
[
  {
    "bank_accounts": [
      {
        "account_code": "35746698",
        "branch_code": "00001",
        "id": "1ede2f26-28cd-462b-a7ea-429960c8480b",
        "institution_code": "197"
      }
    ],
    "email": "contactemail@empresaxyz.com",
    "id": "f0c83515-c7ea-40b8-b9c4-c85d9489c40c",
    "mobile": "21 999999999",
    "name": "Contact name",
    "tax_id": "47647430351"
  },
  {
    "bank_accounts": [
      {
        "account_code": "883841975",
        "branch_code": "0001",
        "id": "5b332a1b-57ef-4398-bb9c-79011cc6c58e",
        "institution_code": "197"
      }
    ],
    "email": "tyson@huber.com",
    "id": "a0ee3a1a-a1d6-48ad-8ea3-7fdf5ea5c250",
    "mobile": null,
    "name": "Tyson Huber",
    "tax_id": "11111111111"
  },
  {
    "bank_accounts": [],
    "email": "johndoe@hotmail.com",
    "id": "a862d499-26cc-48df-9583-585ba604e9c8",
    "mobile": "2124759861",
    "name": "John Doe",
    "tax_id": "42373740761"
  }
]
```
