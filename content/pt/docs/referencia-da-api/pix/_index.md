---
title: "PIX (Beta)"
linkTitle: "PIX (Beta)"
lastmod: 2021-03-31T18:00:00-03:00
weight: 16
draft: false
description: >
---      
---
<br>

{{% pageinfo %}}
A integração com o Pix ainda está em Alpha, o que significa que temos um grupo pequeno de parceiros testando a funcionalidade para que possamos fazer ajustes e então liberar para todos os parceiros.
{{% /pageinfo %}}

<br>

## O que é o Pix?
---
<br>

O Pix é a nova modalidade de pagamentos instantâneos do Banco Central, que entrou em vigor no Brasil inteiro no dia 16 de novembro de 2020. 

Além de sua ampla grade de funcionamento e pequeno tempo de processamento, o Pix busca simplificar a experiência do usuário que consegue passar o dinheiro para outro participante informando apenas seu telefone, documento (CPF/CNPJ), seu email ou lendo um QR Code. Lembrando que também é possível fazer um Pix informando os dados bancários, como é feito em uma TED.

<br>

{{< alert title="Horário de funcionamento" >}}
<br>

A API de Pix fica disponível todos os dias da semana e 24 horas por dia, pois é uma modalidade de pagamento instantânea.	
{{< /alert >}}

<br>

## Participantes do Pix
---
<br>

O Pix tem quatro tipos de participantes principais:<br><br>
- **Participante Direto (PSP direto)**: Instituição homologada junto ao Banco Central (BC) que fará o processamento do Pix junto aos sistemas do BC tanto do ponto de vista informacional, quanto do ponto de vista financeiro. Ou seja, além de ser responsável por toda a troca de informação com os sistemas do Pix, quando agindo como instituição do pagador será a instituição que enviará o dinheiro para o BC e quando agindo como instituição do recebedor receberá o dinheiro do BC. Fazendo um comparativo com o arranjo de cartões seria mais ou menos o equivalente a adquirência e o emissor dependendo se estamos agindo ao lado do recebedor ou do pagador respectivamente. <br>
- **Participante Indireto (PSP indireto)**: Instituição homologada junto ao Banco Central que fará parte do arranjo do Pix tanto do ponto de vista informacional, quanto do ponto de vista financeiro, mas que usará um participante direto para fazer a intermediação da integração com os sistemas do Pix. Fazendo um comparativo com o arranjo de cartões seria mais ou menos o equivalente a uma subadquirente. <br>
- **Usuário Recebedor**: é quem vai receber o dinheiro da transação que está sendo efetuada. Fazendo um comparativo com o arranjo de cartões, seria mais ou menos o equivalente ao lojista. <br>
- **Usuário Pagador**: é quem vai pagar a transação que está sendo efetuada. Fazendo um comparativo com o arranjo de cartões seria mais ou menos o equivalente ao comprador / dono do cartão.<br><br>



## Status de um Pix
---
<br>

Os status possiveis são: `CREATED`, `CONFIRMED`, `FAILED`, `MONEY_RESERVED`, `REFUNDED` e `SETTLED`. A partir do momento que um Pix é criado, ele **nunca expira**.

- `CREATED` -  Significa que o Pix foi criado e está aguardando confirmação.

- `CONFIRMED` - Significa que o Pix que foi criado e estava com o status `CREATED`, foi confirmado.

- `MONEY_RESERVED` - Significa que o Pix que foi confirmado e estava com o status `CONFIRMED`, teve o dinheiro retirado da conta do cliente e reservado em uma conta gráfica a parte para a operação.

- `SETTLED` - Significa que o Pix que estava com o estado de `MONEY_RESERVED`, foi finalizado e liquidamos o dinheiro reservado na conta gráfica da operação.

- `REFUNDED` - Significa que o Pix que estava com o estado de `MONEY_RESERVED`, foi rejeitado ou devolvido.

- `FAILED` - Significa que o Pix que estava com o estado de `CONFIRMED`, falhou no momento de reservar o dinheiro, podendo ser devido a falta de saldo do cliente, e portanto ele vai para o estado de `FAILED` e o fluxo da operação se encerra.<br><br>



## API Pix do BACEN
---
<br>

Para determinados casos, é possível utilizar a API de Pix do BACEN. Para acessá-la, clique [aqui](https://bacen.github.io/pix-api/index.html )

<br>

## Campos de Pix
---

<br>

##### Chave Pix

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

##### Conta do usuário
| Chave                        | Tipo  | Descrição                                                              | Regra de negócio        |
| ---------------------------- | -------------- | -------------------------------------------------------- | ------------------------------ |
| branch_code | String | Número da agência da conta.  | Caso não seja informado será assumido o valor 0001. |
| account_code | String | Número da conta bancária, sempre com dígito. | Obrigatório |
| account_type | String | Código que identifica o tipo de conta. Os valores possíveis são:`CC` - Conta Corrente, `CD` - Conta de Depósito, `CG` - Conta garantida, `CI` - Conta de Investimento, `PG` - Conta de Pagamento, `PP` - Poupança. | Obrigatório |
| opened_at | String | Datetime a abertura da conta que será atrelada a chave. <br> Formato: "2019-11-18T03:00:00Z". | Obrigatório nos casos de em que campo `beneficiary_type` for `external_account`. |

<br><br>

##### Dados do usuário

| Chave                        | Tipo  | Descrição                                                              | Regra de negócio        |
| ---------------------------- | -------------- | -------------------------------------------------------- | ------------------------------ |
| name | String | Nome completo do usuário ou Razão Social no caso de clientes PJ.  | Obrigatório |
| type | String | Identifica se o usuário é uma pessoa física ou uma pessoa jurídica. Os valores são respectivamente: `NATURAL_PERSON` ou `LEGAL_PERSON`. | Obrigatório |
| document | String | Número do CPF ou do CNPJ do usuário.  | Obrigatório |




<br><br>

##### Para realizar transações com Pix, siga de acordo com o menu abaixo:
