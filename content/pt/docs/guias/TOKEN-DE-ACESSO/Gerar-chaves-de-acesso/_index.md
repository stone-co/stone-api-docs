---
title: "Gerar Chaves de Acesso"
linkTitle: "Gerar Chaves de Acesso"
date: 2021-06-28T09:00:00-03:00
lastmod: 2021-06-28T09:00:00-03:00
weight: 2

description: >

---
<br>
Para obter o seu Access Token, será necessário gerar um par de chaves RSA 4096. Você deverá assinar o JWT com a chave privada e nos enviar a chave pública no formato PEM e extensão .pub. <br><br>

Embora existam vários métodos para criação de pares de chaves público e privada, a ferramenta OpenSSL de código aberto é uma das mais usadas, por isso, recomendamos o seu uso.

Em todas as plataformas disponíveis - Linux, MacOS e Windows, os comandos do OpenSSL são iguais: <br>

    openssl genrsa -out mykey.pem 4096
    openssl rsa -in mykey.pem -pubout > mykey.pub

Algumas dicas importantes: 

{{< alert >}}
Linux: é uma ferramenta padrão que já vem instalada em quase todas as distribuições.

MacOS: há algumas formas de instalar, sendo o uso da ferramenta “brew” um dos mais simples. 

Windows: É possível adquirí-la através da [Página de Download](https://slproweb.com/products/Win32OpenSSL.html), e obter detalhes sobre o processo de instalação através do [Tutorial de Instalação](https://tecadmin.net/install-openssl-on-windows/). Após a instalação, você deve acrescentar o caminho do programa na variável PATH e adicionar mais uma variável OPENSSL_CONF para o arquivo openssl.cfg, que normalmente vai ser C:\Program Files\OpenSSL-Win64\bin\openssl.cfg. Atente-se para ajustar o caminho para o local onde você instalou a ferramenta.
{{< /alert >}}

Agora você já pode gerar o seu par de chaves. A chave pública será solicitada pelo nosso time durante a integração. Nós deixamos a chave pública guardada de forma segura e usaremos para validar o seu token num processo de criptografia assimétrica. A chave que deverá ser enviada para Stone através do formulário de integração é sempre a chave pública (arquivo .pub).<br><br>

**Atenção!**  
<br>Você nunca deve compartilhar a chave privada (arquivo.pem)! A chave privada deve ser armazenada de forma segura por você. <br>Em posse da sua chave privada, qualquer aplicação pode decodificar a assinatura e verificar se ela é válida. <br> Por isso destacamos a importância de manter essa informação em segredo.

Depois de obter seu par de chaves, você está pronto para iniciar conosco o [Cadastro da Aplicação](/docs/guias/token-de-acesso/cadastro-da-aplicacao/). 
