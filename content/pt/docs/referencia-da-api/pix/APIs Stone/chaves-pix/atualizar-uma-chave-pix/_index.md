---
title: "Atualizar chaves Pix"
linkTitle: "Atualizar chaves Pix (Beta)"
date: 2021-08-12T19:00:00-03:00
lastmod: 2021-10-14T09:26:00-03:00
weight: 2
draft: false
description: >

---

<br>

```
POST https://sandbox-api.openbank.stone.com.br/api/v1/pix/{{account_id}}/entries/{{entry_id}}
```

<br>

Este endpoint permite que um participante indireto realize a atualização dos dados de uma chave Pix.
Somente chaves com status `key_created` (que estejam em posse do dono da conta) podem ser atualizadas.

Os seguintes campos podem ser atualizados:
  * branch_code
  * account_code
  * account_type
  * created_at
  * name
  * legal_name
<br>

##### **HEADERS**

---

**x-stone-idempotency-key** `string`
<br>Chave de idempotência

**authorization** `string`
<br> Bearer Token

**User-Agent** `string`
<br> Nome da sua aplicacão
<br>

##### **PATH PARAMS**

---

**account_id** `string`
<br> Identificador da conta
<br>Format: `UUID`

**entry_id** `string`
<br> Identificador da chave Pix a ser atualizada
<br>Format: `UUID`
<br>

##### **BODY PARAMS**

---

**participant_ispb** `string`
<br> ISPB do Participante Indireto

**reason** `string`
<br> Valores permitidos: `branch_transfer` ou `user_requested`

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
<br><br>

**- Para atualizar uma chave aleatória**

```json
{
    "id": "fa4c35c2-a181-11ec-b909-0242ac120002",
    "participant_ispb": "16501555",
    "beneficiary_account": {
      "account_code": "123456",
      "branch_code": "0001",
      "account_type": "PG",
      "created_at": "2021-01-01T01:30:00Z"
    },
    "beneficiary_entity": {
      "legal_name": "John Doe SA",
      "name": "John Doe",
      "document": "44015829000133",
      "document_type": "cnpj"
    }
}
```

<br> <br>

##### **Responses**

---

```
202 ACCEPTED
content-type: application/json
```

Body

```json
{
  "id": "fa4c35c2-a181-11ec-b909-0242ac120002"
}
```

---

```
400 BAD REQUEST
```

---

```
422 DOMAIN ERROR
```

Body
```json
{
  "type": "srn:error:already_updated"
}
```
Acontece quando a chave já está atualizada com base nos parâmetros enviados
<br>

Body
```json
{
  "type": "srn:error:already_updated"
}
```
Acontece quando a chave está com um status diferente de `key_created`.
<br><br>
