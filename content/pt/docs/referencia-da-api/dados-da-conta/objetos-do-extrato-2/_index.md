---
title: "old2_Objetos do Extrato"
slug: "objetos-do-extrato-2"
hidden: true
draft: true
date: "2019-09-17T13:31:27.645Z"
lastmod: "2020-10-05T12:37:55.705Z"
---
[block:callout]
{
  "type": "success",
  "title": "Objeto 'type'",
  "body": "O objeto 'type' é o identificador do tipo de operação realizada, assim ele será retornado no extrato com os seguintes valores para as operações:\n  * "internal": Transferência Stone ou Agendamento Transferência Stone\n  * "external": TED ou Agendamento TED\n  * "payment": Pagamento enviado, Agendamento de Pagamento ou Pagamento recebido\n  * "external_refund": Devolução de TED\n  * "payment_refund": Devolução de Pagamento\n  * "balance_blocked": Valor bloqueado\n  * "balance_unblocked": Valor desbloqueado\n  * "payroll": Pagamento de salário\n  * "salary": Recebimento de salário\n  * "salary_portability": Portabilidade de salário\n  * "salary_portability_refund": Devolução de Portabilidade de salário\n  * "salary_portability_employer_refund": Devolução de salário ou Devolução de salário para empresa\n  * "outbound_stone_prepaid_card_payment": Compra feita com Cartão Stone\n  * "outbound_stone_prepaid_card_payment_refund": Devolução de Compra, feita com Cartão Stone, através do estabelecimento original da compra.\n  * "outbound_stone_prepaid_card_payment_chargeback": Devolução de Compra, feita com o Cartão Stone, através da Conta Stone.\n  * "outbound_stone_prepaid_card_withdrawal": Saque com Cartão Stone feito no Banco24Horas.\n  * "outbound_stone_prepaid_card_withdrawal_refund": Devolução de Saque feito no  Banco24Horas."
}
[/block]
Cada tipo de operação retornará um extrato específico para o contexto da operação.

## **Contraparte** 
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"account\":{\n    \"institution\": string,\n    \"institution_name\": string,\n    \"account_code\": string,\n    \"branch_code\": string,\n    \"account_type\": string\n  },\n  \"entity\":{\n    \"name\": string,\n    \"document\": string,\n    \"document_type\": string\n  }\n}",
      "language": "json"
    }
  ]
}
[/block]
## **Movimentação** 
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"balance_before\": integer,\n  \"Balance_after\": integer,\n  \"id\": string,\n  \"amount\": integer,\n  \"created_at\": string,\n  \"status\": string\n}",
      "language": "json"
    }
  ]
}
[/block]
## **Pagamento com Cartão Recebido** 
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"balance_before\": integer,\n  \"balance_after\": integer,\n  \"id\": string,\n  \"created_at\": string,\n  \"amount\": integer,\n  \"card_network_code\": string,\n  \"card_network_name\": string,\n  \"card_type\": string,\n  \"is_prepayment\": boolean,\n  \"operation\": string,\n  \"status\": string,\n  \"type\": string\n}",
      "language": "json"
    }
  ]
}
[/block]
## **Pagamento com código de barras de outras instituições enviado** 
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"balance_before\": integer,\n  \"balance_after\": integer,\n  \"amount\": integer,\n  \"barcode\": string,\n  \"created_at\": string,\n  \"details\": {\n    \"bank_name\": string | null,\n    \"recipient_cpf_cnpj\": string | null,\n    \"recipient_name\": string | null,\n    \"writable_line\": string | null,\n    \"expiration_date\": string | null\n  },\n  \"fee_amount\": integer,\n  \"id\": string,\n  \"operation\":\"debit\",\n  \"operation_amount\": integer,\n  \"operation_id\": string\n}\n    ",
      "language": "json"
    }
  ]
}
[/block]
## **Pagamento com código de barras de outras instituições reembolsado** 
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"balance_before\": integer,\n  \"balance_after\": integer,\n  \"amount\": integer,\n  \"barcode\": string,\n  \"created_at\": string,\n  \"details\": {\n    \"bank_name\": string | null,\n    \"recipient_cpf_cnpj\": string | null,\n    \"recipient_name\": string | null,\n    \"writable_line\": string | null,\n    \"expiration_date\": string | null\n  },\n  \"fee_amount\": integer,\n  \"id\": string,\n  \"operation_amount\": integer,\n  \"original_operation_id\": string\n}",
      "language": "json"
    }
  ]
}
[/block]
## **Pagamento com código de barras recebido** 
[block:code]
{
  "codes": [
    {
      "code": "{\n      \"account_id\": \"c72ad932-e507-4d1f-a25c-a9bbb05500e6\",\n      \"amount\": 2000,\n      \"balance_after\": 2000,\n      \"balance_before\": 0,\n      \"barcode\": \"19791851500000020010000020200206193505504757\",\n      \"barcode_payment_invoice_id\": \"0a41b13d-b9b2-488c-944d-f48ef3a47aa3\",\n      \"beneficiary\": {\n        \"document\": \"12036082777\",\n        \"document_type\": \"cpf\",\n        \"legal_name\": \"Maria Fonseca Clemente Cruz\",\n        \"trade_name\": null\n      },\n      \"capture\": {\n        \"branch_code\": \"0001\",\n        \"institution_ispb\": \"16501555\",\n        \"institution_name\": \"Stone Pagamentos S.A.\",\n        \"medium\": \"3\"\n      },\n      \"created_at\": \"2020-02-07T21:42:54Z\",\n      \"expiration_date\": \"2021-01-29\",\n      \"fee_amount\": 200,\n      \"id\": \"ec951a20-997b-46b8-a476-4d481703a1d7\",\n      \"invoice_type\": \"proposal\",\n      \"issuance_date\": \"2020-02-06\",\n      \"limit_date\": \"2021-01-29\",\n      \"operation\": \"credit\",\n      \"operation_amount\": 2000,\n      \"payer\": {\n        \"document\": \"12036082777\",\n        \"document_type\": \"cpf\",\n        \"legal_name\": \"Maria Fonseca Clemente Cruz\",\n        \"trade_name\": null\n      },\n      \"status\": \"FINISHED\",\n      \"type\": \"payment\",\n      \"writable_line\": \"19790000052020020619935055047571185150000002001\"\n    }",
      "language": "json",
      "name": null
    }
  ]
}
[/block]

