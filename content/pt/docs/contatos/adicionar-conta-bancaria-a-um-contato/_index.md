---
title: "Adicionar Conta Bancária a Um Contato"
slug: "adicionar-conta-bancária-a-um-contato"
hidden: false
date: 2019-04-01T20:10:46.029Z
lastmod: 2019-12-02T22:56:58.188Z
weight: 7
---


```http
POST https://sandbox-api.openbank.stone.com.br/api/v1/accounts/account_id/contacts/contact_id/bank_accounts
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

**account_code**  `string`

Número da conta.

---

**branch_code**  `string`

Número da agência bancária.

---

**institution_code**  `string`

Número da instituição.

<br>

---

#### **HEADERS**

---

**x-stone-idempotency-key**  `string`

Chave de idempotência.

<br>

---

#### **Response**

```http
200 OK
content-type: application/json
```
Body
```JSON
{
  "account_code": "4567864",
  "branch_code": "1234",
  "id": "9145a75a-f86b-4cc5-bcfe-64b658c610b6",
  "institution_code": "00000000"
}
```
