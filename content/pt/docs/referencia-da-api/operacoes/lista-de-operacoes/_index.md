---
title: "Listar Operações"
slug: "listar-operacoes"
hidden: true
date: 2022-01-13T18:00:00.687Z
lastmod: 2022-01-13T18:00:00.687Z
weight: 3
draft: true
---

<br>

Para listar operações não executadas, você deve utilizar o endpoint abaixo:


```
GET https://sandbox-api.openbank.stone.com.br/api/v1/accounts/{account_id}/operations
```
<br>

Este endpoint lista as operações de uma conta que não foram executadas até o momento da consulta. O query param **status** é obrigatório e através dele é possível filtrar por 2 tipos de operações:

* Agendamentos usando o filtro *?status=SCHEDULED*
* Operações pendentes de aprovação usando o filtro *?status=PENDING_APPROVAL*

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

<br>

---

#### **QUERY PARAMS**

---

**after**  `string`

Cursor da paginação.

**before**  `string`

Cursor da paginação.

**limit**  `string`

Quantidade de itens trazidos na paginação.

**status**  `string`

Filtra operações pelo tipo de status(SCHEDULED, PENDING_APPROVAL).

---

#### **Response**

```
200 ok
content-type: application/json
```
Body
```json
{
  "cursor": {
    "after": null,
    "before": null,
    "limit": 25
  },
  "data": [
    {
      "account_id": "e6b237af-e1d4-49e1-b727-399df7507766",
      "id": "6c15e682-ed02-4a1a-be6a-ea8deebf251b",
      "type": "barcode_payment",
      "status": "SCHEDULED",
      "fee": -10,
      "amount": -100,
      "subtitle": null,
      "title": "Agendamento",
      "counterparty_agent": {
        "entity": {
          "name": "John Kuririn",
          "document": "47647430351",
          "document_type": "cpf"
        },
        "institution": {
          "name": "Stone Pagamentos S.A."
        }
      }
    },
    {
      "created_at": "2020-08-20T19:07:53Z",
      "created_by": "user:efabb7a7-122a-4e35-9437-7f4321d4d3f9",
      "fee": -10,
      "amount": -10000,
      "account_id": "e6b237af-e1d4-49e1-b727-399df7507766",
      "id": "86e9a057-01bd-4b3c-bec5-261049f03db0",
      "type": "external_transfer",
      "status": "SCHEDULED",
      "scheduled_to": "2020-08-20",
      "subtitle": "Agendamento | TED",
      "title": "Fulano do outro banco",
      "counterparty_agent": {
        "entity": {
          "name": "John Doe",
          "document": "47647430351",
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
          "account_code": "14363907"
        }
      }
    }
  ]
}
```
