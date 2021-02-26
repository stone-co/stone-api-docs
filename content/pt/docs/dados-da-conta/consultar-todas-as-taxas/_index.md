---
title: "Consultar Todas as Taxas"
slug: "consultar-todas-as-taxas"
hidden: true
date: 2019-02-19T19:30:26.314Z
lastmod: 2019-12-02T22:56:58.127Z
weight: 12
---

---

```http
GET https://sandbox-api.openbank.stone.com.br/api/v1/accounts/account_id/fees
```

---

**PATH PARAMS**

---

**account_id**  `string`

Identificador da conta.

---

##### Response

```http
201 OK
content-type: application/json
```

```JSON
{
  "cursor": {
    "after": null,
    "before": null,
    "limit": 25
  },
  "data": [
    {
      "amount": 0,
      "fee_type": "barcode_payment"
    },
    {
      "amount": 0,
      "fee_type": "external_transfer",
      "original_fee": 200,
      "billing_exemption_participant": true,
      "max_free_transfers": 20,
      "remaining_free_transfers": 3
    },
    {
      "amount": 0,
      "fee_type": "internal_transfer"
    },
    {
      "amount": 100,
      "fee_type": "boleto_issuance"
    },
    {
      "amount": 0,
      "fee_type": "outbound_stone_prepaid_card_payment"
    },
    {
      "amount": 650,
      "fee_type": "outbound_stone_prepaid_card_withdrawal"
    },
    {
      "amount": 200,
      "fee_type": "barcode_payment_invoice",
      "original_fee": 200,
      "billing_exemption_participant": true,
      "max_free": 20,
      "remaining_free": 3
    }
  ]
}
```
