---
title: "Cadastro da Aplicação"
date: 2020-05-14T14:47:07-03:00
lastmod: 2020-05-14T14:47:07-03:00
weight: "2"
draft: false
---

#### Primeiros Passos

O primeiro passo para a integração é obter o acesso ao nosso ambiente de Sandbox. Este ambiente reflete o de Produção e deve ser utilizado para testes.

Utilizamos [OpenID Connect](https://openid.net/connect/) para a [autenticação](https://docs.openbank.stone.com.br/docs/referencia-de-api/autenticacao-guides) em nossa API. Para obter acesso e conseguir se autenticar em nossa API de Sandbox, siga os seguintes passos:

1. Solicite o ClientID preenchendo o [formulário](https://docs.google.com/forms/d/e/1FAIpQLSf_qlDh41jfthVn80v4S-HT40_Fr2wbkkGb-KuDrioEqepnXw/viewform).

  * _Será necessário gerar um par de chaves RSA 4096 e compartilhar a **chave pública** conosco no formato .pem. O passo a passo para gerar essas chaves está detalhado abaixo, como também no formulário._

  *  _A URI de redirecionamento faz parte do fluxo [OAuth 2.0](https://oauth.net/2/)._

2. Enviaremos o seu ClientID para o e-mail cadastrado. Com ele você conseguirá realizar o processo de [autenticação](https://docs.openbank.stone.com.br/docs/referencia-de-api/autenticacao-guides). Após a realização de testes através de nosso Sandbox e estiver pronto para a Homologação, entre em contato através de parcerias@openbank.stone.

Para entender qual [modelo de parceria](https://docs.openbank.stone.com.br/docs/padroes-e-definicoes-guides#section-modelos-de-parcerias) melhor se aplica a sua aplicação, pode ser necessário realizar algumas reuniões presenciais ou por vídeo com a gente.

3. Realizaremos o procedimento de [homologação](https://docs.openbank.stone.com.br/docs/testando-a-api-guides#section-homologando-sua-integra%C3%A7%C3%A3o) para garantir o funcionamento da integração. Em seguida, a utilização em Produção já será possível.

{{< notice info >}}
**Atenção à chave enviada no formulário**
<br>A chave que deverá ser enviada para a Stone através do formulário é a **chave pública** e **não** a chave **chave privada**.
{{< /notice >}}

#### Operações em nossa API

Em SandBox, por padrão, a aplicação nasce com as seguintes autorizações:
1. Realizar transferências externas;
2. Realizar transferências internas;
3. Pagar boletos;
4. Ler o extrato;
5. Ler o saldo;
6. Ler os contatos de contas de pagamento;
7. Criar, editar e deletar um contato de conta de pagamento;
8. Ler taxas.

Quando colocarmos a Aplicação em produção, a Stone e o Parceiro irão validar quais acessos são realmente necessários para a solução criada, ajustando as autorizações.

#### Gerando o par de chaves

Para gerar as chaves recomendamos o uso da ferramenta OpenSSL, disponível para Linux, MacOS e Windows.

Para Linux, é uma ferramenta padrão que já vem instalada em quase todas as distribuições.

Para MacOS, há algumas formas de instalar, sendo o uso da ferramenta "brew" um dos mais simples.

Para Windows, infelizmente é preciso configurar um pouco mais. É possível adquirí-la através da [Página de Download](https://slproweb.com/products/Win32OpenSSL.html), e obter detalhes sobre o processo de instalação através do [Tutorial de Instalação](https://tecadmin.net/install-openssl-on-windows/), em inglês.

Após a instalação, você deve acrescentar o caminho do programa na variável `PATH` e adicionar mais uma variável `OPENSSL_CONF` para o arquivo `openssl.cfg`, que normalmente vai ser `C:\Program Files\OpenSSL-Win64\bin\openssl.cfg`.

Mas **atenção** para ajustar o caminho para o local onde você instalou a ferramenta:

{{< figure src="https://files.readme.io/439cf15-be5a447-environment-vars.png" alt="Variáveis de Ambiente" >}}

Está pronto para gerar as chaves!

Em **todas** as plataformas - Linux, MacOS e Windows - os comandos do OpenSSL são iguais:

```json5
openssl genrsa -out mykey.pem 4096
openssl rsa -in mykey.pem -pubout > mykey.pub
```
