---
title: "Criar Cobranças com Validade"
linkTitle: "Criar Cobranças com Validade"
date: 2021-06-16T15:17:00-03:00
lastmod: 2021-06-16T15:17:00-03:00
weight: 4
description: >
  
---

Através desse endpoint será possível criar cobranças Pix com vencimento.


```
GET https://sandbox-api.openbank.stone.com.br/api/v1/pix_payment_invoices_with_due_date
```
<br>

##### **HEADERS**
---

**authorization*** `string`
<br> Bearer token de autenticação.

**x-stone-idempotency-key*** `string`
<br> Chave de idempotência.

<br>

##### **BODY PARAMS**
---
<br>

**transaction_id*** `string`
<br>Validação: "^[a-zA-Z0-9]{26,35}$"

**account_id** `string`

**additional_data** `object` <br>
**name*** `string` <br>
Tamanho: min 1 / max 50
**value*** `string` <br>
Tamanho: min 1 / max 200

**amount** `integer`

**customer** `object`<br>
**document*** `string` <br>
**name*** `string` <br>

**expiration_date*** `string`
<br>Format: date

**key*** `string`

**request_for_payer** `string`

**payment** `integer`

**only_business_days** `boolean`

**fine** `object`
**type** `string` <br>
Valores aceitos: `fixed`, `proportional` <br>
**fixed_value** `integer`
**proportional_value** `object` <br>
Representação de porcentagem, dada a seguinte fórmula: `coefficient * 10^exponent`<br>
**coefficient*** `integer`
**exponent*** `integer`

**reduction** `object`
**type** `string` <br>
Valores aceitos: `fixed`, `proportional` <br>
**fixed_value** `integer`
**proportional_value** `object` <br>
Representação de porcentagem, dada a seguinte fórmula: `coefficient * 10^exponent`<br>
**coefficient*** `integer`
**exponent*** `integer`

**interest** `object`
**type** `string` <br>
Valores aceitos: `fixed`, `proportional` <br>
**period** `string` <br>
Valores aceitos: `day`, `month`, `year` <br>
**fixed_value** `integer`
**proportional_value** `object` <br>
Representação de porcentagem, dada a seguinte fórmula: `coefficient * 10^exponent`<br>
**coefficient*** `integer`
**exponent*** `integer`

**discount** `object`
**type** `string` <br>
Valores aceitos: `fixed`, `proportional` <br>
**calculation_mode** `string` <br>
Valores aceitos: `date`, `period` <br>
**period_discount** `object`
**date_discounts** `object`
**date** `string`
**fixed_value** `integer`
**proportional** `object` <br>
Representação de porcentagem, dada a seguinte fórmula: `coefficient * 10^exponent`<br>
**coefficient*** `integer`
**exponent*** `integer`


Exemplo:

