---
title: "Overview"
linkTitle: "Overview"
date: 2021-06-28T09:00:00-03:00
lastmod: 2021-06-28T09:00:00-03:00
weight: 1
draft: true
description: >

---
<br>
Para realizar chamadas na API Stone Open Banking, será necessário ter em mãos um Token de Acesso, ou Access Token. 
<br>O Token de Acesso gerado será no formato JWT e funcionará como uma chave de acesso para todas as requisições na API. 

<br>
<br>
O JWT é um padrão (RFC-7519) de mercado que define como transmitir e armazenar objetos JSON de forma compacta e segura entre diferentes aplicações. Os dados nele contidos podem ser validados a qualquer momento pois o token é assinado digitalmente.

<br>
<br>
Para receber esse Token de Acesso, será necessário que você gere um  JWT local, com suas partes em base64 já decodificadas e que deverá ser formado por três seções:

{{< alert >}}
Header: é um objeto JSON que define informações sobre o tipo do token (typ) - nesse caso JWT - e o algoritmo de criptografia usado em sua assinatura (alg) - no nosso caso usamos sempre o RS256. 

Payload: é um objeto JSON com as Claims (informações /alegações) da entidade tratada. São as informações que o JWT carrega, tipicamente a data de expiração do token ("EXPiration date"), quem gerou aquele token ("ISSuer"), quando ("Instanciated AT"), quem deve consumi-lo ("AUDience"), e o que mais for necessário entre as partes — como por exemplo um ID de usuário. Para esta etapa, você precisará de um ClientID, ou seja, o identificador recebido após realização do [Cadastro da sua Aplicação](/docs/guias/token-de-acesso/cadastro-da-aplicacao/) com a Stone. <br>Além disso, você deverá preencher os Claims conforme nosso processo de [Autenticação](/docs/guias/token-de-acesso/autenticacao/). 

Signature: É a assinatura única de cada token que é gerada a partir de um algoritmo de criptografia e tem seu corpo com base no header, no payload e na chave secreta definida pela aplicação. A assinatura é que vai garantir a integridade do token, se ele foi modificado e se realmente foi gerado por você. Para essa etapa, você já deve ter [gerado um par de chaves](/docs/guias/token-de-acesso/gerar-chaves-de-acesso/). 
{{< /alert >}}


Após a geração do token local formado acima, é preciso fazer uma chamada para o nosso servidor de [Autenticação](/docs/guias/token-de-acesso/autenticacao/) para que a gente faça a validação e retorne o Token de Acesso.

Provido com o Token de Acesso (token que já foi autenticado), você poderá acessar os endpoints da aplicação, que antes estavam restritos. Para realizar esse acesso, é preciso informar esse token no header Authorization da requisição e, por convenção, após a palavra Bearer. 

Em seguida, vamos te guiar para realizar as seguintes etapas para obtenção do seu Token de Acesso:

[Gerar um par de chaves de acesso](/docs/guias/token-de-acesso/gerar-chaves-de-acesso/)

[Cadastrar  sua Aplicação](/docs/guias/token-de-acesso/cadastro-da-aplicacao/)

[Fazer a Autenticação](/docs/guias/token-de-acesso/autenticacao/)

[Realizar Chamada Autenticada](/docs/guias/token-de-acesso/chamada-autenticada/)
