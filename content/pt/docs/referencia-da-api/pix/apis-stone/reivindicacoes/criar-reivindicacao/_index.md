---
title: "Criar Reivindicação"
linkTitle: "Criar Reivindicação"
date: 2022-11-21T11:00:00-03:00
lastmod: 2022-11-21T1:00:00-03:00
weight: 8
draft: false
description: >

---
<br>

Esse endpoint tem como finalidade criar o processo de reivindicação.

##### **Request**
---

```
POST /api/v1/pix/:account_id/entry_claims
```

##### **Headers**
---

**x-stone-idempotency-key** `string`
<br>Chave de idempotência
<br>

#### **Body params**
---

**pix_entry_id** `UUID` _(obrigatório)_
<br>Identificador da chave Pix cuja criação resultou em falha.
<br>

**participant_ispb** `string` _(obrigatório)_
<br>Identificador da instituição.
<br>

**beneficiary_account** `object`
<br>&nbsp;&nbsp;&nbsp;&nbsp;**account_code** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;Número da conta
<br>&nbsp;&nbsp;&nbsp;&nbsp;**branch_code** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;Agência
<br>&nbsp;&nbsp;&nbsp;&nbsp;Format: ^\d{4}$
<br>&nbsp;&nbsp;&nbsp;&nbsp;**account_type** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;Tipo da conta.
<br>&nbsp;&nbsp;&nbsp;&nbsp;Valores permitidos: `CC`, `CS`, `PP` ou `PG`
<br>&nbsp;&nbsp;&nbsp;&nbsp;**created_at** `datetime`
<br>&nbsp;&nbsp;&nbsp;&nbsp;Data de criação da conta.
<br>&nbsp;&nbsp;&nbsp;&nbsp;Format: ISO8601 - "YYYY-MM-DDThh:mm:ssZ"

**beneficiary_entity** `object`
<br>&nbsp;&nbsp;&nbsp;&nbsp;**name** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;Nome
<br>&nbsp;&nbsp;&nbsp;&nbsp;**legal_name** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;É o nome que identifica o pagador para fins legais, administrativos e outros fins oficiais
<br>&nbsp;&nbsp;&nbsp;&nbsp;**document** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;Número do documento (CPF/CNPJ)
<br>&nbsp;&nbsp;&nbsp;&nbsp;**document_type** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;Valores permitidos: `cpf`, `cnpj`
<br>
<br>

--- 

Exemplo:  

```
{
  "pix_entry_id": "390d7eda-e948-4552-bcdf-886c62e5923b",
  "participant_ispb": "16501555"
}
```
<br> 

##### **Response**
---

```
202 Accepted
```

Sucesso na criação da reivindicação de posse/portabilidade 
<br>
Body
```json
{  
  "id": "390d7eda-e948-4552-bcdf-886c62e5923b",
  "claim_type": "ownership" | "portability"
}
```
<br> 

```
401 Unauthenticated
```

Usuário não autenticado
<br>
Body
```json
{  
  "type": "srn:error:unauthenticated"
}
```
<br> 

```
422 Unprocessable Entity
```

Chave não encotrada ou com status diferente de `failed`
<br>
Body
```json
{
  "type": "srn:error:entry_not_found" 
}
```

```
422 Unprocessable Entity
```

Reivindicação não é possível 
<br>
Body
```json
{  
  "type": "claim_type_not_available"
}
```
<br> 