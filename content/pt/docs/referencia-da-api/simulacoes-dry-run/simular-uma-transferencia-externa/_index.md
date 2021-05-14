---
title: "Simular uma Transferência Externa"
slug: "simular-uma-transferência-externa"
hidden: false
date: 2018-10-19T20:57:05.070Z
lastmod: 2019-12-02T22:56:58.216Z
weight: 2
---
---

```http
POST https://sandbox-api.openbank.stone.com.br/api/v1/dry_run/external_transfers
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

Identificador da conta.

---

<br>

**target**  `object`

- **account**  `object`

  - **account_code** `string`
    Número da conta. Padrão: `^\d+$`

  - **branch_code** `string`
    Número da agência. Padrão: `^\d{1,4}$`

  - **institution_code** `string`
    Código ISPB da instituição ou número do banco. Padrão: `^(\d{8}|\d{3})$`

- **entity**  `object`
  
  - **name** `string`
    Nome da dona da conta alvo.

  - **document** `string`
    Número do documento sem pontos da dona da conta alvo.

  - **document_type** `string`
    Tipo do documento da dona da conta alvo. Pode ser `cpf` ou `cnpj`.

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

---

##### **Response**

```http
202 Accepted
content-type: application/json
```
Body
```JSON
{  
   "amount":16600,
   "approval_expired_at":null,
   "approved_at":"2019-06-07T18:57:57Z",
   "approved_by":"user:b2b80e9a-7412-47de-b303-2f70f3c8e279",
   "cancelled_at":null,
   "created_at":"2019-06-07T18:57:57Z",
   "created_by":"user:b2b80e9a-7412-47de-b303-2f70f3c8e279",
   "delayed_to_next_business_day":false,
   "failed_at":null,
   "fee":0,
   "finished_at":null,
   "id":"05e2950b-ff0c-4b8f-aa5f-7055bb8bc6f1",
   "refund_reason_code":null,
   "refund_reason_description":null,
   "refunded_at":null,
   "rejected_at":null,
   "rejected_by":null,
   "scheduled_to_effective":null,
   "scheduled_to_requested":null,
   "status":"APPROVED",
   "target":{  
      "account":{  
         "account_code":"1241441",
         "branch_code":"1241",
         "institution_ispb":"60701190",
         "institution_name":"Itaú Unibanco  S.A.",
         "institution_number_code":"341"
      },
      "entity":{  
         "document":"133835162745",
         "document_type":"cpf",           
         "name":"fulano novo"
      }
   }
}
```