```json
{
  "type": "object",
  "properties": {
    "transaction_id": {
      "type": "string",
      "pattern": "^[a-zA-Z0-9]{26,35}$"
    },
    "account_id": {
      "type": "string",
      "format": "uuid"
    },
    "additional_data": {
      "type": [
        "array",
        "null"
      ],
      "maxItems": 50,
      "items": {
        "type": "object",
        "required": [
          "name",
          "value"
        ],
        "properties": {
          "name": {
            "type": "string",
            "minLength": 1,
            "maxLength": 50
          },
          "value": {
            "type": "string",
            "minLength": 1,
            "maxLength": 200
          }
        }
      }
    },
    "amount": {
      "type": "integer"
    },
    "customer": {
      "type": "object",
      "required": [
        "document",
        "name"
      ],
      "properties": {
        "document": {
          "type": "string"
        },
        "name": {
          "type": "string"
        }
      }
    },
    "expiration_date": {
      "type": "string",
      "format": "date"
    },
    "key": {
      "type": "string"
    },
    "request_for_payer": {
      "type": [
        "string",
        "null"
      ]
    },
    "payment_limit_pediod_days": {
      "type": "integer"
    },
    "only_business_days": {
      "type": "boolean"
    },
    "fine": {
      "type": "object",
      "properties": {
        "type": {
          "type": "string",
          "enum": [
            "fixed",
            "proportional"
          ]
        },
        "fixed_value": {
          "type": [
            "integer",
            "null"
          ]
        },
        "proportional_value": {
          "type": "object",
          "title": "Porcentagem",
          "required": [
            "coefficient",
            "exponent"
          ],
          "description": "Representação de porcentagem, dada a seguinte fórmula: `coefficient * 10^exponent`",
          "properties": {
            "coefficient": {
              "type": "integer"
            },
            "exponent": {
              "type": "integer"
            }
          }
        }
      }
    },
    "reduction": {
      "type": "object",
      "required": [
        "type"
      ],
      "properties": {
        "type": {
          "type": "string",
          "enum": [
            "fixed",
            "proportional"
          ]
        },
        "fixed_value": {
          "type": [
            "integer",
            "null"
          ]
        },
        "proportional_value": {
          "type": "object",
          "title": "Porcentagem",
          "required": [
            "coefficient",
            "exponent"
          ],
          "description": "Representação de porcentagem, dada a seguinte fórmula: `coefficient * 10^exponent`",
          "properties": {
            "coefficient": {
              "type": "integer"
            },
            "exponent": {
              "type": "integer"
            }
          }
        }
      }
    },
    "interest": {
      "type": "object",
      "required": [
        "type",
        "period"
      ],
      "properties": {
        "type": {
          "type": "string",
          "enum": [
            "fixed",
            "proportional"
          ]
        },
        "period": {
          "type": "string",
          "enum": [
            "day",
            "month",
            "year"
          ]
        },
        "fixed_value": {
          "type": [
            "integer",
            "null"
          ]
        },
        "proportional_value": {
          "type": "object",
          "title": "Porcentagem",
          "required": [
            "coefficient",
            "exponent"
          ],
          "description": "Representação de porcentagem, dada a seguinte fórmula: `coefficient * 10^exponent`",
          "properties": {
            "coefficient": {
              "type": "integer"
            },
            "exponent": {
              "type": "integer"
            }
          }
        }
      }
    },
    "discount": {
      "type": "object",
      "required": [
        "type",
        "calculation_mode"
      ],
      "properties": {
        "type": {
          "type": "string",
          "enum": [
            "fixed",
            "proportional"
          ]
        },
        "calculation_mode": {
          "type": "string",
          "enum": [
            "date",
            "period"
          ]
        },
        "period_discount": {
          "type": [
            "object",
            "null"
          ]
        },
        "date_discounts": {
          "type": [
            "object",
            "null"
          ],
          "properties": {
            "date": {
              "type": "string",
              "format": "date"
            },
            "fixed_value": {
              "type": [
                "integer",
                "null"
              ]
            },
            "proportional": {
              "type": "object",
              "title": "Porcentagem",
              "required": [
                "coefficient",
                "exponent"
              ],
              "description": "Representação de porcentagem, dada a seguinte fórmula: `coefficient * 10^exponent`",
              "properties": {
                "coefficient": {
                  "type": "integer"
                },
                "exponent": {
                  "type": "integer"
                }
              }
            }
          }
        }
      }
    }
  },
  "required": [
    "transaction_id",
    "customer",
    "expiration_date",
    "key"
  ]
}
```
<br>

##### **Response**
---

```json
200 OK
```

