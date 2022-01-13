---
title: "Aprovar Operações em Lote"
slug: "aprovar-operacoes"
date: 2022-01-13T18:00:00.687Z
lastmod: 2022-01-13T18:00:00.687Z
weight: 2
draft: false
description: >

---
<br>

Este endpoint realiza a aprovação em lote de operações pendentes para uma conta.

```
POST https://sandbox-api.openbank.stone.com.br/api/v1/account/{account_id}/operations/actions/approve
```

Existem 2 ações possíveis nessa API:
* **approve_only**: aprova apenas as operações passadas no campo **operations**
* **approve_all_except** aprova todas as operações dessa conta exceto as passadas na lista **operations**

Esta API tem um limite de 1000 operações na lista.

Tipos de operações que podem ser aprovadas:

- `external_transfer` (TED)
- `internal_transfer` (Pagamento Interno)
- `barcode_payment` (Pagamento de Boleto)
- `pix_payment` (Pix)
- `refund_for_pix_payment` (Devolução de um Pix)

<br>

##### **HEADERS**
---

**x-stone-idempotency-key** `string`
<br>Chave de idempotência

**authorization** `string`
<br> Bearer Token

**User-Agent** `string`
<br>Nome da sua aplicacão

<br>

##### **QUERY PARAMS**
---

**account_id** `string`
<br> Identificador da conta
<br> <br> 

<br>

##### **BODY PARAMS**
---
<br>

**action** `string`

**operations** `list`

**operations** <br>Dados das operações
  <br>&nbsp;&nbsp;&nbsp;&nbsp;**id** `string`
  <br>&nbsp;&nbsp;&nbsp;&nbsp;**type** `string`

<br>

**- Para aprovar um pagamento Pix**


```json
{
  "action": "approve_only",
  "operations": [{
      "id": "b14bd4ba-4476-43ef-baf6-58c8524830b3/",
      "type": "pix_payment"
  }]   
}

```



<br> <br> 
##### **Response**
---

```
202 ACCEPTED
content-type: application/json
```

Body
```json
{
  "number_of_approvals": 1
}
```

---
