---
title: "Consultar devolução de Pix"
linkTitle: "Consultar devolução de Pix"
date: 2021-06-16T15:17:00-03:00
lastmod: 2021-09-19T09:09:00-03:00
weight: 9
description: >
  
---

Através desse endpoint será possível exibir os detalhes de uma devolução realizada para uma transferência Pix. Os status possíveis para a devolução poderão ser:

* `EM_PROCESSAMENTO` - a devolução ainda está em processamento
* `DEVOLVIDO` - concluído com sucesso 
* `NAO_REALIZADO` - a devolução foi rejeitada


```
GET https://sandbox-api.openbank.stone.com.br/api/v1/pix/{end_to_end_id}/devolucao/{id}
```
<br>

##### **HEADERS**
---

**authorization*** `string`
<br> Bearer token de autenticação.

**x-stone-account-id*** `string`
<br> Necessário para permissionamento.


##### **PATH PARAMS**
---

**e2eid*** `string`
<br>

**id*** `uuid`
<br>

##### **Response**
---

```
200 OK
```

```json
{
  "endToEndId": "E12345678202009091221abcdef12345",
  "txid": "cd1fe328c875481285a6f233ae41b662",
  "valor": "100.00",
  "horario": "2020-09-10T13:03:33.902Z",
  "infoPagador": "Reforma da casa",
  "devolucoes": [
    {
      "id": "000AAA111",
      "rtrId": "D12345678202009091000abcde123456",
      "valor": "11.00",
      "horario": {
        "solicitacao": "2020-09-10T13:03:33.902Z"
      },
      "status": "EM_PROCESSAMENTO"
    }
  ]
}
```

<br>

```
400 Bad Request
```

```json
{
  "type": "https://pix.bcb.gov.br/api/v2/error/PixConsultaInvalida",
  "title": "Consulta Pix Inválida",
  "status": 400,
  "detail": "Os parâmetros de consulta à lista de pix recebidos não respeitam o schema ou não fazem sentido semanticamente."
}
```

<br>

```
403 Forbidden
```

```json
{
  "type": "https://pix.bcb.gov.br/api/v2/error/AcessoNegado",
  "title": "Acesso Negado",
  "status": 403,
  "detail": "Requisição de participante autenticado que viola alguma regra de autorização."
}
```
