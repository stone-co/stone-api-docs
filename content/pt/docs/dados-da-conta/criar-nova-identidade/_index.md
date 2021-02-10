---
title: "Criar nova identidade"
excerpt: "Cria um novo usuário e sua organização, caso exista."
hidden: false
createdAt: "2019-07-03T18:29:01.266Z"
updatedAt: "2019-12-03T16:55:47.197Z"
weight: 1
description: >



---
Cria um novo usuário e sua organização, caso exista.


---

```http 
POST https://sandbox-api.openbank.stone.com.br/api/v1/users/signup
```
---

**BODY PARAMS**

---

**jwe***  `string` 



{{% pageinfo %}}
**Conteúdo Criptografado**

O body deste endpoint (abaixo) deve ser criptografado antes de ser enviado (JWE).
{{% /pageinfo %}}



O conteúdo a ser criptografado é um JSON com a seguinte estrutura:

```JSON
{
	"user": {
		"document": "00000000000",
		"document_type": "cpf",
		"full_name": "string",
		"email": "string"
	},

	"organization": {
		"document": "00000000000000",
		"document_type": "cnpj",
		"full_name": "string",
		"email": "string"

	}
}
```




Para gerar um token JWT criptografado (usando JWE) temos 3 passos:
1. Criar um conteúdo a ser criptografado (payload), no caso, o conteúdo JSON acima;
2. Buscar a chave pública da Stone no endpoint /api/v1/discovery/keys, cujo campo "use" seja igual a "enc";
3. Usar uma biblioteca passando o payload, a chave pública e o algoritmo utilizado, no caso, RSA-OAEP-256.