## **Saldo Desbloqueado** 
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"balance_before\": integer,\n  \"balance_after\": integer,\n  \"amount\": integer,\n  \"created_at\": string,\n  \"operation_amount\": integer,\n  \"operation\": string,\n  \"status\": string,\n  \"id\": string,\n  \"type\": string\n}",
      "language": "json"
    }
  ]
}
[/block]
## **Saldo Bloqueado** 
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"balance_before\": integer,\n  \"balance_after\": integer,\n  \"amount\": integer,\n  \"created_at\": string,\n  \"operation_amount\": integer,\n  \"operation\": string,\n  \"status\": string,\n  \"id\": string,\n  \"type\": string\n}",
      "language": "json"
    }
  ]
}
[/block]
## **Transferência interna enviada** 
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"balance_before\": integer,\n  \"balance_after\": integer,\n  \"amount\": integer,\n  \"fee_amount\": integer,\n  \"operation_amount\": integer,\n  \"created_at\": string,\n  \"id\": string,\n  \"operation_id\": string,\n  \"operation\": string,\n  \"description\": string | null,\n  \"type\": string,\n  \"counter_party\":{\n    \"account\":{\n      \"institution\": string,\n      \"institution_name\": string,\n      \"account_code\": string,\n      \"branch_code\": string,\n      \"account_type\": string\n    },\n    \"entity\":{\n      \"name\": string,\n      \"document\": string,\n      \"document_type\": string\n    }\n  },\n  \"status\": string\n}\n    ",
      "language": "json"
    }
  ]
}
[/block]
## **Transferência interna recebida** 
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"balance_before\": integer,\n  \"balance_after\": integer,\n  \"amount\": integer,\n  \"fee_amount\": integer,\n  \"operation_amount\": integer,\n  \"created_at\": string,\n  \"id\": string,\n  \"operation_id\": string,\n  \"operation\": string,\n  \"description\": string | null,\n  \"type\": string,\n  \"counter_party\":{\n    \"account\":{\n      \"institution\": string,\n      \"institution_name\": string,\n      \"account_code\": string,\n      \"branch_code\": string,\n      \"account_type\": string\n    },\n    \"entity\":{\n      \"name\": string,\n      \"document\": string,\n      \"document_type\": string\n    }\n  },\n  \"status\": string\n}",
      "language": "json"
    }
  ]
}
[/block]
## **Transferência externa enviada** 
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"balance_before\": integer,\n  \"balance_after\": integer,\n  \"amount\": integer,\n  \"fee_amount\": integer,\n  \"operation_amount\": integer,\n  \"created_at\": string,\n  \"id\": string,\n  \"operation_id\": string,\n  \"operation\": string,\n  \"type\": string,\n  \"refund_reason_code\": string,\n  \"refund_reasion_description\": string,\n  \"counter_party\": {\n    \"account\": {\n      \"institution\": string,\n      \"institution_name\": string,\n      \"account_code\": string,\n      \"branch_code\": string,\n      \"account_type\": string\n    },\n    \"entity\": {\n      \"name\": string,\n      \"document\": string,\n      \"documento_type\": string\n    }\n  },\n  \"status\": string,\n  \"delayed_to_next_business_day\": boolean\n}",
      "language": "json"
    }
  ]
}
[/block]
## **Transferência externa recebida** 
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"balance_before\": integer,\n  \"balance_after\": integer,\n  \"amount\": integer,\n  \"created_at\": string,\n  \"id\": string,\n  \"operation_id\": string,\n  \"operation\": string,\n  \"type\": string,\n  \"counter_party\": {\n    \"account\": {\n      \"institution\": string,\n      \"institution_name\": string,\n      \"account_code\": string,\n      \"branch_code\": string,\n      \"account_type\": string\n    },\n    \"entity\": {\n      \"name\": string,\n      \"document\": string,\n      \"documento_type\": string\n    }\n  },\n  \"status\": string\n}",
      "language": "json"
    }
  ]
}
[/block]
## **Transferência externa reembolsada** 
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"balance_before\": integer,\n  \"balance_after\": integer,\n  \"amount\": integer,\n  \"fee_amount\": integer,\n  \"operation_amount\": integer,\n  \"created_at\": string,\n  \"id\": string,\n  \"original_operation_id\": string,\n  \"operation\": string,\n  \"type\": string,\n  \"refund_reason_code\": string,\n  \"refund_reason_description\": string,\n  \"counter_party\": {\n    \"account\": {\n      \"institution\": string,\n      \"institution_name\": string,\n      \"account_code\": string,\n      \"branch_code\": string,\n      \"account_type\": string\n    },\n    \"entity\": {\n      \"name\": string,\n      \"document\": string,\n      \"document_type\": string\n    }\n  },\n  \"status\": string,\n  \"refunded_at\": string\n}",
      "language": "json"
    }
  ]
}
[/block]