```json
{
  "account_id": "477f8576-ca82-462b-be73-dc28cc6490c3",
  "additional_data": [
    {
      "name": "Mr. Due",
      "value": "Date"
    }
  ],
  "amount": 555,
  "beneficiary_address": {
    "city": "Rio de JaneiroA",
    "country": "BRA",
    "extra": "A",
    "neighborhood": "FlamengoA",
    "postal_code": "22250120",
    "reference_point": null,
    "state": "RJA",
    "street": "Rua Honório de BarrosoA",
    "street_number": "3A"
  },
  "beneficiary_entity": {
    "document": "91092573062",
    "document_type": "cpf",
    "legal_name": "Gilderoy Lockhart",
    "trade_name": null
  },
  "cancelled_at": null,
  "created_at": "2021-03-19T14:43:55Z",
  "created_by": "user:380f9968-8946-4f88-a781-be8b7efc1f90",
  "customer": {
    "document": "85553990335",
    "document_type": "cpf",
    "name": "Fulano da Silva"
  },
  "discount": null,
  "expiration_date": "2021-03-19",
  "fine": null,
  "id": "b4bdc3df-795e-4d33-9851-15192fb7e216",
  "inbound_pix_payments": [],
  "interest": null,
  "key": "4e4bb64d-d17c-4c53-a51b-44f06e28be06",
  "key_type": "random_key",
  "location": "pix-h.stone.com.br/pix/v2/cobv/b4bdc3df-795e-4d33-9851-15192fb7e216",
  "only_business_days": false,
  "paid_at": null,
  "payment_limit_period_days": 30,
  "qr_code_content": "00020101021226890014br.gov.bcb.pix2567pix-h.stone.com.br/pix/v2/cobv/b4bdc3df-795e-4d33-9851-15192fb7e21652040000530398654045.555802BR5925Nome do CPF 581.360.533-96014RIO DE JANEIRO622905253f6a429254c34b3091847f85d63046EBC",
  "qr_code_image": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAfgAAAH4CAIAAAApSmgoAAA590lEQVR4nO2bMaIjSbIj//0vvauMGvWIpFnDPRlQyxswIB5Tmvm//3d1dXV19Wr9Xxvg6urq6srV/dBfXV1dvVz3Q391dXX1ct0P/dXV1dXLdT/0V1dXVy/X/dBfXV1dvVz3Q391dXX1ch0/9P+3RCk/dW/vluZSPHYvKpfawfb5dpennFSvaTyUT+qf+rR05H9tMfne3i3NpXjsXlQutYPt8+0uTzmpXtN4KJ/UP/Vp6cj/2mLyvb1bmkvx2L2oXGoH2+fbXZ5yUr2m8VA+qX/q09KR/7XF5Ht7tzSX4rF7UbnUDrbPt7s85aR6TeOhfFL/1KelI/9ri8n39m5pLsVj96JyqR1sn293ecpJ9ZrGQ/mk/qlPS0f+1xaT7+3d0lyKx+5F5VI72D7f7vKUk+o1jYfySf1Tn5aO/K8tJt/bu6W5FI/di8qldrB9vt3lKSfVaxoP5ZP6pz4tHflfW0y+t3dLcykeuxeVS+1g+3y7y1NOqtc0Hson9U99Wjry20NTiotRAw0Ttc",
  "reduction": null,
  "request_for_payer": "do something until today",
  "request_id": "f06fe0c17b96d26965b069c73b77153c",
  "status": "ACTIVE",
  "transaction_id": "3f6a429254c34b3091847f85da88eb65",
  "updated_at": "2021-03-19T14:43:55Z"
}
```

---

```json
400 Bad Request
```

```json
{
  "reason": [
    {
      "error": "is invalid",
      "path": [
        "key_type"
      ]
    },
    {
      "error": "is invalid",
      "path": [
        "status"
      ]
    }
  ],
  "type": "srn:error:validation"
}
```

---

```json
401 Unauthorized
```

```json
{
  "type": "srn:error:unauthorized"
}
```

---

```json
403 Forbidden
```

```json
{
  "type": "srn:error:unauthenticated"
}
```

---

```json
409 Conflict
```

```json
{
  "type": "srn:error:idempotency_conflict"
}
```

---

```json
422 Unprocessable
```

```json
{
  "reason": [
    {
      "error": "has already been taken",
      "path": [
        "transaction_id"
      ]
    }
  ],
  "type": "srn:error:unprocessable_entity"
}
```
