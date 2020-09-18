---
title: "Códigos De Resposta"
date: 2020-05-02T18:33:23-03:00
lastmod: 2020-05-13T18:33:23-03:00
weight: "6"
draft: false
---

Nossa API usa como retorno os [códigos HTTP](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) padrão para indicar tanto o sucesso de uma requisição, quanto para indicar falha. Pode-se utilizar a tabela abaixo como referência:

| Código | Significado                                                                              |
| ------ | ---------------------------------------------------------------------------------------- |
| 200    | Tudo ocorreu como deveria e sua requisição foi processada com sucesso.                   |
| 201    | A requisição foi bem sucedida e um novo recurso foi criado como resultado.               |
| 202    | Processo iniciado com sucesso.                                                           |
| 204    | Bem sucedido, sem conteúdo de resposta.                                                  |
| 400    | Algum parâmetro obrigatório não foi passado ou os parâmetros passados não estão corretos.|
| 401    | Falta de autenticação para acessar este endpoint.                                        |
| 403    | Falta de autorização para acessar este endpoint.                                         |
| 404    | Endpoint não encontrado, revise a URL passada.                                           |
| 409    | A solicitação atual conflitou com o recurso que está no servidor.                        |
| 422    | Entidade não processável. Não é uma ação válida para os dados enviados.                  |
| 500    | Erro interno do servidor, tente sua requisição novamente.                                |

{{< notice tip >}}
**Identificador da Requisição**
<br>O cabeçalho da resposta sempre inclui um campo identificador da requisição, chamado `x-request-id`. Este valor deve ser enviado sempre que precisar de suporte, já que ele nos permite encontrar a chamada no nosso sistema e verificar o que possa ter dado errado.
{{< /notice >}}

