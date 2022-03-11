---
title: "Excluir chave Pix"
linkTitle: "Excluir chave Pix"
date: 2021-07-15T14:00:00-03:00
lastmod: 2021-07-15T14:00:00-03:00
weight: 3
draft: false
description: >
   
---
<br>

Para deletar uma chave Pix você deve usar o endpoint abaixo:

```
DELETE /api/v1/pix/{{account_id}}/entries/{{id}}
```

##### **HEADERS**
---

**x-stone-idempotency-key** `string`
<br>Chave de idempotência

**authorization** `string`
<br> Bearer Token

**User-Agent** `string`
<br>Nome da sua aplicacão

<br>

##### **PATH PARAMS**
---

**account_id** `string`
<br> Identificador da conta 

**id** `string`
<br> Identificador da chave a ser deletada. Caso não saiba o `id` da chave, liste as chaves da conta por esse [endpoint]({{< relref "/docs/referencia-da-api/pix/chaves-pix/listar-chaves-pix/">}}) e pegue o `id`.
<br><br>

##### **BODY PARAMS**
---

Na requisição deve-se informar informar a razão pela qual deseja excluir aquela chave:<br>
Exemplo: "reason": "user_requested" - significa que foi um pedido da cliente final

```json
{
  "key_type": “phone”,
  "participant_ispb": “1234567890”,
  "beneficiary_account": {
     "branch_code": “0001”,
     "account_code": "00016583",
     "account_type": "CC",
     "opened_at": "2019-11-18T03:00:00Z"
  },
  "reason": "user_requested"
}
```
<br> <br> 

##### **RESPONSE**

```
202 ACCEPTED
content-type: application/json
```
**Body**

```text
{
  "id": “4b612bce-f964-11ea-adc1-0242ac120002”
}
```
<br> <br> 


##### **Webhook de exclusão de uma chave**
Serão disparados webhooks quando o status da solicitação sofrer alterações, são eles:
- **pix_entries_delete_requested** : requisição de exclusão feita e em andamento
- **pix_entries_deleted** : chave deletada
- **pix_entries_deletion_failed** : falha na exclusão da chave


Veja [aqui]({{< relref "/docs/referencia-da-api/pix/#status-de-um-pix">}}) os possíveis status para uma solicitação.

As seguintes informações virão no campo `target_data` dos webhooks:

```json
{
  "id": “4b612bce-f964-11ea-adc1-0242ac120002”
  “key”: “+5510998765432”,
  “key_type”: "phone"
  “key_status”: “deleted”,
  “beneficiary_id”: “bad7ab7e-f95d-11ea-adc1-0242ac120002”,
   "created_at": “20200- 09-18T03:00:00Z”,
   "error_description": “”,
   "status": “accepted"
}
```
<br> <br> 
