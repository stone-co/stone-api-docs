---
title: "Overview"
slug: "overview"
draft: false
date: "2021-08-26T12:18:04.117Z"
lastmod: "2021-08-26T12:18:04.117Z"
weight: 1
---

---

## O que é um Pagamento
<br>

### Conceito

<br>

Oferecemos uma API de Pagamentos, através da qual é possível efetuar o pagamento de contas com código de barras como, por exemplo, boletos, contas de luz, água, gás, IPTU, IPVA, entre outras.

Nossa API suporta pagamentos de todos os boletos CIP e um grande número de concessionárias/tributos. A janela de pagamentos de concessionárias pode variar de acordo com a empresa emissora. Pagamentos processados após o horário limite imposto pelo emissor serão acolhidos no dia útil seguinte.

<br>

{{< alert title="Horário de funcionamento" >}}
<br>

A API de Pagamentos fica disponível todos os dias das 00h00 até 23h50. Boletos pagos após 23h50 serão acolhidos no dia útil seguinte.		
{{< /alert >}}


<br>

### Estados
---

<br>

Segue abaixo os estados possíveis de um **pagamento**: 

<br>

![Imagem 1](/docs/referencia-da-api/pagamentos/o-que-e-um-pagamento/estados_pagamento.png)

<br>



### Falhas em Pagamentos

---

<br>

Falha é qualquer erro que ocorra entre a criação e a movimentação do dinheiro na conta. Ou seja, qualquer condição que era válida no momento da criação do pagamento, mas que mudou nas etapas seguintes.

A seguir listamos algumas das falhas possíveis para operações de pagamento.

<br>


| Código | Descrição                                                                  |
| ------ | -------------------------------------------------------------------------- |
| 0      | Ocorreu um erro durante o pagamento. Por favor, tente novamente.           |
| 1      | Saldo insuficiente.                                                        |
| 2      | Pagamento sem valor registrado não é suportado. Contate o emissor.         |
| 3      | Pagamento para titularidade diferente não suportado. Conclua seu cadastro. |
| 4      | Pagamento sem valor registrado não é suportado. Contate o emissor.         |


<br>



### Reembolsos em Pagamentos
---

<br>

Abaixo listamos algumas das razões possíveis para ocorrer reembolsos, como também seus códigos correspondentes.

<br>

| Código | Descrição                                                                  |
| ------ | -------------------------------------------------------------------------- |
| 40     | Código de moeda inválido.                                                  |
| 51     | Boleto de pagamento liquidado com valor maior ou menor do que o permitido. |
| 52     | Boleto vencido sem os juros/multa devidos.                                 |
| 53     | Código de barras não pertence ao banco emissor do boleto.                  |
| 63     | Código de barras inválido.                                                 |
| 68     | Boleto pago em duplicidade                                                 |
| 69     | Boleto pago em duplicidade.                                                |
| 70     | Por solicitação do cliente do banco recebedor do boleto.                   |
| 71     | Valor inválido.                                                            |
| 73     | Beneficiário não cadastrado no banco emissor.                              |
| 74     | Beneficiário com CPF/CNPJ divergente do cadastro no banco emissor.         |
| 75     | Pagador com CPF/CNPJ divergente do cadastro no banco emissor.              |
| 76     | Cópia não encaminhada pelo banco recebedor no prazo previsto.              |

<br>


## O Objeto Pagamento

Aqui listamos quais são os campos que usamos para realizar um pagamento.

| Chave                                                                                                                        | Descrição                                                                                                                                                                                                                                            | Tipo      |
| ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- |
| account_id                                                                                                                   | Identificador da conta.                                                                                                                                                                                                                              | _String_  |
| amount                                                                                                                       | Valor da transação, em centavos de reais.                                                                                                                                                                                                            | _Integer_ |
| approval_expired_at                                                                                                          | Horário em que a transação expirou, em formato ISO8601. Retorna `null` caso a transação estaja aguardando aprovação ou já tenha sido aprovada em algum momento.                                                                                        | _String_  |
| approved_at                                                                                                                  | Horário em que a transação foi aprovada, em formato ISO8601. Retorna `null` caso a transação não tenha sido aprovada em nenhum momento.                                                                                                                | _String_  |
| approved_by                                                                                                                  | Identificador único da usuária que aprovou a transação, no formato user:UUID4. Retorna `null` caso não tenha sido aprovada em nenhum momento.                                                                                                          | _String_  |
| barcode                                                                                                                      | Código de barras.                                                                                                                                                                                                                                    | _String_  |
| cancelled_at                                                                                                                 | Horário em que um pagamento agendado foi cancelado, em formato ISO8601. Retorna `null` caso não haja cancelamento.                                                                                                                                     | _String_  |
| created_at                                                                                                                   | Horário em que a transação foi criada, em formato ISO8601. Nesse caso nunca será `null`.                                                                                                                                                               | _String_  |
| created_by |  Identificador único da usuária que criou a transação, no formato user:UUID4. Neste caso nunca irá retornar `null`. | _String_                                                                                                                                                                                                                                             |
| details                                                                                                                      | Detalhes da transferência como nome da instituição, nome do destinatário, documento do beneficiário e nome do beneficiário. Retorna `null` caso ainda não tenhamos essa informação. Uma outra forma de obter essa informação é realizar uma simulação. | _Objeto_  |
| failed_at                                                                                                                    | Horário em que a transação falhou, em formato ISO8601. Retorna `null` caso a transação nunca tenha falhado.                                                                                                                                            | _String_  |
| failure_reason_code                                                                                                          | Código do motivo da falha.                                                                                                                                                                                                                           | _String_  |
| failure_reason_description                                                                                                   | Descrição do motivo da falha.                                                                                                                                                                                                                        | _String_  |
| fee | Taxa da transação, em centavos de reais.  |  Integer                                                                      |
| finished_at                                                                                                                  | Horário em que a transação foi finalizada, em formato ISO8601. Retorna `null` caso a transação não tenha sido finalizada.                                                                                                                              | _String_  |
| id                                                                                                                           | Identificador único da transação, no formato UUID4.                                                                                                                                                                                                  | _String_  |
| refunded_at                                                                                                                  | Horário em que a transação foi extornada em caso de falha, em formato ISO8601. Retorna `null` caso a transação não tenha sido extornada.                                                                                                               | _String_  |
| rejected_at                                                                                                                  | Horário em que a transação foi rejeitada, em formato ISO8601. Retorna `null` caso a transação não tenha sido rejeitada em nenhum momento.                                                                                                              | _String_  |
| rejected_by                                                                                                                  | Identificador único da usuária que rejeitou a transação, no formato user:UUID4. Retorna `null` caso não tenha sido rejeitada em nenhum momento.                                                                                                        | _String_  |
| scheduled_to                                                                                                                 | Data do agendamento. Caso não tenha sido agendado retornará `null`.                                                                                                                                                                                    | _String_  |
| status                                                                                                                       | Status atual do pagamento, podendo ser um dentre os status à seguir: CREATED, REJECTED, EXPIRED, APPROVED, SCHEDULED, FAILED, FINISHED, CANCELLED.                                                                                                   | _String_  |
| writable_line                                                                                                                | Código numérico que acompanha o código de barras.                                                                                                                                                                                                    | _String_  |

<br>

## Webhooks

Para visualizar as notificações enviadas a cada etapa de um pagamento de boleto, tributo ou concessionária, basta acessar [aqui]({{< relref "/docs/guias/webhooks/#pagamento-de-boleto">}})

<br>
