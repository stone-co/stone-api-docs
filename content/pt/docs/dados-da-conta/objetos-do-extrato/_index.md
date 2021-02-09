---
title: "Objetos do Extrato"
slug: "objetos-do-extrato"
hidden: false
createdAt: "2020-08-13T18:33:18.658Z"
updatedAt: "2020-10-28T19:48:19.261Z"
weight: 7
---

---
O extrato mostra todos os tipos de transações que ocorreram em determinada conta de pagamento. 

Cada transação é uma nova entrada no extrato e elas estão listadas abaixo com seus campos.

Para ver a estrutura de cada transação, basta dar uma olhadinha aqui do lado ->


### Tipos de Transação

Veja os possíveis valores para o campo `type`, sua descrição e as possíveis combinações com o campo `operation`.

<br>

| Valores type                                   |    Descrição               | Valores Possiveis (Operation)      |
| ---------------------------------------------- | -------------------------  | -----------------------------------|
| balance_blocked                                | Bloqueio de Saldo.         | `credit` ou `debit`  |
| balance_unblocked                              | Desbloqueio de Saldo.      | `credit`
| card_payment                                   | Liquidação de recebíveis de cartão recebido.  | `credit`
| external                                       | Transferência externa. (TED)| `credit` ou `debit`
| external refund                                | Devolução de Transferência externa. | `credit`
| instant_payment                                | Transação de Instant Payment / Qr Code. | `credit` ou `debit` 
| internal                                       | Transferencia interna. | `credit` ou `debit` 
| loan_payments                                  | Valor referente a um empréstimo/crédito | `credit` ou `debit` 
| outbound_stone_prepaid_card_payment            | Compra feita com Cartão Stone. | `debit`
| outbound_stone_prepaid_card_payment_refund     | Devolução de compra com Cartão Stone. | `credit`
| outbound_stone_prepaid_card_payment_chargeback | Devolução do dinheiro a usuária devido ao pedido de chagerback de uma compra feita com cartão Stone.   | `credit`
| outbound_stone_prepaid_card_withdrawal         | Saque com Cartão Stone feito no Banco24Horas. | `debit`
| outbound_stone_prepaid_card_withdrawal_refund  | Devolução de Saque feito no Banco24Horas. | `credit`
| payment                                        | Pagamento de documento com código de barras. | `credit` ou `debit`
| payment refund                                 | Devolução do pagamento de documento com código de barras. | `credit`
| payroll                                        | Folha de pagamento.  | `debit`
| sallary                                        | Recebimento de salário.  | `credit`
| salary_portability                             | Envio do salário para a outra instituição onde foi solicitada a portabilidade. | `debit`
| salary_portability_refund                      | Devolução de salário pela instituição cadastrada na portabilidade. | `credit`
| salary_portability_employer_refund             | Devolução de salário do empregado para a instituição cadastrada na portabilidade. (No caso de processamento do cancelamento da portabilidade, o empregado poderá receber nas duas instituições) | `debit`

---

### Campos das Transações

Todas as entradas do extrato tem alguns campos padrões são eles:

<br>

| Chave                                   |    Descrição               | Tipo    |
| ---------------------------------------------- | -------------------------  | -----------------------------------|
| type                                | Identifica o tipo de movimentação do extrato. Veja os possíveis valores desse campo na tabela acima.         | `String` 
| operation                              | Identifica se a movimentação foi de entrada de dinheiro, credit, ou de saída de dinheiro debit. Veja as combinações possíveis de tipos e operações na tabela acima.      | `String`
| balance_before                                   | Saldo antes da operação ocorrer.  | `Integer`
| balance_after                                       | Saldo disponível após o valor da operação, incluindo taxas. | `Integer`
| amount                               | Valor da operação sem taxas.  | `Integer`
| account_id                                | ID da conta pagamento a qual essa entrada pertence. | `String`
| created_at                                       | Data de processamento da transação / de entrada da transação no extrato. Formato: datetime. | `String`
| status                                  | Status atual da transação. Varia de acordo com o tipo de transação. | `String` 
| id            | Identificador da transação que originou essa movimentação no extrato | `String`

