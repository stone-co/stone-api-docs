---
title: "Objetos"
linkTitle: "Objetos"
date: 2020-09-17T18:00:00-03:00
lastmod: 2020-09-17T18:00:00-03:00
weight: 1
draft: true
description: >
      
---
### Chave Pix

| Chave                        | Tipo  | Descrição                                                              | Regra de negócio        |
| ---------------------------- | -------------- | -------------------------------------------------------- | ------------------------------ |
| key_Type | String | Indica o tipo de chave que será criada.<br>Valores possíveis: `CNPJ`, `CPF`, `phone`, `email` e `random_key`. | Obrigatório
| key | String | É onde deve ser informado o dado do usuário a ser usado como chave no caso de chaves do tipo celular, documento ou e-mail. <br> No caso de telefone deverá ser informado no  formato internacional. Ex.: “+5521912345678”. | Obrigatório nos tipos `CNPJ`, `CPF`, `phone` e `email`. |
| account_id | String | Identificador da Conta Stone de quem está chamando a API. | Obrigatório |
| participant_ispb | String | Código ISPB do participante. | Obrigatório nos casos de em que campo `beneficiary_type` for `external_account`. |
| beneficiary_type | String | Indica se o usuário é cliente da Conta Stone ou de um PSP indireto. Os valores possíveis são respectivamente: `stone_account` ou  `external_account`. | Obrigatório |
| beneficiary_account | Object | Dados da conta do usuário que serão atrelados a chave que está sendo criada. | Obrigatório |
| beneficiary_entity | Object | Dados do usuário. | Obrigatório |
| beneficiary_id  | String | Id do beneficiário.  | - |
| id | String | Identificador da requisição que pode ser para uma criação de chave ou uma remoção de chave. | - |
| status | String | Status da requisição.  | - |
| erro_description | String | Descreve especificamente qual foi o erro na criação da Chave PIX.  | Só é retornado quando o staus é `rejected`. |
| reason | String  | Razão da solicitação de remoção de uma Chave PIX. Valores possíveis são:`user_requested”, `account_closured`, `entry_inactivity`, `reconciliation`ou `fraud`. `entry_inactivity`deve ser usado quando por algum motivo a chave usada não está mais ativa, como um email ativo que foi desabilitado ou um CPF que foi inativado. | - |
| key_status | String  | Status da Chave PIX. Os possíveis valores são: `active`, `deleted`. | - |
| created_at | Datetime | Datetime de criação da Chave PIX.<br> Formato: "2019-11-18T03:00:00Z".  | - |
| claim_id | String | Identificador da reivindicação. | - |
| claim_type | String | Especifica o tipo de solicitação. | - |
| approval_response | Boolean | Indica se deseja aprovar a solicitação (`true`) ou rejeitar a solicitação (`false`). | - |
| aproval_reason | String | ???? | - |
| updated_at | Datetime | Datetime da atualização da reivindicação. <br> Formato: "2019-11-18T03:00:00Z". | - |
| expiration_at| Datetime | Datetime da expiração de uma reivindicação.<br> Formato: "2019-11-18T03:00:00Z". | caso a mesma não seja respondida dentro da data o Banco Central assumirá que a mesma aprovada. |

<br><br>

### Conta do usuário
| Chave                        | Tipo  | Descrição                                                              | Regra de negócio        |
| ---------------------------- | -------------- | -------------------------------------------------------- | ------------------------------ |
| branch_code | String | Número da agência da conta.  | Caso não seja informado será assumido o valor 0001. |
| account_code | String | Número da conta bancária, sempre com dígito. | Obrigatório |
| account_type | String | Código que identifica o tipo de conta. Os valores possíveis são:`CC` - Conta Corrente, `CD` - Conta de Depósito, `CG` - Conta garantida, `CI` - Conta de Investimento, `PG` - Conta de Pagamento, `PP` - Poupança. | Obrigatório |
| opened_at | String | Datetime a abertura da conta que será atrelada a chave. <br> Formato: "2019-11-18T03:00:00Z". | Obrigatório nos casos de em que campo `beneficiary_type` for `external_account`. |

<br><br>

### Dados do usuário

| Chave                        | Tipo  | Descrição                                                              | Regra de negócio        |
| ---------------------------- | -------------- | -------------------------------------------------------- | ------------------------------ |
| name | String | Nome completo do usuário ou Razão Social no caso de clientes PJ.  | Obrigatório |
| type | String | Identifica se o usuário é uma pessoa física ou uma pessoa jurídica. Os valores são respectivamente: `NATURAL_PERSON` ou `LEGAL_PERSON`. | Obrigatório |
| document | String | Número do CPF ou do CNPJ do usuário.  | Obrigatório |


