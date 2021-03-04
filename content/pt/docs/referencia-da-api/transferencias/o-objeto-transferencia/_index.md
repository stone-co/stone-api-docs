---
title: "O Objeto Transferência"
slug: "objeto-transferência"
draft: false
weight: 2
---
Abaixo vamos trazer os campos de cada tipo de transferência.

---

#### Transferência Interna

| Chave                      | Descrição                                                                                                                                                          | Tipo      |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------- |
| id                         | Identificador único da transação, no formato UUID4.                                                                                                                | _String_  |
| amount                     | Valor da transação, em centavos de Reais.                                                                                                                          | _Integer_ |
| fee                        | Taxa da transação, em centavos de Reais.                                                                                                                           | _Integer_ |
| target                     | Objeto com os dados de conta destino. Veja [abaixo](/docs/referencia-de-api/transferencias/2-o-objeto-transferencia/#campos-do-objeto-target) seus campos.         | _Object_  |
| created_at                 | Horário em que a transação foi criada, em formato ISO8601. Nesse caso nunca será `null`.                                                                           | _String_  |
| approved_at                | Horário em que a transação foi aprovada, em formato ISO8601. Retorna `null` caso a transação não tenha sido aprovada em nenhum momento.                            | _String_  |
| rejected_at                | Horário em que a transação foi rejeitada, em formato ISO8601. Retorna `null` caso a transação não tenha sido rejeitada em nenhum momento.                          | _String_  |
| failed_at                  | Horário em que a transação falhou, em formato ISO8601. Retorna `null` caso a transação nunca tenha falhado.                                                        | _String_  |
| failure_reason_code        | Código do motivo da falha.                                                                                                                                         | _String_  |
| failure_reason_description | Descrição do motivo da falha.                                                                                                                                      | _String_  |
| status                     | Status atual da transação, podendo ser um dentre os status à seguir: `CREATED`, `REJECTED`, `EXPIRED`, `APPROVED`, `SCHEDULED`, `FAILED`, `FINISHED`, `CANCELLED`. | _String_  |
| description                | Descrição que foi adicionada durante a criação da transação. Retornará "" caso não tenha sido preenchido. Campo com tamanho máximo de 140 caracteres.              | _String_  |
| approved_by                | Identificador único do usuário que aprovou a transação, no formato `user:UUID4`. Retorna `null` caso não tenha sido aprovada em nenhum momento.                    | _String_  |
| created_by                 | Identificador único do usuário que criou a transação, no formato `user:UUID4`. Neste caso nunca irá retornar `null`.                                               | _String_  |
| rejected_by                | Identificador único do usuário que rejeitou a transação, no formato `user:UUID4`. Retorna `null` caso não tenha sido rejeitada em nenhum momento.                  | _String_  |
| approval_expired_at        | Horário em que a transação expirou, em formato ISO8601. Retorna `null` caso a transação esteja aguardando aprovação ou já tenha sido aprovada em algum momento.    | _String_  |
| cancelled_at               | Horário em que um pagamento agendado foi cancelado, em formato ISO8601. Retorna `null` caso não haja cancelamento.                                                 | _String_  |
| finished_at                | Horário em que a transação foi finalizada, em formato ISO8601. Retorna `null` caso a transação não tenha sido finalizada.                                          | _String_  |
| scheduled_to               | Data na qual a transferência será executada. Retornará `null` caso não haja agendamento.                                                                           | _String_  |

<br>   
    
#### Transferência Externa

| Chave                        | Descrição                                                                                                                                                                      | Tipo      |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------- |
| id                           | Identificador único da transação, no formato UUID4.                                                                                                                            | _String_  |
| amount                       | Valor da transação, em centavos de Reais.                                                                                                                                      | _Integer_ |
| fee                          | Taxa da transação, em centavos de Reais.                                                                                                                                       | _Integer_ |
| target                       | Objeto com os dados de conta destino. Veja abaixo seus campos. Veja seus campos [aqui](/docs/referencia-de-api/transferencias/o-objeto-transferencia/#campos-do-objeto-target) | _Object_  |
| created_at                   | Horário em que a transação foi criada, em formato ISO8601. Nesse caso nunca será `null`.                                                                                       | _String_  |
| approved_at                  | Horário em que a transação foi aprovada, em formato ISO8601. Retorna `null` caso a transação não tenha sido aprovada em nenhum momento.                                        | _String_  |
| rejected_at                  | Horário em que a transação foi rejeitada, em formato ISO8601. Retorna `null` caso a transação não tenha sido rejeitada em nenhum momento.                                      | _String_  |
| failed_at                    | Horário em que a transação falhou, em formato ISO8601. Retorna `null` caso a transação nunca tenha falhado.                                                                    | _String_  |
| failure_reason_code          | Código do motivo da falha.                                                                                                                                                     | _String_  |
| failure_reason_description   | Descrição do motivo da falha.                                                                                                                                                  | _String_  |
| status                       | Status atual da transação, podendo ser um dentre os status à seguir: `CREATED`, `REJECTED`, `EXPIRED`, `APPROVED`, `SCHEDULED`, `FAILED`, `FINISHED`, `CANCELLED`.             | _String_  |
| approved_by                  | Identificador único do usuário que aprovou a transação, no formato `user:UUID4`. Retorna `null` caso não tenha sido aprovada em nenhum momento.                                | _String_  |
| created_by                   | Identificador único do usuário que criou a transação, no formato `user:UUID4`. Neste caso nunca irá retornar `null`.                                                           | _String_  |
| rejected_by                  | Identificador único do usuário que rejeitou a transação, no formato `user:UUID4`. Retorna `null` caso não tenha sido rejeitada em nenhum momento.                              | _String_  |
| approval_expired_at          | Horário em que a transação expirou, em formato ISO8601. Retorna `null` caso a transação esteja aguardando aprovação ou já tenha sido aprovada em algum momento.                | _String_  |
| cancelled_at                 | Horário em que um pagamento agendado foi cancelado, em formato ISO8601. Retorna `null` caso não haja cancelamento.                                                             | _String_  |
| finished_at                  | Horário em que a transação foi finalizada, em formato ISO8601. Retorna `null` caso a transação não tenha sido finalizada.                                                      | _String_  |
| delayed_to_next_business_day | Caso a transação seja feita fora do horário, será agendada para o póximo dia útil. Caso esse agendamento ocorra, retorna `true`, caso contrário, retorna `false`.              | _Boolean_ |
| refund_reason_code           | Código do reembolso. Retorna `null` caso não haja reembolso.                                                                                                                   | _String_  |
| refund_reason_description    | Descrição do motivo do reembolso. Retorna `null` caso não haja reembolso.                                                                                                      | _String_  |
| scheduled_to_effective       | Data na qual a TED será executada. Pode divergir da data solicitada quando esta for um dia não útil. Retornará `null` caso não haja agendamento.                               | _String_  |
| scheduled_to_requested       | Data para a qual o agendamento da TED foi solicitado. Retornará null caso não haja agendamento.                                                                                | _String_  |


<br>


##### Campos do objeto **target**

| Chave   | Descrição                                                                                                                                                                                                    | Tipo     |
| ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------- |
| account | Objeto que representa a conta destino da transferência. Veja os campos desse objeto [abaixo](/docs/referencia-de-api/transferencias/o-objeto-transferencia/#campos-do-objeto-account).                       | _Object_ |
| entity  | Objeto que contem os dados do indivíduo ou companhia responsável pela conta. Veja os campos desse objeto [abaixo](/docs/referencia-de-api/transferencias/2-o-objeto-transferencia/#campos-do-objeto-entity). | _Object_ |


<br>

##### Campos do objeto **account**

| Chave                   | Descrição                                                                                                                                                                                                                                                      | Tipo     |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| account_code            | Número da conta bancária.                                                                                                                                                                                                                                      | _String_ |
| branch_code             | NNúmero da agência da conta. **Apenas para transferência externa**.                                                                                                                                                                                            | _String_ |
| institution_ispb        | Código ISPB da instituição responsável pela conta. Existe uma lista completa relacionando as instituições e seus respectivos códigos neste [link](https://www.bcb.gov.br/pom/spb/estatistica/port/ASTR003.pdf). **Apenas para transferência externa**.         | _String_ |
| institution_name        | Nome da instituição responsável pela conta. **Apenas para transferência externa**.                                                                                                                                                                             | _String_ |
| institution_number_code | Código numérico da instituição responsável pela conta.**Apenas para transferência externa**.                                                                                                                                                                   | _String_ |
| account_type            | Código que identifica o tipo de conta. Os valores possíveis são:<br> `CC` - Conta Corrente, `CD` - Conta de Depósito, `CG` - Conta garantida, `CI` - Conta de Investimento, `PG` - Conta de Pagamento, `PP` - Poupança. **Apenas para transferência externa**. | _String_ |

<br>

##### Campos do objeto **entity**

| Chave         | Descrição                                                                                                                                                                                                                          | Tipo     |
| ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| name          | Nome do proprietário da conta.                                                                                                                                                                                                     | _String_ |
| document      | Número do documento sem pontos da dona da conta alvo. **Apenas para transferência externa**.                                                                                                                                       | _String_ |
| document_type | Tipo do documento da dona da conta alvo. Pode ser `cpf` ou `cnpj`. Utilizamos esse valor para distinguir o tipo de entidade da proprietária da conta entre pessoa física e pessoa jurídica. **Apenas para transferência externa**. | _String_ |


{{% pageinfo %}}
A criação de transferências internas e externas estão sujeitas a um limite de `"amount": 999999999999999999`.
<br>Observe que o usuário não é limitado de nenhuma forma prática por esse valor.
{{% /pageinfo %}}
