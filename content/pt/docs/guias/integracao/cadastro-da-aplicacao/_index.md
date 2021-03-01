---
title: "Cadastro da Aplicação"
slug: "Cadastro-da-aplicação"
hidden: false
date: "2020-01-27T00:38:05.163Z"
lastmod: "2020-09-29T12:03:51.843Z"
weight: 1
---

---

<br>

1. Será enviado pelo nosso time de parcerias o formulário para criação das [credenciais da sua aplicação](/docs/guias/integracao/cadastro-da-aplicacao/#credenciais-da-minha-aplicação).

{{% pageinfo %}}
**Atenção**

Será necessário [gerar um par de chaves RSA 4096](/docs/guias/integracao/cadastro-da-aplicacao/gerando-o-par-de-chaves) e compartilhar a **chave pública** conosco no formato PEM e extensão .pub

{{% /pageinfo %}}

<br>

2. Você será inserido na nossa ferramenta de comunicação com o time de suporte e terá durante todo o processo de integração uma equipe te ajudando com as possíveis dúvidas. Lá serão disponibilizadas suas credencias de sandbox. 

{{% pageinfo %}}
**Chave Pública**

A chave que deverá ser enviada para a Stone através do formulário é a **chave pública** e **não** a **chave privada**. Não queremos o arquivo .pem, mas sim o .pub

{{% /pageinfo %}}

<br>


#### **Credenciais da minha aplicação**

O identificador que representa uma aplicação parceira na API Stone OpenBank é chamado de `cliend_id`. Ele é gerada pela Stone e é único. Ele será utilizada no processo de [autenticação](/docs/guias/integracao/autenticacao) junto a API identificando assim todos os requests provenientes dessa aplicação. 

Alguns processos da nossa API, como o próprio processo de [autenticação](/docs/guias/integracao/autenticacao), envolvem uma etapa de criptografia assimétrica, assim na hora da criação do `client_id` da sua aplicação atrelaremos a ele a chave pública fornecida por você. 

Montamos um guia para te ajudar a gerar seu [par de chaves assimétricas](/docs/guias/integracao/cadastro-da-aplicacao/gerando-o-par-de-chaves).

Cada `client_id` tem também as URIs de webhook e URI de redirect que serão configuradas de acordo com as informações fornecidas pelo parceiro.

<br>
