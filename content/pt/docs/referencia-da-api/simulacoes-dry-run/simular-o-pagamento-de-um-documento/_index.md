---
title: "Simular o Pagamento de Um Documento"
slug: "simular-o-pagamento-de-um-documento"
hidden: false
date: 2019-04-01T20:21:16.934Z
lastmod: 2020-06-04T00:43:25.396Z
weight: 4
---

```shell
POST https://sandbox-api.openbank.stone.com.br/api/v1/dry_run/payments
```

#### **HEADERS**

---

**Authorization** `string` _(obrigatório)_

Bearer token de autenticação

**x-stone-idempotency-key** `string` _(obrigatório)_

Chave de idempotência

#### **BODY PARAMS**

---

**barcode** `string` _(obrigatório)_

Código de barras do documento.

**account_id** `string` _(obrigatório)_

Identificador da conta pagadora

**scheduled_to** `string`

Data de agendamento para o pagamento

**amount** `integer`

Valor do pagamento

##### **RESULT PARAMS**

| Chave                    | Descrição                                                                                                                                                              | Tipo      | Regra de Negócio                      |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- | ------------------------------------- |
| account_id               | Identificador da conta pagadora                                                                                                                                        | _String_  | Obrigatório                           |
| amount                   | Valor do pagamento                                                                                                                                                     | _Integer_ | Obrigatório                           |
| barcode                  | Código de barras do pagamento                                                                                                                                          | _String_  | Obrigatório                           |
| barcode_details          | Informações extraídas do código de barras                                                                                                                              | _Object_  | [Detalhes do objeto](#barcodedetails) |
| details                  | Informações acerca do status do pagamento de acordo com a sua fonte emissora                                                                                           | _Object_  | [Detalhes do objeto](#details)        |
| payment_being_processed? | Indica se a Stone já recebeu uma solicitação de pagamento deste documento e ainda está processando a solicitação. Em caso de “true” não deve ser feito novo pagamento. | _Boolean_ | Obrigatório                           |

###### BarcodeDetails

| Chave           | Descrição                                                                | Tipo      | Regra de negócio                                                               |
| --------------- | ------------------------------------------------------------------------ | --------- | ------------------------------------------------------------------------------ |
| bank_code       | Código numérico da instituição que emitiu o documento                    | _String_  | Obrigatório para boletos bancários, opcional para pagamentos de concessionária |
| bank_name       | Nome da instituição que emitiu o documento                               | _String_  | Obrigatório para boletos bancários, opcional para pagamentos de concessionária |
| barcode         | Código de barras do documento                                            | _String_  | Obrigatório                                                                    |
| expiration_date | Data de vencimento do documento                                          | _String_  | Opcional                                                                       |
| face_value      | Valor com o qual o documento foi criado e que consta no código de barras | _Integer_ | Obrigatório                                                                    |
| writable_line   | Código numérico que acompanha o código de barras                         | _String_  | Obrigatório                                                                    |

###### Details

| Chave                  | Descrição                                                                                   | Tipo      | Regra de Negócio                                                                                     |
| ---------------------- | ------------------------------------------------------------------------------------------- | --------- | ---------------------------------------------------------------------------------------------------- |
| bank_name              | Nome da instituição que emitiu o documento.                                                 | _String_  | Opcional                                                                                             |
| barcode                | Código de barras.                                                                           | _String_  | Obrigatório                                                                                          |
| discount_value         | Valor do desconto que está sendo aplicado ao boleto.                                        | _Integer_ | `null` caso não haja disconto sendo aplicado                                                         |
| document_payment_type  | Informa o código referente a título.                                                        | _Integer_ | [Possíveis valores](#document_payment_type)                                                          |
| document_type          | Informa o tipo de documento.                                                                | _String_  | `"boleto"` ou `"concessionaria"`                                                                     |
| expiration_date        | Data de vencimento                                                                          | _String_  | Opcional                                                                                             |
| face_value             | Valor com o qual o documento foi criado e que consta do código de barras.                   | _Integer_ | Opcional                                                                                             |
| fine_value             | Valor da multa que está sendo aplicada ao boleto.                                           | _Integer_ | `null` caso nenhuma multa esteja sendo aplicada                                                      |
| interest_value         | Valor dos juros que estão sendo aplicados ao boleto.                                        | _Integer_ | `null` caso não hajam juros sendo aplicados                                                          |
| max_value              | Valor máximo que será aceito no pagamento deste documento.                                  | _Integer_ | Opcional                                                                                             |
| min_value              | Valor mínimo que será aceito no pagamento deste documento.                                  | _Integer_ | Opcional                                                                                             |
| payer_cpf_cnpj         | Número do documento do pagador sem pontos.                                                  | _String_  | Opcional                                                                                             |
| payer_legal_name       | É o nome que identifica o pagador para fins legais, administrativos e outros fins oficiais. | _String_  | Opcional                                                                                             |
| payer_trade_name       | Nome fantasia do pagador.                                                                   | _String_  | Opcional                                                                                             |
| payment_limit_date     | Data limite para pagamento do documento.                                                    | _String_  | Opcional. Formato ISO8601 `YYYY-MM-DD`.                                                              |
| payment_start_time     | Horário a partir do qual o pagamento é possível em um dia útil.                             | _String_  | Respeita o `payment_limit_date`. Formato `hh:mm:ss`.                                                 |
| payment_end_time       | Horário até o qual o pagamento é possível em um dia útil.                                   | _String_  | Respeita o `payment_limit_date`. Formato `hh:mm:ss`.                                                 |
| recipient_cpf_cnpj     | Número do documento do beneficiário sem pontos.                                             | _String_  | Opcional                                                                                             |
| recipient_name         | Nome do beneficiário.                                                                       | _String_  | Opcional                                                                                             |
| settlement_date        | Data em que o dinheiro do pagamento do boleto é depositado na conta do beneficiário.        | _String_  | Formato ISO8601 `YYYY-MM-DDThh:mm:ssZ`. Caso o boleto ainda não tenha sido pago o valor será `null`. |
| status                 | Status atual do documento na sua instituição emissora.                                      | _String_  | `"payable"`, `"paid"` ou `"unpayable"`.                                                              |
| total_added_value      | Total que foi adicionado ao valor original do documento decorrente de juros e multas.       | _Integer_ | Retornado somente em pagamentos de concessionária                                                    |
| total_discounted_value | Total que foi abatido do valor originial do documento decorrente de descontos.              | _Integer_ | Retornado somente em pagamentos de concessionária                                                    |
| updatable_value        | Indica se é permitido alterar o valor do documento.                                         | _Boolean_ | Retornado somente em pagamentos de concessionária                                                    |
| value                  | Valor atualizado já com descontos, multas e juros que se aplicam.                           | _Integer_ | Opcional                                                                                             |
| writable_line          | Código numérico que acompanha o código de barras.                                           | _String_  | Obrigatório                                                                                          |
| unpayable_reason_code  | Código que representa o motivo de estar impagável.                                          | _String_  | Retornado somente se o status do documento for `"unpayable"`, caso contrário será `null`             |

---

###### document_payment_type

| Domínio | Descrição                           |
| ------- | ----------------------------------- |
| 1       | CH Cheque                           |
| 2       | DM Duplicata Mercantil.             |
| 3       | DMI Duplicata Mercantil Indicação.  |
| 4       | DS Duplicata de Serviço.            |
| 5       | DSI Duplicata de Serviço Indicação. |
| 6       | DR Duplicata Rural.                 |
| 7       | LC Letra de Câmbio.                 |
| 8       | NCC Nota de Crédito Comercial.      |
| 9       | NCE Nota de Crédito Exportação.     |
| 10      | NCI Nota de Crédito Industrial.     |
| 11      | NCR Nota de Crédito Rural.          |
| 12      | NP Nota Promissória.                |
| 13      | NPR Nota Promissória Rural.         |
| 14      | TM Triplicata Mercantil.            |
| 15      | TS Triplicata de Serviço.           |
| 16      | NS Nota de Seguro.                  |
| 17      | RC Recibo.                          |
| 18      | FAT Bloqueio.                       |
| 19      | ND Nota de Débito.                  |
| 20      | AP Apólice de Seguro.               |
| 21      | ME Mensalidade Escolar.             |
| 22      | PC Parcela de Consórcio.            |
| 23      | NF Nota Fiscal.                     |
| 24      | DD Documento de Dívida.             |
| 25      | Cédula de Produto Rural.            |
| 26      | Warrant.                            |
| 27      | Dívida Ativa de Estado.             |
| 28      | Dívida Ativa do Município.          |
| 29      | Dívida Ativa da União.              |
| 30      | Encargos Condominiais.              |
| 31      | Cartão de Crédito.                  |
| 32      | Boleto Proposta.                    |
| 33      | Boleto de Depósito e Aporte.        |
| 99      | Outros.                             |

##### **Response**

```
200 ok
content-type: application/json
```

Body

```json
{
  "account_id": "87ec3cb5-884e-492f-ae46-4e2c92a2e359",
  "amount": 5000000,
  "approval_expired_at": null,
  "approved_at": "2022-06-15T14:50:28Z",
  "approved_by": "user:9d213bde-d468-41ea-a502-348ddf7fa573",
  "barcode": "19792912500050000000000075096336954691269269",
  "barcode_details": {
    "bank_code": "197",
    "bank_name": "STONE IP S.A.",
    "barcode": "19792912500050000000000075096336954691269269",
    "expiration_date": "2022-10-01",
    "face_value": 5000000,
    "writable_line": "19790000057509633695546912692699291250005000000"
  },
  "cancelled_at": null,
  "cancelled_by": null,
  "created_at": "2022-06-15T14:50:28Z",
  "created_by": "user:9d213bde-d468-41ea-a502-348ddf7fa573",
  "details": {
    "value": null,
    "min_value": null,
    "max_value": null,
    "unpayable_reason_description": null,
    "unpayable_reason_details": null,
    "barcode": "19792912500050000000000075096336954691269269",
    "expiration_date": null,
    "total_added_value": null,
    "payment_limit_date": null,
    "payment_start_time": null,
    "bank_ispb": "16501555",
    "discounts": null,
    "payer_legal_name": null,
    "recipient_name": null,
    "settlement_date": null,
    "bank_code": "197",
    "fine_date": null,
    "interest_value": null,
    "number_of_partials": null,
    "payment_end_time": null,
    "accepts_partial_payment": null,
    "payer_cpf_cnpj": null,
    "unpayable_reason_code": null,
    "face_value": null,
    "document_payment_type": null,
    "bank_name": "STONE IP S.A.",
    "payer_trade_name": null,
    "interest_date": null,
    "document_type": "boleto",
    "divergent_amount_auth_type": null,
    "fine_value": null,
    "updatable_value": null,
    "recipient_cpf_cnpj": null,
    "status": "unpayable",
    "discount_value": null,
    "total_discounted_value": null,
    "writable_line": "19790000057509633695546912692699291250005000000"
  },
  "effective_payer": {
    "document": "289.851.350-40",
    "document_type": "cpf",
    "legal_name": "Caio Giovanni Ricardo Moraes"
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
  "request_id": "74bc3080-1f51-939d-8f7a-6fda572c8675",
  "scheduled_to": null,
  "status": "APPROVED",
  "writable_line": "19790000057509633695546912692699291250005000000"
}
```
