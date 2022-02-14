---
title: "Relato de Infração recebido"
linkTitle: "Relato de infração recebido"
date: 2022-02-11T14:00:00-03:00
lastmod: 2022-02-11T14:00:00-03:00
weight: 3
draft: false
description: >
  Veja como listar e fechar relatos de infrações recebidos
---

## O que é um Relato de Infração
---
Relatos de infração servem para reportar transações sob suspeita de fraude. Podem ser feitas tanto pelo participante debitado quanto pelo creditado na transação.
<br><br>
Os relatos tem dois motivos(InfractionType), que é de preenchimento obrigatório, são eles, fraude(fraud) e associada a uma solicitação de devolução(refund_request). Depois de criado, o relato deve ser reconhecido pela outra parte da transação (acknowledge) e, após análise, fechado (close) concordando (AGREED) ou discordando (DISAGREED) da infração.
<br><br>
O criador do relato pode cancelá-lo a qualquer momento, mesmo depois de fechado.
<br><br>
Relatos de infração são criados a partir do identificador da transação realizada no SPI (EndToEndId). O prazo máximo para relatar infração em uma transação é de 80 dias após a data da transação questionada. A resolução do relato com desfecho de concordando (AGREED) ou discordando (DISAGREED) da infração deve ser no prazo máximo de 7 dias corridos da data de sua abertura.
<br><br>
Cada participante deve realizar polling periódico na lista de relatos para verificar se existem novos relatos em que é parte. O recebimento do relato não implica em concordância. 
<br><br>
Os níveis de serviço exigidos para as operações com relatos de infração estão definidos no Manual de Tempos do Pix. Os relatos por motivo de fraude são contabilizados e retornados ao consultar vínculo. 
<br><br>
Se for cancelado, o relato deixa de ser contabilizado em REPORTED_FRAUDS durante a consulta de vínculos.

{{% pageinfo %}}
**Atenção!**<br>As interações descritas aqui irão servir apenas para participantes indiretos. <br>
{{% /pageinfo %}}
<br>


## Campos do relato de infração
---

<br>

| Campo                        | Tipo  | Descrição                                                              | Regra de negócio        |
| ---------------------------- | -------------- | -------------------------------------------------------- | ------------------------------ |

| end_to_end_id | String | Identificador ponta a ponta do pagamento que está sendo relatado uma infração. | Ou end_to_end_id ou refund_id deve estar preenchido. |

| refund_id | String | Identificador ponta a ponta da devolução que está sendo relatado uma infração. | Ou end_to_end_id ou refund_id deve estar preenchido. |

| infraction_id | String | Identificador do relato de infração. | Obrigatório. |

| account_id | String | Identificador da Conta Stone associada ao pagamento/devolução. | Obrigatório. |

| request_id | String | Identificador da requisição de criação de relato de infração. | Obrigatório. |

| direction | Enum | Indica se o relato foi enviado ou recebido.| Obrigatório. Possíveis valores são: `inbound`, `outbound`. |

| type | Enum | Indica o tipo de relato de infração. | Obrigatório. Possíveis valores são: `fraud`, `request_refund`, `refund_cancelled`. |

| report_details | String | Detalhes do relato de infração. | Opcional. Pode ter até 2000 caracteres |

| reported_by | Enum | Indica por quem for reportado. | Obrigatório. Possíveis valores são: `debited_participant`, `credited_participant`. |

| status | Enum | Situação do relato de infração. | Obrigatório. Possíveis valores são: `pending`, `accepted`, `rejected`, `cancelled`. |

| debited_participant | String | ISPB do participante debitado no pagamento/transação.  | Obrigatório. |

| credited_participant | String | ISPB do participante creditado no pagamento/transação. | Obrigatório. |

| created_at | Datetime | Data de quando o relato foi criado | Obrigatório. |

| expires_at | Datetime | Data limite que o relato de infração pode ser fechado. | Obrigatório. |

| analysis_result | Enum | Resultado da análise do relato de infração. | Opcional. Possíveis valores são: `accepted`, `rejected`. |

| analysis_details | String | Detalhes da análise do relato de infração. | Opcional. |

| accepted_at | Datetime | Data de quando o relato de infração foi aceito. | Opcional. |

| rejected_at | Datetime | Data de quando o relato de infração foi rejeitado. | Opcional. |

| cancelled_at | Datetime | Data de quando o relato de infração foi cancelado. | Opcional. |

| transaction_type | Enum | Se o pagamento/devolução associado ao relato de infração foi interna ou externa (SPI) | Opcional. Possíveis valores são: `spi`, `internal`. |

| transaction_result | Enum | Se o pagamento/devolução associado ao relato de infração foi liquidada ou rejeitada por uma das partes | Opcional. Possíveis valores são: `settled`, `rejected_payee`, `rejected_payer`. |


##### Status dos Relatos de Infrações

- `pending`: aguardando fechamento.
- `accepted`: relato de infração aceito.
- `rejected`: relato de infração rejeitado.
- `cancelled`: relato de infração cancelado.

<br>  

Para detalhes técnicos dos relatos de infrações, clique em um dos links abaixo: