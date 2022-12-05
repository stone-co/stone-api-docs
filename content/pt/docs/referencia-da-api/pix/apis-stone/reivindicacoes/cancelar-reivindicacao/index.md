---
title: "Cancelar Reivindicação/Portabilidade"
linkTitle: "Cancelar Reivindicação/Portabilidade"
date: 2022-11-21T11:00:00-03:00
lastmod: 2022-11-21T1:00:00-03:00
weight: 8
draft: true
description: Cancelar reivindicação/portabilidade da chave Pix>

---
<br>

Esse endpoint tem como finalidade cancelar o processo de reivindicação/portabilidade.

##### **Request**
---

```
POST /api/v1/pix/:account_id/entry_claims/cancel
```

##### **Headers**
---

**x-stone-idempotency-key** `string`
<br>Chave de idempotência
<br>

#### **Body params**
---

**claim_id** `String` _(obrigatório)_
<br>Identificador da reivindicação.
<br>

**reason** `String` _(obrigatório)_
<br>Valores permitidos: `user_requested`
<br>

**direction** `string`
<br>Valores permitidos: `outbound`, `inbound` 
<br>

**participant_ispb** `string` _(obrigatório)_
<br>Identificador da instituição.
<br>

Exemplo:  

```
{
  "claim_id": "390d7eda-e948-4552-bcdf-886c62e5923b",
  "reason": "user_requested",
  "direction": "outbound",
  "participant_ispb": "16501555"
}
```

##### **Response**
---

```
202 Accepted
```

Pedido de cancelamento realizado com sucesso.
<br>
Body
```json
{  
  "pix_entry_claim": "390d7eda-e948-4552-bcdf-886c62e5923b",
  "claim_type": "ownership" | "portability"
}
```
<br> 

```
401 Unauthenticated
```

Usuário não está autenticado.
<br>
Body
```json
{  
    "type": "srn:error:unauthenticated"
}
```
<br> 

```
403 Unauthorized
```

Usuário não autorizado a realizar a ação.
<br>
Body
```json
{  
     "type": "srn:error:unauthorized"
}
```
<br> 

```
422 Unprocessable Entity
```

Reivindicação á foi cancelada ou confirmada.
<br>
Body
```json
{  
    "type": "srn:error:already_cancelled" | "srn:error:already_confirmed"
}
```
<br> 