---
title: "Mensagens De Erro"
linkTitle: "Mensagens De Erro"
date: 2021-07-12T11:20:05-03:00
lastmod: 2021-07-12T11:20:05-03:00
weight: 6
description: >

---

<br>

Nossos endpoints seguem um padrão de mensagens. Toda mensagem de erro, por exemplo, seguirá o modelo "srn:error:xxx\" e um [código HTTP](/docs/referencia-da-api/padroes-da-api/codigos-de-resposta/) apropriado para a falha.

Exemplo:

```JSON
{
    "type": "srn:error:target_account_not_found"
}
```
<br>

Alguns endpoints têm uma resposta mais completa, entregando a mensagem de erro mencionada e mais detalhes.

Exemplo:

```JSON
{
    "errors": [
        {
            "error": "is invalid",
                "path": [
                    "tax_id"
                    ]
        }
    ],
    "type": "srn:error:bad_request"
}
```