---
<br>

Abaixo temos os campos que são utilizados em cada tipo de transação no extrato:

| Chave                 |    Descrição             | Tipo        | Transação                   |
| --------------------- | -------------------------| ------------| ----------------------------|
|operation_amount |Valor bloqueado ou desbloqueado na operação. | String | balance_blocked, balance_unblocked)
|reason | Motivo do bloqueio ou desbloqueio. | String | balance_blocked, balance_unblocked
|acquirer | Instituição responsável pela liquidação de recebíveis. | String | card_payment
|card_network_code | Código da rede do cartão. | String  | card_payment
|card_network_name | Nome da rede do cartão. | String  | card_payment
|card_type | Tipo do cartão. | String  | card_payment
|is_prepayment | Informa se o cartão é do tipo pré-pago ou não. | Boolean | card_payment
|counter_party | Dados do beneficiário da transação. | Object  | external, external_refund, instant_payment, internal, salary, salary_portability, salary_portability_refund, salary_portability_employer_refund
|delayed_to_next_business_day | Informa se a transação foi adiada para o próximo dia útil ou não. | Boolean | external
|fee_amount | Valor da taxa da transação. | Integer |  external, external_refund, instant_payment, internal, outbound_stone_prepaid_card_payment, outbound_stone_prepaid_card_payment_refund, outbound_stone_prepaid_card_payment_chargeback, outbound_stone_prepaid_card_withdrawal, outbound_stone_prepaid_card_withdrawal_refund, payment, payment_refund
|operation_amount | Valor da operação, sem o valor da taxa. | Integer | external, external_refund, instant_payment, internal, outbound_stone_prepaid_card_payment, outbound_stone_prepaid_card_payment_refund, outbound_stone_prepaid_card_payment_chargeback, outbound_stone_prepaid_card_withdrawal, outbound_stone_prepaid_card_withdrawal_refund, payment, payment_refund
|operation_id | Código identificador da operação. | String | external, instant_payment, internal, outbound_stone_prepaid_card_payment, outbound_stone_prepaid_card_payment_refund, outbound_stone_prepaid_card_payment_chargeback, outbound_stone_prepaid_card_withdrawal, outbound_stone_prepaid_card_withdrawal_refund, payment, payroll
|refund_reason_code | Código da razão da devolução da transação. | String | external, external_refund, salary_portability_refund
|refund_reason_description | Descrição da razão de devolução da transação. | String | external, external_refund, salary_portability_refund
|scheduled_at | Data em que foi realizado o agendamento da transação. | String | external, internal, payment
|scheduled_to_effective | Data que o sistema agendou para realizar a transação. | String | external
|scheduled_to_requested | Data solicitada para agendamento da transação. | String | external
|original_operation_id | Código identificador da operação original. | String | external_refund, payment_refund
|refunded_at | Data em que a transação foi devolvida. | String | external_refund, payment_refund
|schedule_to | Data para qual foi realizado o agendamento da transação. | String | internal
|account_settlement_policy_retention | Dados da conta em que será realizada a retenção de liquidação de conta | Object | loan_payments
|original_operation_entry  | Dados da operação original. | Object | loan_payments
|original_operation_entry_type | Tipo da operação original. | String | loan_payments
|acquirer_code | Código do adquirente. | String | outbound_stone_prepaid_card_payment, outbound_stone_prepaid_card_payment_refund, outbound_stone_prepaid_card_payment_chargeback, outbound_stone_prepaid_card_withdrawal, outbound_stone_prepaid_card_withdrawal_refund
|acquirer_name | Nome do adquirente | String | outbound_stone_prepaid_card_payment, outbound_stone_prepaid_card_payment_refund, outbound_stone_prepaid_card_payment_chargeback, outbound_stone_prepaid_card_withdrawal, outbound_stone_prepaid_card_withdrawal_refund
|card_acceptor | Dados sobre o cartão em que foi realizada a compra. | Object | outbound_stone_prepaid_card_payment, outbound_stone_prepaid_card_payment_refund, outbound_stone_prepaid_card_payment_chargeback, outbound_stone_prepaid_card_withdrawal, outbound_stone_prepaid_card_withdrawal_refund
|card_last_four_digits | Últimos dígitos do cartão em que foi realizada a compra. | String | outbound_stone_prepaid_card_payment, outbound_stone_prepaid_card_payment_refund, outbound_stone_prepaid_card_payment_chargeback, outbound_stone_prepaid_card_withdrawal, outbound_stone_prepaid_card_withdrawal_refund
|transaction_authorization | Dados sobre a autorização da transação de uma compra feita com cartão. | Object | outbound_stone_prepaid_card_payment, outbound_stone_prepaid_card_payment_refund, outbound_stone_prepaid_card_payment_chargeback, outbound_stone_prepaid_card_withdrawal, outbound_stone_prepaid_card_withdrawal_refund
|transaction_chargeback | Dados sobre o estorno da transação de uma compra feita com cartão. | Object | outbound_stone_prepaid_card_payment_chargeback
|barcode | Código de barras de um boleto. | String | payment
|details | Dados sobre o pagamento de um boleto. Veja mais sobre esse campo aqui | Object  | payment, payment_refund
|scheduled_to | Data para qual foi agendado o pagamento de um boleto. | String  | payment
|writable_line | Linha digitável de um boleto. | String | payment, payment_refund

