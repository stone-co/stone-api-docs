---
title: "Campos"
slug: "campos"
draft: true
weight: 4
date: "2020-04-26T21:06:22.337Z"
lastmod: "2020-10-20T15:04:35.254Z"
---
---

<br>

#### Boleto
---

<br>

|Chave|Descrição|Tipo|Caracteres (min/max)|
|-----|---------|----|----------|
|account_id	|Identificador da conta do beneficiário.|*String* | min: 36 / max: 36 |
|amount	|Valor do boleto bancário gerado, em centavos de reais.|*Integer* | min: 2000 / max: 9999999999999999999 |
|barcode|	Código de barras.	|*String* | min: 44 / max: 44 |
|beneficiary	|Objeto com os dados do beneficiário. Veja os campos desse `object` [abaixo](/docs/referencia-da-api/emissao-de-boletos/campos/#campos-do-objeto-beneficiary).	|*Object* | - - - - - - - - - - -   |
|created_at	|Data e hora em que o boleto bancário foi gerado. Nesse caso nunca será `null`. Formato ISO8601 `"YYYY-MM-DDThh:mm:ssZ"`.	|*String* | min: 20 / max: 20 |
|created_by	|Identificador único do usuário ou aplicação que criou a transação, no formato user:UUID4 ou application:UUID4respectivamente. Nesse caso nunca será `null`.	|*String* | min: 42 / max: 48 |
|customer|Objeto com os dados do cliente que será informa como pagador no ato de registro do boleto. Veja os campos desse `object` [abaixo](/docs/referencia-da-api/emissao-de-boletos/campos/#campos-do-objeto-customer).		|*Object* | - - - - - - - - - - -   |
|discount	|Objeto com os dados referentes ao desconto. Veja os campos desse `object` [abaixo](/docs/referencia-da-api/emissao-de-boletos/campos/#campos-do-objeto-discount).|*Object* | - - - - - - - - - - -   |
|expiration_date	|Data de vencimento do boleto bancário. Mesmo depois dessa data expirar o pagamento ainda pode ser feito. <br>Formato `"YYYY-MM-DD"`.	|*String* | min: 10 / max: 10 |
|fee	|Projeção da taxa que seria cobrada do beneficiário no ato de recebimento do pagamento caso o recebimento fosse agora. É atualizada com a taxa cobrada quando receber o pagamento. |	*Integer* | min: 0 / max: 4 |
|fee_metadata	|Objeto que identifica detalhes sobre a aplicação da taxa. Veja os campos desse `object` [abaixo](/docs/referencia-da-api/emissao-de-boletos/campos/#campos-do-objeto-fee_metadata).	|*Object* | - - - - - - - - - - -   |
|fine	|Objeto com os dados referentes a multa. Veja os campos desse `object` [abaixo](/docs/referencia-da-api/emissao-de-boletos/campos/#campos-do-objeto-fine).	|*Object* | - - - - - - - - - - -   |
|id	|Identificador único do boleto bancário, no formato UUID4.|	*String* | min: 36 / max: 36 |
|interest	|Objeto com os dados referentes aos juros. Veja os campos desse `object` [abaixo](/docs/referencia-da-api/emissao-de-boletos/campos/#campos-do-objeto-interest).	|*Object* | - - - - - - - - - - -   |
|invoice_type	|Tipo de boleto bancário. Valores suportados: `proposal`, `deposit` e `bill_of_exchange`.	|*String* | min: 7 / max: 16 |
|issuance_date	|Data da emissão de boleto bancário. Formato `"YYYY-MM-DD"`.	|*String* | min: 10 / max: 10 |
|limit_date	|Data limite para pagamento do boleto bancário. Sempre igual ou maior a data de vencimento. Formato `"YYYY-MM-DD"`.	|*String* | min: 10 / max: 10 |
|our_number	|Número que identifica unicamente um boleto para uma conta frente a outras instituições.	|*String* | min: 20 / max: 20 |
|receiver| Objeto com os dados do sacador avalista. Veja os campos desse `object` [abaixo](/docs/referencia-da-api/emissao-de-boletos/campos/#campos-do-objeto-receiver).	|*Object* | - - - - - - - - - - -   |
|registered_at	|Data e hora de registro do boleto bancário. Formato ISO8601 `"YYYY-MM-DDThh:mm:ssZ"`.|	*String* | min: 20 / max: 20 |
|settled_at	|Data e hora em que o dinheiro do pagamento do boleto é depositado na conta do beneficiário. Formato ISO8601 <br>`"YYYY-MM-DDThh:mm:ssZ"`.	|*String* | min: 20 / max: 20 |
|paid_at	|Data e hora em que foi realizado o pagamento. Formato ISO8601 <br>`"YYYY-MM-DDThh:mm:ssZ"`.	|*String* | min: 20 / max: 20 |
|status	|Status atual do boleto bancário, podendo ser um dentre os status à seguir: `CREATED`, `REGISTERED`, `SETTLED`, `CANCELLED` ou `EXPIRED`.	|*String* | min: 7 / max: 22 |
|writable_line	|Código de barras traduzido em números.	|*String* | min: 47 / max: 47 |


<br>

##### Campos do objeto `beneficiary`
---
<br>

|Chave|Descrição|Tipo|Caracteres (min/max)|
| --- | ------- | -- | -------------------|
| account_code  | Número da conta bancária.    | *String* | min: 3 / max: 20 |
| branch_code   | Número da agência da conta.  | *String* | min: 4 / max: 4 |
| document      | Número do documento do beneficiário sem pontos.              | *String* | min: 11 / max: 14 |
| document_type | Tipo do documento do beneficiário. Pode ser 'cpf' ou 'cnpj'. | *String* | min: 3 / max: 4  |
| legal_name    | É o nome que identifica o beneficiário para fins legais, administrativos e outros fins oficiais. | *String* | min: 1 / max: 50 |
| trade_name    | Nome fantasia do beneficiário. | *String* | min: 1 / max: 80 |

<br>

##### Campos do objeto `discount`
---
<br>

|Chave|Descrição|Tipo|Caracteres (min/max)|
| --- | ------- | -- | -------------------|
| date  | Data até a qual o desconto deve ser aplicado.<br>Formato ISO8601 `"YYYY-MM-DD"`.  | *String* | min: 8 / max: 8 |
| value | Valor percentual (%) do desconto que será aplicado ao boleto. O valor do deve ser maior que 0.0 e até 90.0. <br>Formato decimal. Ex: "20.0". | *String* | min: > 0 / max: < 90 |


<br>

##### Campos do objeto `fee_metadata`
---
<br>


|Chave|Descrição|Tipo|Caracteres (min/max)|
| --- | ------- | -- | -------------------|
|billing_exemption_participant	|Indica se o usuário possui alguma condição especial vigente.	|*Boolean* | min: 4 / max: 5 |
|fee	|Projeção da taxa que seria cobrada no ato de recebimento do pagamento caso o recebimento fosse agora.	|*Integer* | min: 0 / max: 4 |
|max_free	|Indica o número total de boletos emitidos que podem ser liquidados sem que haja custos por mês.	|*Integer* | min: 0 / max: 2 |
|original_fee	|Indica a taxa original do item para a essa conta.	|*Integer* | min: 0 / max: 4 |
|remaining_free	|Indica o número restante de boletos gerados que podem ser pagos sem que haja custos no periódo.	|*Integer* | min: 0 / max: 2 |




<br>


##### Campos do objeto `fine`
---
<br>

|Chave|Descrição|Tipo|Caracteres (min/max)|
| --- | ------- | -- | -------------------|
| date  | Data que define o dia a partir do qual a multa deve ser aplicada ao boleto.<br>Formato ISO8601 `"YYYY-MM-DD"`.                         | *String* | min: 10 / max: 10 |
| value | Valor percentual (%) da multa que será aplicada ao boleto. O valor do deve ser maior que 0.0 e até 2.0.<br>Formato decimal. Ex: "2.0". | *String* | min: > 0 / max: < 2  |



<br>


##### Campos do objeto `interest`
---
<br>


|Chave|Descrição|Tipo|Caracteres (min/max)|
| --- | ------- | -- | -------------------|
| date  | Data que define o dia a partir do qual os juros passam a ser aplicados ao boleto.<br>Formato ISO8601 `"YYYY-MM-DD"`.                      | *String* | min: 10 / max: 10 |
| value | Valor percentual (%) dos juros que serão aplicados ao boleto. O valor do deve ser maior que 0.0 e até 2.0.<br>Formato decimal. Ex: "2.0". | *String* | min: > 0 / max: < 1 |



<br>


##### Campos do objeto `customer`
---
<br>


|Chave|Descrição|Tipo|Caracteres (min/max)|
| --- | ------- | -- | -------------------|
| document      | Número do documento do pagador sem pontos.    | *String* | min: 11 / max: 14 |
| document_type | Tipo do documento do pagador. Pode ser `CPF` ou `CNPJ`.  | *String* | min: 3 / max: 4 |
| legal_name    | É o nome que identifica o pagador para fins legais, administrativos e outros fins oficiais. | *String*  | min: 1 / max: 50 |
| trade_name    | Nome fantasia do pagador.     | *String* | min: 1 / max: 80 |



<br>


##### Campos do objeto `receiver`
---
<br>


|Chave|Descrição|Tipo|Caracteres (min/max)|
| --- | ------- | -- | -------------------|
| document   | Número do documento do sacador avalista.  | *String* | min: 11 / max: 14 |
| legal_name | É o nome que identifica o sacado avalista para fins legais, administrativos e outros fins oficiais. | *String* | min: 1 / max: 50 |

