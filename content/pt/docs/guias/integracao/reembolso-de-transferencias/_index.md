---
title: "Reembolso de transferências"
slug: "reembolso-de-transferencias"
hidden: false
createdAt: "2020-10-07T19:43:06.948Z"
updatedAt: "2020-10-09T19:44:31.481Z"
weight: 8
---

---


#### **Porque uma transferência é reembolsada?**

Temos vários motivos para que uma transferência retorne, sendo os casos mais comuns conta, agência ou documento do destino errados e saldo insuficiente na conta de origem.
O reembolso de uma transferência somente é realizado quando ela ocorre para contas que não sejam Contas Stone, ou seja, quando ocorrem transferências externas.

<br>

#### **Quando pode ocorrer um reembolso**


##### **Saldo insuficiente**

Através da nossa API é possível agendar uma transferência. Ocorre refund nesses casos quando, na data agendada para a transferência, a conta origem não possuir saldo suficiente em conta.



##### **Dados da transferência incorretos**

Ao realizar uma transferência a usuária precisará enviar os dados da conta destino. Caso os dados de agência, conta ou documento do destino estejam incorretos ou inexistentes, a transferência retorna indicando esse erro.



##### **Tipo de transação ou finalidade inválida**

Caso a conta destinatária não seja do tipo especificado na transferência ou algum dado do destino é inválido. Exemplo: conta destinatária é corrente e o tipo informado era conta poupança ou envio no nome fantasia do destino enquanto era esperado o nome da razão social.



##### **Dados ausentes ou inválidos**

Quando uma transferência é realizada sem um dado obrigatório para a finalização da mesma, como código verificador, agência não informada ou quando o formato de um dado é inválido.
Alguns bancos utilizam códigos verificadores com letras no número da conta ao invés de números, nesses casos, a Conta Stone solicita que a conta origem digite ‘0’ no lugar dessa letra, para que a transferência ocorra com sucesso.



##### **CPF/CNPJ inapto junto à Receita Federal**

Nesse caso, a transferência é retornada para a conta de origem, porém, caso a mesma pessoa tenha acesso a outra conta com outro documento, ela poderá receber a transferência. Exemplo: A pessoa possui o CPF inapto junto à Receita Federal então não poderá receber a transferência em sua conta de pessoa física, porém, se essa mesma pessoa for sócia de uma empresa, nada impede que a transferência seja realizada para conta de pessoa jurídica, a não ser que o CNPJ também esteja inapto.




#### **Códigos de Reembolsos**

Ocorre somente em casos de transferências externas.

| Código                  | Descrição                                           | 
| ----------------------- | --------------------------------------------------- |
| 0                       | Ocorreu um erro de processamento no sistema de origem durante a transferência.
| 1                       | A conta destino é inexistente.
| 2                       | A conta ou agência destino é inexistente.
| 3                       | O documento do destino está incorreto.
| 4                       | Conta destinatária do crédito inválida para o tipo de transação ou finalidade.
| 5                       | Erro de processamento no sistema de origem durante a transferência.
| 6                       | Transferência supera limite para o tipo de conta destino / Conta destinatária do crédito inválida para o tipo de transação ou finalidade.
| 7                       | Não conformidade no pagamento. Exemplo: pagamento a um fornecedor com o valor diferente que o devido.
| 8                       | Os dados informados estão incorretos: Código Identificador de Transferência Inválido / Campo obrigatório ausente / Formato do dado inválido / Agência não informada.
| 9                       | CPF/CNPJ inapto junto à Receita Federal do Brasil.
| 10                      | A instituição financeira do destino não é válida.
| 11                      | A conta destino não pode ter mais de 13 dígitos para o tipo de conta escolhido. Por favor, confira os dados e tente novamente.
| 12                      | Por solicitação de cliente da instituição participante recebedora.
| 13                       | Devolução de ordem bancária pelo agente financeiro.
| 14                       | Beneficiário não identificado - Documentos com código de barras.