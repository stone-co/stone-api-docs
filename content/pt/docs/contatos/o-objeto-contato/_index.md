---
title: "O Objeto Contato"
slug: "o-objeto-contato"
hidden: false
createdAt: "2019-06-04T20:19:47.711Z"
updatedAt: "2019-06-06T19:54:27.690Z"
weight: 1
---




| Chave                     |    Descrição                        | Tipo    
| ------------------------- | ----------------------------------  | -------------------------|
| bank_accounts             | Lista de contas bancárias. Caso não seja preenchido, retornará []. | _List de Accounts_
| email                     | E-mail do contato. Caso não seja preenchido, retornará null.  |  _String_
| id                        | Identificador único do contato, no formato UUID4.   | _String_
| mobile                    | Número do celular do contato. Caso não seja preenchido, retornará null. | _String_
| name                      | Nome da proprietária da conta. | _String_
| tax_id                    | Documento do contato, pode ser cpf ou cnpj. Caso não seja preenchido, retornará null. |  _String_