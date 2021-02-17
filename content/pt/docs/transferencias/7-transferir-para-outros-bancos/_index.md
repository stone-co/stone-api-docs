---
title: "Transferir para Outros Bancos"
slug: "transferir-para-outros-bancos"
excerpt: "Faz transferências monetárias para outra instituição (TED). Não é permitido realizar uma TED de uma conta Stone para outra conta Stone.\n\nCaso a transferência seja criada em um dia não útil ou fora do horário de funcionamento de TEDs, a transferência será agendada automaticamente para o dia seguinte. Nesse caso seu status será `DELAYED_TO_NEXT_BUSINESS_DAY`, como também a flag `delayed_to_next_business_day = true`. O campo `scheduled_to_effective` conterá a data para a qual a TED foi agendada.\n\nA transferência também pode ser agendada através do campo `scheduled_to`. A data usada no campo `scheduled_to` deve estar entre a data `next_available_execution_date` e a data limite retornada no campo `execution_limit_date` da [API de calendário de agendamento](https://docs.openbank.stone.com.br/reference#calend%C3%A1rio-de-agendamento) chamada com o parâmetro `operation_type=external_transfer`. Caso a data escolhida seja menor do que `next_available_execution_date`, a transferência será executada imediatamente. Caso a data seja maior que `execution_limit_date` será retornado um erro 422.\n\nCaso a data escolhida não seja um dia útil, a transferência será automaticamente agendada para o próximo dia útil depois do escolhido. O dia útil requisitado (que veio na request) e o efetivo (em que de fato o agendamento vai ocorrer) são representados pelos campos `scheduled_to_requested` e `scheduled_to_effective`.\n\nA data usada no campo `scheduled_to` deve obedecer a data limite retornada na [API de calendario de agendamento](https://docs.openbank.stone.com.br/reference#calend%C3%A1rio-de-agendamento). Caso contrário, será retornado um erro 422 na criação."
hidden: false
createdAt: "2019-04-01T19:28:14.644Z"
updatedAt: "2020-07-02T21:56:08.155Z"
---
[block:callout]
{
  "type": "info",
  "body": "O corpo da requisição deve conter todos os dados da transferência.\nObserve que os \"0\"s que prefixam o `account_code` são removidos. Por exemplo, “00012345” é armazenado como “12345” e vai ser retornado assim nas APIs de consulta.\nEssa transformação é aplicada pela API antes dos dados serem armazenados.",
  "title": "Request Body"
}
[/block]

[block:callout]
{
  "type": "warning",
  "title": "Tipos de conta ( target.account.account_type )",
  "body": "Através deste campo, é possível enviar o tipo de conta destino. Os valores aceitos são:\n“CC” - Conta Corrente\n“CD” - Conta de Depósito\n“CG” - Conta garantida\n“CI” - Conta de Investimento\n“PG” - Conta de Pagamento\n“PP” - Poupança\n\nEste campo possui regras especiais para utilização:\nSe o tipo de conta for PG, a agência (branch_code) é removida.\nSe o tipo de conta for CC ou nulo, mas o número da conta (account_code) possuir mais de 13 dígitos, o tipo de conta é convertido para PG e a agência (branch_code) é removida.\nSe o tipo de conta for CC ou nulo, mas a agência (branch_code) não vier preenchida, o tipo de conta é convertido para PG.\nSe o tipo de conta é nulo e não cai nos casos acima, o tipo de conta usado é CC."
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "Sobre o objeto target",
  "body": "Quando a conta alvo pertence a uma pessoa jurídica, usar `cnpj` ao invés de `cpf` no objeto `target.entity`."
}
[/block]

[block:callout]
{
  "type": "warning",
  "body": "Em _sandbox_, a transferência externa está disponível de 6:30 às 17:23 todos os dias. Em produção, só está habilitada em dias úteis de 6:30 até 17:23. Após este horário a transferência será agendada para o próximo dia útil.",
  "title": "Agendamento"
}
[/block]