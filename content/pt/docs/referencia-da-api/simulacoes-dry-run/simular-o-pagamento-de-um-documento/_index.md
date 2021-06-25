---
title: "Simular o Pagamento de Um Documento"
slug: "simular-o-pagamento-de-um-documento"
hidden: false
date: 2019-04-01T20:21:16.934Z
lastmod: 2020-06-04T00:43:25.396Z
weight: 4
---

---

```
POST https://sandbox-api.openbank.stone.com.br/api/v1/dry_run/payments
```

---

#### **BODY PARAMS**

---

<br>

**barcode**  `string`

Código de barras do documento.

---
<br>

**account_id**  `string`

Identificador da conta pagadora

<br>

---
#### **HEADERS**

---
<br>

**x-stone-idempotency-key**  `string`

Chave de idempotência

<br>

---

##### Results Params

| Chave                    | Descrição                                                                                                                                                              |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| document_type            | Tipo do documento, podendo ser um dentre os valores à seguir: 'boleto' ou 'concessionaria'                                                                             |
| payment_being_processed? | Indica se a Stone já recebeu uma solicitação de pagamento deste documento e ainda está processando a solicitação. Em caso de "true" não deve ser feito novo pagamento. |

<br>

---

##### **Response**

```
200 ok
content-type: application/json
```
Body
```json
{
    "account_id": "79d8449d-94f7-454d-9a37-6f053748058f",
    "amount": 15000,
    "approval_expired_at": null,
    "approved_at": "2021-05-20T17:58:59Z",
    "approved_by": "user:893c0cfb-166f-4233-a97d-02c5943cebe0",
    "barcode": "19796863300000150000000025300979370888041628",
    "barcode_details": {
        "bank_code": "197",
        "bank_name": "STONE PAGAMENTOS S.A.",
        "barcode": "19796863300000150000000025300979370888041628",
        "expiration_date": "2021-05-27",
        "face_value": 15000,
        "writable_line": "19790000052530097937108880416287686330000015000"
    },
    "cancelled_at": null,
    "cancelled_by": null,
    "created_at": "2021-05-20T17:58:59Z",
    "created_by": "user:893c0cfb-166f-4233-a97d-02c5943cebe0",
    "details": {
        "payer_trade_name": "E",
        "divergent_amount_auth_type": 3,
        "interest_value": 0,
        "updatable_value": null,
        "min_value": 8000,
        "payer_cpf_cnpj": "11725907020",
        "payment_limit_date": "2021-05-27",
        "writable_line": "19790000052530097937108880416287686330000015000",
        "total_discounted_value": null,
        "barcode": "19796863300000150000000025300979370888041628",
        "accepts_partial_payment": false,
        "interest_date": null,
        "status": "payable",
        "recipient_name": "Nome do CPF 11725907020",
        "payment_end_time": null,
        "discounts": [{
            "date": null
        }],
        "bank_name": null,
        "discount_value": 0,
        "fine_value": 0,
        "document_payment_type": "33",
        "total_added_value": null,
        "unpayable_reason_code": null,
        "value": 15000,
        "unpayable_reason_description": null,
        "payer_legal_name": "Nome do CPF 11725907020",
        "payment_start_time": null,
        "face_value": 15000,
        "document_type": "boleto",
        "settlement_date": null,
        "fine_date": null,
        "max_value": 15000,
        "expiration_date": "2021-05-27",
        "recipient_cpf_cnpj": "11725907020",
        "accepts_partial_payment": true,
        "number_of_partials": 2
    },
    "failed_at": null,
    "failure_reason_code": null,
    "failure_reason_description": null,
    "fee": 0,
    "finished_at": null,
    "id": null,
    "idempotency_key": null,
    "payment_being_processed?": false,
    "refund_reason_code": null,
    "refund_reason_description": null,
    "refunded_at": null,
    "rejected_at": null,
    "rejected_by": null,
    "request_id": "7d9abd369b0a19a3e26fc6b3e2f52f8c",
    "scheduled_to": null,
    "status": "APPROVED",
    "writable_line": "19790000052530097937108880416287686330000015000"
}
```