---
<br>

Campos do Objeto `counter_party` : 

| Chave                     |    Descrição                        | Tipo    
| ------------------------- | ----------------------------------  | -------------------------|
| account                   |   Dados da conta destino.           |   `Object`
| entity                    |   Dados Pessoais.                   |   `Object`


<br>

Campos do Objeto `account` :

| Chave                     |    Descrição                        | Tipo    
| ------------------------- | ----------------------------------  | -------------------------|
| account_code              |   Código da Conta.                  |   `Integer`
| account_type              |   Tipo da conta.                    |   `String` 
| branch_code               |   Agência da conta.                 |   `Integer`
| institution               |   Código da instituição da conta.   |   `Integer`
| institution_name          |   Nome da instituição da conta.     |   `String`


<br>

Campos do Objeto `entity` :

| Chave                     |    Descrição                                | Tipo    
| ------------------------- | ------------------------------------------  | -------------------------|
| document                  | Número de documento do responsável da conta.|  `Integer`
| document_type             | Tipo de documento do responsável da conta.  |  `String`
| name                      | Nome do responsável da conta.               |  `String`


<br>

Campos do Objeto `account_settlement_policy_retention` :

| Chave                        |    Descrição                                | Tipo    
| ---------------------------- | ------------------------------------------  | -------------------------|
| account_settlement_policy_id | Identificador único dos juros do empréstimo/crédito. |  `String`       
| applied_retention_rules      | Dados de onde será aplicada as regras de juros.      |  `Object`       
| retained_amount              | Valor dos juros.                                     |  `Integer`
| total_amount                 | Valor total do empréstimo/crédito.                   |  `Integer`

<br>

Campos do Objeto `applied_retention_rules` :

| Chave                        |    Descrição                                | Tipo    
| ---------------------------- | ------------------------------------------  | -------------------------|
| acquirer                     | Instituição responsável pela liquidação de recebíveis. | `String`
| card_network_code            | Código da rede do cartão.                   | `String`
| card_type                    | Tipo de cartão.                             | `String`
| desired_rule_amount          | Valor desejado do juros.                    | `Integer`
| effective_rule_amount        | Valor efetivo dos juros.                    | `Integer`
| is_prepayment                | Informa se o cartão é do tipo pré-pago ou não. | `Boolean`
| retained_portion             | Dados sobre a porcentagem dos juros.        | `Object`
| same_ownership               | Informa se o pagador pode ser da mesma instituição que o beneficiário. | `String`
| target_account_id            | Identificador da conta que ira receber o empréstimo/crédito. | `String`


