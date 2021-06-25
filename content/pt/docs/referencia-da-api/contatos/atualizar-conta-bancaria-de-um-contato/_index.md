---
title: "Atualizar Conta Bancária de Um Contato"
slug: "atualizar-conta-bancária-de-um-contato"
hidden: false
date: 2019-04-01T20:12:36.094Z
lastmod: 2019-12-02T22:56:58.190Z
weight: 8
---

```
POST https://sandbox-api.openbank.stone.com.br/api/v1/accounts/account_id/contacts/contact_id/bank_accounts/bank_account_id
```

---

#### **PATH PARAMS**

---

**account_id**  `string`

Identificador da conta.

---

**contact_id**  `string`

Identificador do contato.

---

**bank_account_id**  `string`

Identificador da conta bancária do contato.

<br>

---

#### **BODY PARAMS**

---

**account_code**  `string`

Número da conta bancária.

---

**branch_code**  `string`

Número da agência bancária.

---

**institution_code**  `string`

Número da instituição.

---

#### **HEADERS**

---

**x-stone-idempotency-key**  `string`

Chave de idempotência.

<br>

---

#### **Response**

```
200 OK
content-type: application/json
```
Body
```json
{
  "id": "e43e3003-c587-4cb8-ab37-b374fe0d157f",
  "branch_code": "1234",
  "institution_code": "197",
  "account_code": "4567864"
}
```
