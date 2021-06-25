---
title: "Simular uma Transferência Interna"
slug: "simular-uma-transferência-interna"
hidden: false
date: 2018-10-19T20:57:05.070Z
lastmod: 2019-12-02T22:56:58.216Z
weight: 1
---
---

```
POST https://sandbox-api.openbank.stone.com.br/api/v1/dry_run/internal_transfers
```

---

#### **BODY PARAMS**

---
<br>

**amount**  `int32`

Valor da transferência em centavos de Real, ou seja, um real é igual a 100.

---

<br>

**account_id**  `string`

Identificador da conta que está enviando a transferência.

---

<br>

**target**  `object`

- **account**  `object`
  
  - **account_code** `string`
    Número da conta. Padrão: `^\d+$`


---
<br>

**description**  `string`

Descrição da transação. Essa descrição será exibida tanto no extrato de quem enviou quanto de quem recebeu (limite 200 caracteres).

---

<br>

**scheduled_to**  `string`

Formato: `yyyy-mm-dd`

<br>

---

#### **HEADERS**

---

<br>

**x-stone-idempotency-key**  `string`

Chave de idempotência.

<br>

##### **Response**

```
200 ok
content-type: application/json
```
Body
```json
{
  "amount": 12,
  "approval_expired_at": null,
  "approved_at": "2019-04-26T16:06:43Z",
  "approved_by": "user:380f9968-8946-4f88-a781-be8b7efc1f90",
  "cancelled_at": null,
  "created_at": "2019-04-26T16:06:43Z",
  "created_by": "user:380f9968-8946-4f88-a781-be8b7efc1f90",
  "description": "",
  "failed_at": null,
  "fee": 100,
  "finished_at": null,
  "id": "8d427b2b-7a8e-4570-9c90-224339a10517",
  "rejected_at": null,
  "rejected_by": null,
  "scheduled_to": null,
  "status": "APPROVED",
  "target": {
     "account": {
       "account_code": "123"
      },
      "entity": {
        "name": "Fulano da Silva"
      }
  }
}
```