<br>

Campos do Objeto `retained_portion` :


| Chave                        |    Descrição                                | Tipo    
| ---------------------------- | ------------------------------------------  | -------------------------|
| coefficient                  | Valor do coeficiente para cálculo dos juros do empréstimo/crédito. | `Integer`
| exponent                     | Valor do expoente para cálculo dos juros do empréstimo/crédito. | `Integer`


<br>

Campos do Objeto `original_operation_entry` :


| Chave                        |    Descrição                                | Tipo    
| ---------------------------- | ------------------------------------------  | -------------------------|
| amount                       | Valor original retido para pagamento do empréstimo/crédito. | `Integer`
| barcode                      | Código de barras referente ao empréstimo/crédito. | `String`
| barcode_payment_invoice_id   | Identificador do pagamento do código de barras do empréstimo/crédito. | `String`
| beneficiary                  | Dados do beneficário do empréstimo/crédito. | `Object`
| created_at                   | Data da criação do pedido do empréstimo/crédito. | `String`
| invoice_type                 | Tipo de fatura do empréstimo/crédito. | `String`
| operation                    | Tipo de operação do empréstimo/crédito. | `String`
| writable_line                | Linha digitável do empréstimo/crédito.  | `String`


<br>

Campos do Objeto `beneficiary` :

| Chave                        |    Descrição                                | Tipo    
| ---------------------------- | ------------------------------------------  | -------------------------|
| document                     | Documento do beneficiário.                  |  `String`
| document_type                | Tipo do documento do beneficiário.          |  `String`
| legal_name                   | Nome completo ou razão social do beneficiário. | `String`
| trade_name                   | Nome fantasia do beneficiário. Campo não obrigatório. | `String`


<br>

Campos do Objeto `card_acceptor` :

| Chave                        |    Descrição                                | Tipo    
| ---------------------------- | ------------------------------------------  | -------------------------|
| city                         | Cidade onde foi realizada a compra.         | `String`
| country                      | País onde foi realizada a compra.           | `String`
| mcc                          | Tipo de taxa que será aplicada à compra. (Ex.: taxa de intercâmbio, taxa da rede do cartão, entre outras) | `String`
| name                         | Nome do dono do cartão.                     | `String`


<br>

Campos do Objeto `transaction_authorization` :


| Chave                        |    Descrição                                | Tipo    
| ---------------------------- | ------------------------------------------  | -------------------------|
| authorization_medium         | Tipo de autorização recebida na compra.     | `String`
| captured_value               | Dados do valor na moeda em que ocorreu a compra, sem taxas. | `Object`
| conversion_rate              | Taxa de conversão.                          | `String`
| country                      | Código do país onde ocorreu a compra.       | `String`
| iof_fee                      | Taxa de IOF. Campo não obrigatório.         | `Integer`
| pos_authorization_time       | Data da autorização.                        | `String`
| value                        | Dados do valor convertido pra BRL, com taxas. | `Object`


<br>

Campos do Objeto `captured_value` :


| Chave                        |    Descrição                                | Tipo    
| ---------------------------- | ------------------------------------------  | -------------------------|
| amount                       | Valor capturado no momento da compra via cartão, sem taxas. | `Integer`
| currency                     | Moeda utilizada no momento da compra via cartão.  | `String`


<br>

Campos do Objeto `value` :


| Chave                        |    Descrição                                | Tipo    
| ---------------------------- | ------------------------------------------  | -------------------------|
| amount                       | Valor total da compra convertido para BRL, com taxas incluídas. | `Integer`
| currency                     | Moeda convertida para BRL.                  | `String`


<br>

Campos do Objeto `transaction_chargeback` :


| Chave                        |    Descrição                                | Tipo    
| ---------------------------- | ------------------------------------------  | -------------------------|
| charged_back_at              | Data em que ocorreu a devolução do valor da compra. | `String`
| id                           | Identificador da devolução da transação.    | `String`
| value                        | Dados do valor estornado.                   | `Object`