---
title: "Gerando o par de chaves"
slug: "gerando-o-par-de-chaves"
hidden: false
createdAt: "2020-01-27T15:29:06.333Z"
updatedAt: "2021-02-01T22:52:07.420Z"
weight: 1
---

---

<br>

Para gerar as chaves recomendamos o uso da ferramenta OpenSSL, disponível para Linux, MacOS e Windows.

Para Linux, é uma ferramenta padrão que já vem instalada em quase todas as distribuições.

Para MacOS, há algumas formas de instalar, sendo o uso da ferramenta "brew" um dos mais simples.

Para Windows, infelizmente é preciso configurar um pouco mais. É possível adquirí-la através da [Página de Download](https://slproweb.com/products/Win32OpenSSL.html), e obter detalhes sobre o processo de instalação através do [Tutorial de Instalação](https://tecadmin.net/install-openssl-on-windows/), em inglês.

Após a instalação, você deve acrescentar o caminho do programa na variável `PATH` e adicionar mais uma variável `OPENSSL_CONF` para o arquivo `openssl.cfg`, que normalmente vai ser `C:\Program Files\OpenSSL-Win64\bin\openssl.cfg`.

Mas **atenção** para ajustar o caminho para o local onde você instalou a ferramenta:

<br>

![imagem_gerando_o_par_de_chaves](/docs/guias/integracao/cadastro-da-aplicacao/gerando-o-par-de-chaves/gerando-o-par-de-chaves.png)



<br>

Você está pronto para gerar as chaves!

Em **todas** as plataformas - Linux, MacOS e Windows - os comandos do OpenSSL são iguais:

```shell
openssl genrsa -out mykey.pem 4096
openssl rsa -in mykey.pem -pubout > mykey.pub
```


Com seu par de chaves em mãos você está pronto para solicitar a criação da sua Chave de Sandbox. Envie um e-mail para parcerias@openbank.stone.com.br e solicite a sua.