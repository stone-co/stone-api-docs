---
title: "old_Objetos do extrato"
slug: "objetos-do-extrato-1"
hidden: true
draft: true
date: "2020-03-09T22:16:07.755Z"
lastmod: "2020-08-13T18:33:56.204Z"
---
[block:api-header]
{
  "title": "Pagamento de boleto bancário recebido"
}
[/block]

[block:parameters]
{
  "data": {
    "0-0": "account_id",
    "h-0": "Chave",
    "h-1": "Descrição",
    "h-2": "Tipo",
    "0-2": "*String*",
    "1-0": "amount",
    "2-0": "balance_after",
    "3-0": "balance_before\"",
    "2-2": "*Integer*",
    "3-2": "*Integer*",
    "1-2": "*String*",
    "4-2": "*String*",
    "4-0": "barcode",
    "5-0": "barcode_payment_invoice_id",
    "5-2": "*String*",
    "6-0": "beneficiary",
    "7-0": "capture",
    "6-2": "*Object*",
    "7-2": "*Object*",
    "8-0": "created_at",
    "8-2": "*String*",
    "9-0": "expiration_date",
    "9-2": "*String*",
    "10-0": "fee_amount",
    "10-2": "*Integer*",
    "11-0": "id",
    "11-2": "*String*",
    "12-0": "invoice_type",
    "13-0": "issuance_date",
    "14-0": "limit_date",
    "12-2": "*String*",
    "13-2": "*String*",
    "14-2": "*String*",
    "15-0": "operation",
    "16-0": "operation_amount",
    "15-2": "*String*",
    "16-2": "*String*",
    "17-0": "payer",
    "17-2": "*Object*",
    "18-0": "status",
    "19-0": "type",
    "20-0": "writable_line",
    "18-2": "*String*",
    "19-2": "*String*",
    "20-2": "*String*",
    "0-1": "Identificador da conta do beneficiário.",
    "1-1": "?????",
    "2-1": "Saldo da conta após a entrada desde evento.",
    "3-1": "Saldo da conta antes da entrada deste evento.",
    "4-1": "Código de barras.",
    "5-1": "Identificador único do boleto bancário emitido, no formato UUID4.",
    "8-1": "Horário em que o boleto bancário foi gerado. Nesse caso nunca será `null`. Formato ISO8601 \"YYYY-MM-DDThh:mm:ssZ.",
    "9-1": "Data de vencimento do boleto bancário. Mesmo depois dessa data expirar o pagamento ainda pode ser feito. Formato ISO8601 \"YYYY-MM-DDThh:mm:ssZ.",
    "10-1": "Taxa cobrada pela operação.",
    "11-1": "Identificador único do pagamento do boleto bancário, no formato UUID4.",
    "12-1": "Tipo de boleto bancário. Valor suportado `proposal`.",
    "13-1": "Data da emissão de boleto bancário. Formato ISO8601 \"YYYY-MM-DDThh:mm:ssZ.",
    "14-1": "?????",
    "18-1": "Status atual do boleto bancário, podendo ser um dentre os status à seguir: `CREATED`, `REGISTRATED` ou `SETTLED`.",
    "20-1": "Código numérico que acompanha o código de barras.",
    "6-1": "Objeto com os dados do beneficiário.",
    "7-1": "Objeto com os detalhes da captura do pagamento.",
    "15-1": "?????",
    "16-1": "?????",
    "17-1": "Objeto com os dados do pagador."
  },
  "cols": 3,
  "rows": 21
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "{\n      \"account_id\": \"c72ad932-e507-4d1f-a25c-a9bbb05500e6\",\n      \"amount\": 2001,\n      \"balance_after\": 31233216130,\n      \"balance_before\": 31233214129,\n      \"barcode\": \"19791851500000020010000020200206193505504757\",\n      \"barcode_payment_invoice_id\": \"0a41b13d-b9b2-488c-944d-f48ef3a47aa3\",\n      \"beneficiary\": {\n        \"document\": \"12036082769\",\n        \"document_type\": \"cpf\",\n        \"legal_name\": \"Gabriel Silva de Lima Rocha\",\n        \"trade_name\": null\n      },\n      \"capture\": {\n        \"branch_code\": \"0001\",\n        \"institution_ispb\": \"16501555\",\n        \"institution_name\": \"Stone Pagamentos S.A.\",\n        \"medium\": \"3\"\n      },\n      \"created_at\": \"2020-02-07T21:42:54Z\",\n      \"expiration_date\": \"2021-01-29\",\n      \"fee_amount\": 0,\n      \"id\": \"ec951a20-997b-46b8-a476-4d481703a1d7\",\n      \"invoice_type\": \"proposal\",\n      \"issuance_date\": \"2020-02-06\",\n      \"limit_date\": \"2021-01-29\",\n      \"operation\": \"credit\",\n      \"operation_amount\": 2001,\n      \"payer\": {\n        \"document\": \"12036082769\",\n        \"document_type\": \"cpf\",\n        \"legal_name\": \"Gabriel Silva de Lima Rocha\",\n        \"trade_name\": null\n      },\n      \"status\": \"FINISHED\",\n      \"type\": \"payment\",\n      \"writable_line\": \"19790000052020020619935055047571185150000002001\"\n    }",
      "language": "json"
    }
  ],
  "sidebar": true
}
[/block]
##**Beneficiary**
[block:parameters]
{
  "data": {
    "0-0": "document",
    "1-0": "document_type",
    "2-0": "legal_name",
    "3-0": "trade_name",
    "h-0": "Chave",
    "h-1": "Descrição",
    "h-2": "Tipo",
    "1-1": "Tipo do documento do beneficiário. Pode ser 'cpf' ou 'cnpj'.",
    "1-2": "*String*",
    "0-1": "Número do documento do beneficiário sem pontos.",
    "0-2": "*String*",
    "2-1": "É o nome que identifica o beneficiário para fins legais, administrativos e outros fins oficiais.",
    "3-1": "Nome fantasia do beneficiário.",
    "2-2": "*String*",
    "3-2": "*String*"
  },
  "cols": 3,
  "rows": 4
}
[/block]
##**Capture**
[block:parameters]
{
  "data": {
    "h-0": "Chave",
    "h-1": "Descrição",
    "h-2": "Tipo",
    "0-0": "branch_code",
    "1-0": "institution_ispb",
    "2-0": "institution_name",
    "3-0": "medium",
    "1-2": "*String*",
    "2-2": "*String*",
    "3-2": "*String*",
    "0-2": "*String*",
    "0-1": "Número da agência da conta.",
    "1-1": "Código ISPB da instituição responsável pela conta. Existe uma lista completa relacionando as instituições e seus respectivos códigos neste [link](https://www.bcb.gov.br/pom/spb/estatistica/port/ASTR003.pdf).",
    "2-1": "Nome da instituição responsável pela conta.",
    "3-1": "Meio de pagamento do boleto. Valores possíveis: `cash`, `debit`, `credit` e `check`."
  },
  "cols": 3,
  "rows": 4
}
[/block]
## **Payer** 
[block:parameters]
{
  "data": {
    "h-0": "Chave",
    "h-1": "Descrição",
    "h-2": "Tipo",
    "0-0": "document",
    "1-0": "document_type",
    "2-0": "payer.legal_name",
    "3-0": "payer.trade_name",
    "0-1": "Número do documento do pagador sem pontos.",
    "1-1": "CPF ou CPNJ do pagador.",
    "2-1": "É o nome que identifica o pagador para fins legais, administrativos e outros fins oficiais.",
    "3-1": "Nome fantasia do pagador.",
    "0-2": "*String*",
    "1-2": "*String*",
    "2-2": "*String*",
    "3-2": "*String*"
  },
  "cols": 3,
  "rows": 4
}
[/block]
