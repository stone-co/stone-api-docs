---
title: "Excluir Conta Bancária de Um Contato"
slug: "excluir-conta-bancária-de-um-contato"
hidden: false
date: 2019-04-01T20:14:44.779Z
lastmod: 2019-12-02T22:56:58.192Z
weight: 9
---

```http
DELETE https://sandbox-api.openbank.stone.com.br/api/v1/accounts/account_id/contacts/contact_id/bank_accounts/bank_account_id
```

---

**PATH PARAMS**

---

**account_id**  `string`

Identificador da conta.

---

**contact_id**  `string`

Identificador do contato.

---

**bank_account_id**  `string`

Identificador da conta bancária do contato.

---

##### Response

```http
200 ok 
```
