---
title: "Criar Reivindicação/Portabilidade"
linkTitle: "Criar Reivindicação/Portabilidade"
date: 2022-11-21T11:00:00-03:00
lastmod: 2022-11-21T1:00:00-03:00
weight: 8
draft: true
description: >

---

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

#### **Paramentros para query**
---

```
- "pix_entry_id" * (obrigatorio)
- "participant_ispb" *(obrigatório para participantes indiretos)
- "beneficiary_account"
- "beneficiary_account.branch_code"
- "beneficiary_account.account_code"
- "beneficiary_account.account_type"
- "beneficiary_account.created_at"
- "beneficiary_entity"
- "beneficiary_entity.name"
- "beneficiary_entity.legal_name"
- "beneficiary_entity.document_type"
- "beneficiary_entity.document"   
```


```
 **pix_entry_id***
<br>Identificador da chave Pix cuja criação resultou em falha.
<br>Format: UUID
**participant_ispb***
<br>Identificador da instituição.
 **beneficiary_account**
<br> Identificação da conta
**beneficiary_entity** `object`
<br>&nbsp;&nbsp;&nbsp;&nbsp;**name** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;Nome
<br>&nbsp;&nbsp;&nbsp;&nbsp;**legal_name** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;É o nome que identifica o pagador para fins legais, administrativos e outros fins oficiais
<br>&nbsp;&nbsp;&nbsp;&nbsp;**document** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;Número do documento (CPF/CNPJ)
<br>&nbsp;&nbsp;&nbsp;&nbsp;**document_type** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;Valores permitidos: `cpf`, `cnpj`
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
```


Exemplo:  

- `{
  "pix_entry_id": "390d7eda-e948-4552-bcdf-886c62e5923b",
  "participant_ispb": "16501555"
}`;
<br> <br> 

##### **Response**
---


**Status**: 202

Body
```json
{  
  "id": "390d7eda-e948-4552-bcdf-886c62e5923b",
  "claim_type": "ownership" | "portability"

}
```
<br> <br> 


**Status**: 401

Body
```json
{  
    "type": "srn:error:unauthenticated"
}
```
<br> <br> 


**Status**: 403

Apenas após 2 minutos de falaha da chave
<br>
Body
```json
{  
     "type": "srn:error:needs_verification",
     "details": {"verification_id": "uuid"}
}
```
<br> <br> 


**Status**: 422

Chave em status diferente de failed / Reivindicação não é possível (chave já em processo de claim por outra conta)
<br>
Body
```json
{  
    "type": "srn:error:entry_not_found" | "claim_type_not_available"
}
```
<br> <br> 





