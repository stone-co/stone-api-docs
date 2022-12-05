---
title: "Completar Reivindicação de Posse"
linkTitle: "Completar Reivindicação de Posse"
date: 2022-11-21T11:00:00-03:00
lastmod: 2022-11-21T1:00:00-03:00
weight: 8
draft: true
description: Completar reivindicação de posse da chave Pix>

---
<br>

Esse endpoint tem como finalidade completar o processo de reivindicação de posse da chave Pix.

##### **Request**
---

```
POST /api/v1/pix/:account_id/entry_claims/complete
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

Exemplo:  

```
{
  "claim_id": "390d7eda-e948-4552-bcdf-886c62e5923b"
}
```

##### **Response**
---

```
401 Accepted
```

Processo de completar reivindicação realizado com sucesso.
<br>
Body
```json
{  
  "pix_entry_claim": "390d7eda-e948-4552-bcdf-886c62e5923b",
  "claim_type": "ownership" 
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

Usuário não autorizado a realizar a ação
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

Reivindicação já foi completada
<br>
Body
```json
{  
  "type": "srn:error:already_completed" 
}
```
<br> 

```
422 Unprocessable Entity
```

Reivindicação não pode receber ação (por ter sido cancelada ou não ter recebido a confirmação ainda)
<br>
Body
```json
{
  "type": "srn:error:wrong_status"
}
```
<br> 