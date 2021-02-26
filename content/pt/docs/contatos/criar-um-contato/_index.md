---
title: "Criar Um Contato"
slug: "criar-um-contato"
hidden: false
date: 2019-04-01T20:01:02.396Z
lastmod: 2019-12-02T22:56:58.179Z
weight: 2
---

```http
POST https://sandbox-api.openbank.stone.com.br/api/v1/accounts/account_id/contacts
```

---

##### PATH PARAMS

---

**account_id**  `string`

Identificador da conta.

---

##### BODY PARAMS

---

**name**  `string`

Nome do contato.

**tax_id**  `string`

Documento do contato (CPF/CNPJ).

**email**  `string`

E-mail do contato.

**mobile**  `string`

Telefone do contato.

---

##### HEADERS

---

**x-stone-idempotency-key**  `string`

Chave de idempotência.

---

##### Response

```http
200 ok
content-type: application/json
```

```JSON
{
  "bank_accounts": [],
  "email": "guilherme.email@stone.com.br",
  "id": "222f3745-24ed-4968-929f-a88c168ce582",
  "mobile": "21 999999999",
  "name": "Guilherme Posse",
  "tax_id": "16426334022"
}
```
