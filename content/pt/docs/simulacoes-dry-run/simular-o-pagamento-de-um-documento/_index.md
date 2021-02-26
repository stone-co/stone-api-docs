---
title: "Simular o Pagamento de Um Documento"
slug: "simular-o-pagamento-de-um-documento"
hidden: false
date: 2019-04-01T20:21:16.934Z
lastmod: 2020-06-04T00:43:25.396Z
weight: 4
---

```http
POST https://sandbox-api.openbank.stone.com.br/api/v1/dry_run/payments
```

---

**BODY PARAMS**

---

**barcode**  `string`

Código de barras do documento.

---

**account_id**  `string`

Identificador da conta pagadora

---
**HEADERS**

---

**x-stone-idempotency-key**  `string`

Chave de idempotência

---

###### Results Params

| Chave                    | Descrição                                                                                                                                                              |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| document_type            | Tipo do documento, podendo ser um dentre os valores à seguir: 'boleto' ou 'concessionaria'                                                                             |
| payment_being_processed? | Indica se a Stone já recebeu uma solicitação de pagamento deste documento e ainda está processando a solicitação. Em caso de "true" não deve ser feito novo pagamento. |

---

##### Response

```http
200 ok
content-type: application/json
```

```JSON
{
    "account_id": "477f8576-ca82-462b-be73-dc28cc6490c3",
    "amount": 2000,
    "approval_expired_at": null,
    "approved_at": "2020-01-30T21:35:20Z",
    "approved_by": "application:c6738911-0a75-4ba0-9d55-48c11935aabb",
    "barcode": "84680000000737300480011025546608407195190810",
    "barcode_details": {
        "bank_code": "237",
        "bank_name": "BCO BRADESCO S.A.",
        "barcode": "84680000000737300480011025546608407195190810",
        "expiration_date": "2020-01-24",
        "face_value": 2000,
        "writable_line": "846800000008737300480016102554660849071951908103"
    },
    "cancelled_at": null,
    "cancelled_by": null,
    "created_at": "2020-01-30T21:35:20Z",
    "created_by": "user:380f9969-8946-4f88-a781-be8b7efc1f90",
    "details": {
        "bank_name": null,
        "barcode": "84680000000737300480011025546608407195190810",
        "discount_value": null,
        "document_payment_type": null,
        "document_type": "boleto",
        "expiration_date": "2020-01-24",
        "face_value": 2000,
        "fine_value": null,
        "interest_value": null,
        "max_value": null,
        "min_value": null,
        "payer_cpf_cnpj": "06489863000150",
        "payer_legal_name": null,
        "payer_trade_name": "Fadel-Hahn",
        "payment_end_time": null,
        "payment_limit_date": 2020-01-27,
        "payment_start_time": null,
        "recipient_cpf_cnpj": "98146856000174",
        "recipient_name": "Sra. Mirella",
        "settlement_date": null,
        "status": "unpayable",
        "total_added_value": null,
        "total_discounted_value": null,
        "updatable_value": null,
        "value": 2000,
        "writable_line": "846800000008737300480016102554660849071951908103"
    },
    "failed_at": null,
    "failure_reason_code": null,
    "failure_reason_description": null,
    "fee": 0,
    "finished_at": null,
    "id": null,
    "payment_being_processed?":false,
    "refunded_at": null,
    "rejected_at": null,
    "rejected_by": null,
    "scheduled_to": null,
    "status": "APPROVED",
    "writable_line": "846800000008737300480016102554660849071951908103"
}
```
