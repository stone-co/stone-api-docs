---
title: "Como Emitir Um Comprovante"
linkTitle: "Como Emitir Um Comprovante"
slug: "como-emitir-um-comprovante"
hidden: false
date: 2020-09-17T18:00:00-03:00
lastmod: 2020-09-17T18:00:00-03:00
description: >
---
### Como Emitir Um Comprovante

Comprovantes informam sobre uma transação em detalhes, como fonte, destinatário e estado.

As operações que podem ter seu comprovante gerado são apenas as operações: Pagamento com código de barras, envio de TEDs, envio de transferências internas e extrato.

Comprovantes podem ser gerados apenas para transferências em estados de sucesso, como aprovada e agendada.

Comprovantes para extrato aceitam os parâmetros adicionais `start_datetime` e `end_datetime` para especificar o intervalo de tempo cujas entradas serão levadas em consideração ao gerar o comprovante.

```http
POST https://sandbox-api.openbank.stone.com.br/api/v1/receipts
Content-Type: application/json
x-stone-idempotency-key: "jwt_token"
{
    "resource_type": "external_transfer",
    "resource_id": "2e3d6ed0-d442-41eb-8a3c-2a6d5da92dc9",
    "start_datetime": "2020-12-31T00:00:00Z",
    "end_datetime": "2021-01-01T00:00:00Z"
}

200 OK
```

---

#### REQUEST BODY PARAMS

---

##### resource_type

- Type: `string`
- Allowed values: `external_transfer`, `internal_transfer`, `payment` e `statement`

##### resource_id

- Type: `UUID`

##### start_datetime

- Type: `Datetime`
- Format: `ISO8601 - "YYYY-MM-DDThh:mm:ssZ"`
- Example: `"2021-01-01T00:00:00Z"`

##### end_datetime

- Type: `Datetime`
- Format: `ISO8601 - "YYYY-MM-DDThh:mm:ssZ"`
- Example: `"2021-01-01T00:00:00Z"`

---

#### HEADERS

---

- x-stone-idempotency-key: `string`

---

#### RESPONSE

---

- Sucesso:
  - 200 OK
  - Retorna o PDF do comprovante
