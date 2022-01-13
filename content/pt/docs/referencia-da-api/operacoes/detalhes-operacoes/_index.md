---
title: "Detalhe de Operações"
slug: "detalhes-operacoes"
hidden: false
date: 2022-01-13T18:00:00.687Z
lastmod: 2022-01-13T18:00:00.687Z
weight: 3
---

<br>

Exibe os detalhes de uma operação.

```
GET https://sandbox-api.openbank.stone.com.br/api/v1/accounts/{account_id}/operations/{operation_id}
```
<br>

O type da operação deve ser obrigatoriamente passado como query param:
* operations/{operation_id}?*type=pix_payment*

Os tipos de operação podem ser:

- `external_transfer` (TED)
- `internal_transfer` (Pagamento Interno)
- `barcode_payment` (Pagamento de Boleto)
- `pix_payment` (Pix)
- `refund_for_pix_payment` (Devolução de um Pix)

---

#### **PATH PARAMS**
---

**account_id**  `string`

Identificador da conta.

**oepration_id**  `string`

Identificador da transação.

<br>

---

#### **QUERY PARAMS**
---

**type**  `string`

Tipo da operação detalhada

---

#### **Response**

```
200 ok
content-type: application/json
```
Body

```json

{
    "account_id": "7d3c993d-72fe-4739-8176-5ad3a49db9d6",
    "agent": {
        "entity": {
            "name": "Joao Kuririn",
            "document": "12312312312",
            "document_type": "cpf"
        },
        "institution": {
            "name": "Stone Pagamentos S.A.",
            "compe": "197",
            "ispb": "16501555"
        },
        "account": {
            "account_type": "PG",
            "branch_code": null,
            "account_code": "111"
        }
    },
    "amount": -39511,
    "counterparty_agent": {
        "account": {
            "account_code": "1231",
            "account_type": "CC",
            "branch_code": "0001"
        },
        "entity": {
            "document": "***236927**",
            "document_type": "cpf",
            "name": "John Doe"
        },
        "institution": {
            "compe": "0001",
            "ispb": "16501555",
            "name": "Stone Pagamentos S.A."
        }
    },
    "created_at": "2022-01-07T17:38:32Z",
    "created_by": "user:d52a70e9-3bc3-4e50-8d11-fa82b1113931",
    "fee": null,
    "id": "c689f4fd-6700-4877-8e9f-d92ada862eba",
    "operations_details": null,
    "scheduled_to": "2022-01-17",
    "status": "SCHEDULED",
    "subtitle": "Pix",
    "title": "John Doe",
    "type": "pix_payment"
}
```
