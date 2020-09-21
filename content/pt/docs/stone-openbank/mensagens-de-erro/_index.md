---
title: "Mensagens De Erro"
linkTitle: "Mensagens De Erro"
date: 2020-05-01T18:34:12-03:00
lastmod: 2020-09-21T18:00:00-03:00
weight: 7
description: >

---

Nossos endpoints seguem um padrão de mensagens. Toda mensagem de erro, por exemplo, seguirá o modelo "srn:error:xxx\" e um [código HTTP](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) apropriado para a falha.

Por exemplo:

```text
{
    "type": "srn:error:target_account_not_found"
}
```

Alguns endpoints têm uma resposta mais completa, entregando a mensagem de erro mencionada e mais detalhes.

Por exemplo:

```text
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
