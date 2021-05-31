---
title: "Consultar URL para envio da foto"
linkTitle: "Consultar URL para envio da foto"
date: 2021-05-1731T11:30:00-03:00
lastmod: 2021-05-1731T11:30:00-03:00
weight: 2
---

Nesse endpoint será informada a URL de cada uma das fotos enviadas de um usuário.

Essa chamada deve ser realizada para cada foto que será enviada, por exemplo, na maioria dos casos é solicitada a foto da frente do documento, do verso do documento e de uma selfie com o documento, então esse endpoint, nesse caso, será chamado 3 vezes, cada um com o nome diferenciado do arquivo que será enviado.


```http request
POST https://sandbox-api.openbank.stone.com.br/api/v1/storage/{{image_name.jpg}}
```

<br>

#### **HEADERS**
---

**authorization***
<br>Bearer token

**Content-Type*** : image/jpeg

<br>

#### **PATH PARAMS**
---

Nome da imagem que será enviado, no formato `.JPG`.

<br>

#### **Response**
---

```html
200 OK
```

```json
{
    "public_url": "https://storage.googleapis.com/sdb-inside-gateway-frontend-3727/YXBwbGljYXRpb246MDY1ZWNiMDgtMjQzOS00MGMwLThlMTMtMmI0M2MyMTc0M2Uz/c0ea5f60-3d4c-4fc0-815e-bb62681fdd4b/image_name.jpg",
    "upload_info": {
        "headers": {
            "content-type": "image/jpeg",
            "x-goog-acl": "public-read"
        },
        "url": "https://storage.googleapis.com/sdb-inside-gateway-frontend-3727/YXBwbGljYXRpb246MDY1ZWNiMDgtMjQzOS00MGMwLThlMTMtMmI0M2MyMTc0M2Uz/c0ea5f60-3d4c-4fc0-815e-bb62681fdd4b/image_name.jpg?Expires=1622485791&GoogleAccessId=sdb-inside-gateway-c914%40inside-gateway-724c.iam.gserviceaccount.com&Signature=Yy3xZLRyo95oRIVfNWz3J55Cs8YfiRinx0CCY%2BVQtm3PcU%2B2u2eHiSF8yIzO7sRWaHdZ9r6t8j964fS2J3mrbQOvUn68yrW4mVv1%2FQSr1J0kgQ%2B2fIq8JoHw%2BTlwe%2Fbt%2FufKwAq1Y2Kvcsi%2FKO%2BIMyqL8KwwmmcC%2F5oetCfnYg%2BJq2jty01ULuuG6UWvsxiSVjfNNRnOTqQBQ4Ws6r62YoK0xC5A2GrNnACfN4R5%2BKbv4VXoKLKYQ0pGZF3MPHFcbJW4y59XOmIFJP%2F00Xjw8SreELGtk0iCQoIMxU8pEEZQALAIpesTquKGzNqqAgL5RNc46sh6%2BjtNbrwBnhM1vQ%3D%3D"
    }
}
```
A resposta do campo `public_url` deverá ser enviado no endpoint de [enviar os dados de um usuário](/docs/referencia-da-api/kyc/enviar-dados-do-usuario/).

O campo `url` deverá ser usado no endpoint para enviar de fato a imagem, no endpoint [enviar fotos](/docs/referencia-da-api/kyc/enviar-fotos/). Esse campo contém as _Query Params_ desse endpoint.


Próximo passo:

#### [Enviar fotos](/docs/referencia-da-api/kyc/enviar-fotos/).