---
title: "Como Emitir Um Comprovante"
linkTitle: "Como Emitir Um Comprovante"
slug: "como-emitir-um-comprovante"
hidden: false
date: 2020-09-17T18:00:00-03:00
lastmod: 2020-09-17T18:00:00-03:00
description: >
---

Comprovantes informam sobre uma transação em detalhes, como fonte, destinatário e estado.

As operações que podem ter seu comprovante gerado são apenas as operações: Pagamento com código de barras, envio de TEDs, envio de transferências internas e extrato.

Comprovantes podem ser gerados apenas para transferências em estados de sucesso, como aprovada e agendada.

Comprovantes para extrato aceitam os parâmetros adicionais `start_datetime` e `end_datetime` para especificar o intervalo de tempo cujas entradas serão levadas em consideração ao gerar o comprovante.

```http
POST https://sandbox-api.openbank.stone.com.br/api/v1/receipts
```

---

##### **BODY PARAMS**

---

**resource_type*** `string`
<br>Allowed values: `external_transfer`, `internal_transfer`, `payment` e `statement`

**resource_id*** `string`
<br>Format: `UUID`

**start_datetime** `string`
<br>Format: `ISO8601 - "YYYY-MM-DDThh:mm:ssZ"`
<br>Example: `"2021-01-01T00:00:00Z"`

**end_datetime** `string`
<br>Format: `ISO8601 - "YYYY-MM-DDThh:mm:ssZ"`
<br>Example: `"2021-01-01T00:00:00Z"`

---

#### HEADERS

---

**x-stone-idempotency-key** `string`

---

#### **Response**

```JSON
200 OK
content-type: application/json
```

Retorna o PDF do comprovante
