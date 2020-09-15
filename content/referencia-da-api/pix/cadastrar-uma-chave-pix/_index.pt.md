---
title: "Cadastrar uma Chave PIX"
date: 2020-09-14T18:14:34-03:00
lastmod: 2020-09-14T18:14:34-03:00
weight: "2"
draft: false
---
{{< notice info >}}
Beta: O PIX ainda está em beta, o que significa que temos um grupo pequeno testando a funcionalidade para que então possamos liberar para todos.
{{< /notice >}}

A chave PIX é um identificador que vincula uma conta ao arranjo de pagamentos instantâneos, permitindo o recebimento de um PIX. As Chaves PIX poderão ser cadastradas a partir do dia 05 de outubro.

As chaves podem ser:
- Telefone celular;
- CNPJ/CPF;
- E-mail;
- Chave aleatória - código identificador que permite o recebimento do PIX por meio de QRCodes

##### Exemplo de requisição:
```textmate
POST /api/v1/pix_entries
authorization: subject application:participante
content-type: application/json
x-stone-idempotency-key: string()
```

```textmate
{
   "key": string() | null no caso de RANDOM_KEY,
   "key_type": "PHONE", # "CPF" | "CNPJ" | "PHONE" | "EMAIL" | "RANDOM_KEY"
   "account_id": uuid(), # conta do participante indireto | cliente stone
   "participant_ispb": ispb_do_particiapnte(),
   "customer_type": "stone_account" | "external_account",
   "customer_account": {
     "branch_code": "0001", #not required
     "account_code": "0007654321",
     "account_type": "CACC" | "SLRY" | "SVGS" (cacc - conta corrente, slry - conta salário, svgs)),
     "opened_at": "2019-11-18T03:00:00Z" data de abertura da conta no ISPB
   } | null # null ou ignorado em caso do type ser "stone_account"
   "customer_entity": {
     "name":"fulano de tal",
     "document_type": "cpf" | "cnpj",
     "document": cpf() | cnpj(),
   } | null # null ou ignorado em caso do type ser "stone_account"
}
```

##### Exemplo de resposta:
```textmate
202 CONTINUE
content-type: application/json
{
  "id": uuid(),
  "idempotency_key": string()
}
```

##### Webhook:
```textmate
{
   "input": {
     key: uuid(),
     key_type: "RANDOM_KEY"
     customer_type: "stone_account" | "external_account",
     customer_id: uuid()
   },
   "creation_date": datetime(),
   "error_description": string(),
   "status": "pending" | "created" | "rejected" (eventos Kafka)
}
```

_OBS: EVP quer dizer chave aleatória._