---
title: "Data e Hora"
linkTitle: "Data e Hora"
date: 2020-05-05T18:32:12-03:00
lastmod: 2020-09-21T18:00:00-03:00
weight: 3
description: >

---

---

<br>

Representação de datas e horários.

1. Todas as datas com horário seguem o padrão [ISO8601 Extended Format](https://pt.wikipedia.org/wiki/ISO_8601), em [UTC](https://pt.wikipedia.org/wiki/Tempo_Universal_Coordenado) com anotação do _offset_. Ex: `2018-11-06T22:10:00Z`
2. Todas as datas sem horário estão no mesmo padrão. Ex: `2018-11-06`

<br>

Para evitar problemas, sempre mandamos as datas em [UTC](https://pt.wikipedia.org/wiki/Tempo_Universal_Coordenado) e anotamos essa informação na string codificada.

<br>

{{% pageinfo %}}
[UTC](https://pt.wikipedia.org/wiki/Tempo_Universal_Coordenado) (Coordinated Universal Time), como o próprio nome diz, é coordenado internacionalmente. O horário de Brasília é atrasado 3 horas em relação a esse horário. Tenha isso em mente sempre que for gerar um token ou fazer algum agendamento!
{{% /pageinfo %}}

