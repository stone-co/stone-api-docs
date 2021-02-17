---
title: "O Objeto Transferência"
slug: "objeto-transferência-interna"
draft: false
weight: 2
---

#### Transferência Interna

| Chave | Descrição | Tipo |
| ------ | ---------------------------------------------------------------------------------------- |---------|
| id | 
| amount | 
| fee | 
| target | 
| approved_at | 
| created_at | 
| rejected_at | 
| failed_at | 
| failure_reason_code |
| failure_reason_description |
| status | 
| description | 
| approved_by | 
| created_by | 
| rejected_by | 
| approval_expired_at | 
| cancelled_at | 
| cancelled_at | 

    "3-0": "target",
    "4-0": "approved_at",
    "5-0": "created_at",
    "6-0": "rejected_at",
    "7-0": "failed_at",
    "10-0": "status",
    "11-0": "description",
    "12-0": "approved_by",
    "13-0": "created_by",
    "14-0": "rejected_by",
    "14-1": "Identificador único da usuária que rejeitou a transação, no formato `user:UUID4`. Retorna `null` caso não tenha sido rejeitada em nenhum momento.",
    "13-1": "Identificador único da usuária que criou a transação, no formato `user:UUID4`. Neste caso nunca irá retornar null.",
    "12-1": "Identificador único da usuária que aprovou a transação, no formato `user:UUID4`. Retorna `null` caso não tenha sido aprovada em nenhum momento.",
    "11-1": "Descrição que foi adicionada durante a criação da transação. Retornará `\"\"` caso não tenha sido preenchido. Campo com tamanho máximo de 140 caracteres.",
    "10-1": "Status atual da transação, podendo ser um dentre os status à seguir: `CREATED`, `REJECTED`, `EXPIRED`, `APPROVED`, `SCHEDULED`, `FAILED`, `FINISHED`, `CANCELLED`.",
    "7-1": "Horário em que a transação falhou, em formato ISO8601. Retorna `null` caso a transação nunca tenha falhado.",
    "6-1": "Horário em que a transação foi rejeitada, em formato ISO8601. Retorna `null` caso a transação não tenha sido rejeitada em nenhum momento.",
    "5-1": "Horário em que a transação foi criada, em formato ISO8601. Nesse caso nunca será `null`.",
    "4-1": "Horário em que a transação foi aprovada, em formato ISO8601. Retorna `null` caso a transação não tenha sido aprovada em nenhum momento.",
    "3-1": "Objeto com os dados de conta destino.",
    "2-1": "Taxa da transação, em centavos de reais.",
    "1-1": "Valor da transação, em centavos de reais.",
    "0-1": "Identificador único da transação, no formato UUID4.",
    "h-0": "Chave",
    "h-1": "Descrição",
    "h-2": "Tipo",
    "0-2": "*String*",
    "3-2": "*[Object](https://docs.openbank.stone.com.br/reference#section-target)*",
    "4-2": "*String*",
    "5-2": "*String*",
    "6-2": "*String*",
    "7-2": "*String*",
    "10-2": "*String*",
    "11-2": "*String*",
    "12-2": "*String*",
    "13-2": "*String*",
    "14-2": "*String*",
    "1-2": "*Integer*",
    "2-2": "*Integer*",
    "15-0": "approval_expired_at",
    "16-0": "cancelled_at",
    "17-0": "created_by",
    "18-0": "finished_at",
    "19-0": "scheduled_to",
    "15-2": "*String*",
    "16-2": "*String*",
    "17-2": "*String*",
    "18-2": "*String*",
    "19-2": "*String*",
    "15-1": "Horário em que a transação expirou, em formato ISO8601. Retorna `null` caso a transação estaja aguardando aprovação ou já tenha sido aprovada em algum momento.",
    "16-1": "Horário em que um pagamento agendado foi cancelado, em formato ISO8601. Retorna `null` caso não haja cancelamento.",
    "17-1": "Identificador único da usuária que criou a transação, no formato `user:UUID4`. Neste caso nunca irá retornar null.",
    "18-1": "Horário em que a transação foi finalizada, em formato ISO8601. Retorna `null` caso a transação não tenha sido finalizada.",
    "19-1": "Data na qual a transferência será executada. Retornará `null` caso não haja agendamento.",
    "8-0": "failure_reason_code",
    "9-0": "failure_reason_description",
    "8-2": "*String*",
    "9-2": "*String*",
    "8-1": "Código do motivo da falha.",
    "9-1": "Descrição do motivo da falha."
  },
  "cols": 3,
  "rows": 20
}
[/block]

