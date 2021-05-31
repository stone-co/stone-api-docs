---
title: "Enviar fotos do usuário"
linkTitle: "Enviar fotos do usuário"
date: 2021-05-1731T11:30:00-03:00
lastmod: 2021-05-1731T11:30:00-03:00
weight: 3
---

Nesse endpoint serão enviadas as fotos do usuário necessários para realização da análise do KYC.

Deverá ser um request do tipo `PUT` com o endereço recebido no campo `url` do endpoint de [Consultar URL para envio da foto](/docs/referencia-da-api/kyc/consultar-url-para-foto/).

Exemplo:


```http request
PUT https://storage.googleapis.com/sdb-inside-gateway-frontend-3727/dXNlcjo4YTZmMzYzZi05Mzg4LTRiMzEtOGY0ZC05Zjk2NTAyY2Q1NzA=/53acaa13-f74b-4884-9420-f05b0ca79d25/doc_cnh_front.jpg?Expires=1615042461&GoogleAccessId=sdb-inside-gateway-c914%40inside-gateway-724c.iam.gserviceaccount.com&Signature=L1kzM4t2dq4qjzJ9gP%2BM7N7o2UWlQ59TXYui7OyMBe107TvVvSLEqN%2B1VL4Y5pBK%2FKqKoJWXKGizT6PNC%2BP5aPRz9qR94m1oPG2lsNspjFLO%2BdrRhdMTx21ylHNLIOWy54vJ5A84WIAlnAIZvHU7%2B1a2%2BRn8Wd3b62djcOpndFEAYCJDQBBENLwY%2B0Qs0KbumICdVWNqfxwttaOj%2FDpzMqp0TrDfmx8xfL5FyIzyBn7BYwfmhJeWU2VFjWVztohj0wiOIPcHlK%2BUkgGNYQ8qXYMY5aWeO6A55%2FO20QErizp%2BX2Ad2YlfS5mOozXvjFPShR7%2FRBxkhAj%2BEFx9EyVy2A%3D%3D
```

<br>

#### **HEADERS**
---

**Content-Type**: image/jpg
<br>
**x-goog-acl**: public-read

<br>

#### **QUERY PARAMS**
---

<br>

**Expires***
<br>Dado virá no campo `url` do endpoint de Consultar URL para envio da foto.

**GoogleAccessId***
<br>Dado virá no campo `url` do endpoint de Consultar URL para envio da foto.

**Signature***
<br>Dado virá no campo `url` do endpoint de Consultar URL para envio da foto.

<br>


#### **BODY PARAMS*
---

**photo*** `binary`

<br>

#### **Response**
---

```html
200 OK
```

---

```html
400 Bad Request
```

```json
<?xml version='1.0' encoding='UTF-8'?>
<Error>
<Code>ExpiredToken</Code>
<Message>The provided token has expired.</Message>
<Details>Request signature expired at: 2021-03-06T14: 54: 21+00: 00</Details>
</Error>
```


Próximo passo:

#### [Enviar dados do usuário](/docs/referencia-da-api/kyc/enviar-dados-do-usuario/).

