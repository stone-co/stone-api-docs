---
title: "Criar nova identidade"
slug: "criar-usuária-1"
excerpt: "Cria um novo usuário e sua organização, caso exista."
hidden: false
createdAt: "2019-07-03T18:29:01.266Z"
updatedAt: "2019-12-03T16:55:47.197Z"
---
[block:callout]
{
  "type": "warning",
  "title": "Conteúdo criptografado",
  "body": "O body deste endpoint (abaixo) deve ser criptografado antes de ser enviado (JWE)."
}
[/block]
O conteúdo a ser criptografado é um JSON com a seguinte estrutura:
[block:code]
{
  "codes": [
    {
      "code": "{  \n  user:{\n    document: \"00000000000\",\n    document_type: \"cpf\",\n    full_name: string,\n    email: string\n  },\n  organization: {\n    document: \"00000000000000\",\n    document_type: \"cnpj\",\n    full_name: string,\n    email: string\n  }\n}",
      "language": "json"
    }
  ]
}
[/block]
Para gerar um token JWT criptografado (usando JWE) temos 3 passos:
1. Criar um conteúdo a ser criptografado (payload), no caso, o conteúdo JSON acima;
2. Buscar a chave pública da Stone no endpoint /api/v1/discovery/keys, cujo campo "use" seja igual a "enc";
3. Usar uma biblioteca passando o payload, a chave pública e o algoritmo utilizado, no caso, RSA-OAEP-256