[block:api-header]
{
  "title": "Transferência Externa"
}
[/block]

[block:parameters]
{
  "data": {
    "h-0": "Chave",
    "h-1": "Descrição",
    "h-2": "Tipo",
    "0-0": "id",
    "0-1": "Identificador único da transação, no formato UUID4.",
    "0-2": "*String*",
    "1-0": "amount",
    "1-1": "Valor da transação, em centavos de Reais.",
    "1-2": "*Integer*",
    "2-0": "fee",
    "2-1": "Taxa da transação, em centavos de Reais.",
    "2-2": "*Integer*",
    "3-0": "target",
    "3-1": "Objeto com os dados de conta destino.",
    "3-2": "*[Object](https://docs.openbank.stone.com.br/reference#section-target)*",
    "4-0": "created_at",
    "4-1": "Horário em que a transação foi criada, em formato ISO8601. Nesse caso nunca será `null`.",
    "4-2": "*String*",
    "5-1": "Horário em que a transação foi aprovada, em formato ISO8601. Retorna `null` caso a transação não tenha sido aprovada em nenhum momento.",
    "5-0": "approved_at",
    "5-2": "*String*",
    "6-1": "Horário em que a transação foi rejeitada, em formato ISO8601. Retorna `null` caso a transação não tenha sido rejeitada em nenhum momento.",
    "6-0": "rejected_at",
    "6-2": "*String*",
    "12-0": "created_by",
    "12-1": "Identificador único da usuária que criou a transação, no formato `user:UUID4`. Neste caso nunca irá retornar null.",
    "12-2": "*String*",
    "13-0": "approved_by",
    "13-1": "Identificador único da usuária que aprovou a transação, no formato  `user:UUID4`. Retorna `null` caso não tenha sido aprovada em nenhum momento.",
    "14-0": "rejected_by",
    "14-1": "Identificador único da usuária que rejeitou a transação, no formato `user:UUID4`. Retorna `null` caso não tenha sido rejeitada em nenhum momento.",
    "7-0": "failed_at",
    "7-1": "Horário em que a transação falhou, em formato ISO8601. Retorna `null` caso a transação nunca tenha falhado.",
    "7-2": "*String*",
    "10-0": "refunded_at",
    "10-2": "*String*",
    "10-1": "Horário em que a transação foi extornada em caso de falha, em formato ISO8601. Retorna `null` caso a transação não tenha sido extornada.",
    "13-2": "*String*",
    "14-2": "*String*",
    "11-0": "status",
    "11-1": "Status atual da transação, podendo ser um dentre os status à seguir: `CREATED`, `REJECTED`, `EXPIRED`, `APPROVED`, `SCHEDULED`, `FAILED`, `FINISHED`,  , `CANCELLED`, `REFUNDED`, `DELAYED_TO_NEXT_BUSINESS_DAY`.",
    "11-2": "*String*",
    "16-0": "approval_expired_at",
    "17-0": "cancelled_at",
    "15-0": "delayed_to_next_business_day",
    "15-1": "Caso a transação seja feita fora do horário, será agendada para o póximo dia útil. Caso esse agendamento ocorra, retorna `true`, caso contrário, retorna `false`.",
    "15-2": "*Boolean*",
    "18-0": "finished_at",
    "19-0": "refund_reason_code",
    "20-0": "refund_reason_description",
    "21-0": "scheduled_to_effective",
    "22-0": "scheduled_to_requested",
    "16-1": "Horário em que a transação expirou, em formato ISO8601. Retorna `null` caso a transação estaja aguardando aprovação ou já tenha sido aprovada em algum momento.",
    "17-1": "Horário em que um pagamento agendado foi cancelado, em formato ISO8601. Retorna `null` caso não haja cancelamento.",
    "18-1": "Horário em que a transação foi finalizada, em formato ISO8601. Retorna `null` caso a transação não tenha sido finalizada.",
    "18-2": "*String*",
    "16-2": "*String*",
    "17-2": "*String*",
    "19-2": "*String*",
    "20-2": "*String*",
    "21-2": "*String*",
    "22-2": "*String*",
    "19-1": "Código do reembolso. Retorna `null` caso não haja reembolso.",
    "20-1": "Descrição do motivo do reembolso. Retorna `null` caso não haja reembolso.",
    "21-1": "Data na qual a TED será executada. Pode divergir da solicitada quando esta for um dia não útil. Retornará `null` caso não haja agendamento.",
    "22-1": "Data para a qual o agendamento da TED foi solicitado. Retornará `null` caso não haja agendamento.",
    "8-0": "failure_reason_code",
    "8-1": "Código do motivo da falha.",
    "9-1": "Descrição do motivo da falha.",
    "9-0": "failure_reason_description",
    "8-2": "*String*",
    "9-2": "*String*"
  },
  "cols": 3,
  "rows": 23
}
[/block]

