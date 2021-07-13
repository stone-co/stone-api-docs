---
title: "Atualizar Contato"
slug: "atualizar-contato"
hidden: false
date: 2019-04-01T20:07:27.693Z
lastmod: 2019-12-02T22:56:58.185Z
weight: 5
---

```
POST https://sandbox-api.openbank.stone.com.br/api/v1/accounts/account_id/contacts/contact_id
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

#### **BODY PARAMS**

---

**name**  `string`

Nome do contato.

---

**tax_id**  `string`

Documento do contato.

---

**email**  `string`

E-mail do contato.

---

**mobile**  `string`

Telefone do contato.

<br>

---

#### **HEADERS**

---

**x-stone-idempotency-key**  `string`

Chave de idempotência.

---

#### **Response**

```
200 ok
content-type: application/json
```
Body
```json
{
  "bank_accounts": [],
  "email": null,
  "id": "93305585-0576-4ca0-aeac-3a75f9cc3c18",
  "mobile": null,
  "name": "Mauro Barcelos",
  "tax_id": "58515428881"
}
```