[block:api-header]
{
  "title": "Target"
}
[/block]

[block:parameters]
{
  "data": {
    "h-0": "Chave",
    "h-1": "Descrição",
    "h-2": "Tipo",
    "0-0": "account",
    "0-1": "Objeto que representa a conta destino da transferência.",
    "0-2": "[*Object*](https://docs.openbank.stone.com.br/reference#account)",
    "1-0": "entity",
    "1-1": "O indivíduo ou companhia responsável pela conta.",
    "1-2": "[*Object*](https://docs.openbank.stone.com.br/reference#entity)"
  },
  "cols": 3,
  "rows": 2
}
[/block]

[block:api-header]
{
  "title": "Account"
}
[/block]

[block:parameters]
{
  "data": {
    "h-0": "Chave",
    "h-1": "Descrição",
    "h-2": "Tipo",
    "0-0": "account_code",
    "0-1": "Número da conta bancária.",
    "0-2": "*String*",
    "1-0": "branch_code",
    "1-1": "Número da agência da conta. **Apenas para transferência externa.** ",
    "1-2": "*String*",
    "2-0": "institution_ispb",
    "2-1": "Código ISPB da instituição responsável pela conta. Existe uma lista completa relacionando as instituições e seus respectivos códigos neste [link](https://www.bcb.gov.br/pom/spb/estatistica/port/ASTR003.pdf). **Apenas para transferência externa.**",
    "2-2": "*String*",
    "3-0": "institution_name",
    "3-1": "Nome da instituição responsável pela conta. **Apenas para transferência externa.**",
    "3-2": "*String*",
    "4-0": "institution_number_code",
    "4-2": "*String*",
    "4-1": "Código numérico da instituição responsável pela conta. **Apenas para transferência externa.**",
    "5-0": "account_type",
    "5-1": "Código que identifica o tipo de conta. Os valores possíveis são:\n`CC` - Conta Corrente, `CD` - Conta de Depósito, `CG` - Conta garantida, `CI` - Conta de Investimento, `PG` - Conta de Pagamento, `PP` - Poupança.\n**Apenas para transferência externa.**",
    "5-2": "*String*"
  },
  "cols": 3,
  "rows": 6
}
[/block]

[block:api-header]
{
  "title": "Entity"
}
[/block]

[block:parameters]
{
  "data": {
    "0-0": "name",
    "0-1": "Nome da proprietária da conta.",
    "0-2": "*String*",
    "h-0": "Chave",
    "h-1": "Descrição",
    "h-2": "Tipo",
    "1-0": "document",
    "1-1": "Número do documento sem pontos da dona da conta alvo. **Apenas para transferência externa.**",
    "1-2": "*String*",
    "2-0": "document_type",
    "2-2": "*String*",
    "2-1": "Tipo do documento da dona da conta alvo. Pode ser `cpf` ou `cnpj`. Utilizamos esse valor para distinguir o tipo de entidade da proprietária da conta entre pessoa física e pessoa jurídica. **Apenas para transferência externa.**"
  },
  "cols": 3,
  "rows": 3
}
[/block]

[block:callout]
{
  "type": "info",
  "body": "A criação de transferências internas e externas estão sujeitas a um limite de `\"amount\": 999999999999999999`.\nObserve que usuária não é limitada de nenhuma forma prática por esse valor."
}
[/block]