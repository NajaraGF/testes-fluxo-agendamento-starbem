# Feature: Agendamento de Consultas no App Starbem

## Background (Contexto)

```gherkin
Given que o usuário titular possui uma assinatura ativa da Starbem
And que cada dependente também possui o mesmo direito (2 consultas mensais, 1 por semana)
And que o atendimento é realizado via WhatsApp
And que o usuário tem acesso às telas demonstradas nos prints anexos
```

## Cenário 1: Agendar a primeira consulta do mês (Titular)

```gherkin
Given que o usuário (titular) está logado no aplicativo na Tela Inicial
And que ele não tem nenhuma consulta agendada neste mês
When o usuário seleciona “Agendar Consulta”
And escolhe a especialidade "Ginecologista/Obstetra"
And clica no botão "Avançar"
And seleciona uma data disponível para o agendamento
And escolhe um profissional de saúde
And escolhe um horário
And clica no botão "Avançar"
And o usuário informa o motivo da consulta
And clica no botão "Avançar"
And confirma todas as informações de agendamento na tela de "Confirmação"
Then o sistema deve registrar a primeira consulta do mês para o titular
And deve exibir "Consulta Agendada"
And o usuário poderá enviar seus exames para o médico antes da consulta ao clicar nos botões "Enviar depois" ou "Enviar agora"
And o usuário visualiza um modal com o lembrete de que poderá visualizar os detalhes da consulta na tela principal do app
```

## Cenário 2: Agendar a segunda consulta do mês (Titular)

```gherkin
Given que o usuário (titular) está logado no aplicativo na Tela Inicial
And que ele já tem 1 consulta agendada neste mês
And a nova consulta será marcada em uma semana diferente da primeira
When o usuário seleciona “Agendar Consulta”
And escolhe a especialidade "Clínico Geral"
And clica no botão "Avançar"
And seleciona uma data disponível para o agendamento em outra semana
And escolhe um profissional de saúde
And escolhe um horário
And clica no botão "Avançar"
And o usuário informa o motivo da consulta
And clica no botão "Avançar"
And confirma todas as informações na tela de "Confirmação"
Then o sistema deve registrar a segunda consulta do mês para o titular
And deve exibir "Consulta Agendada"
And o usuário poderá enviar seus exames antes da consulta ao clicar nos botões "Enviar depois" e "Enviar agora"
And o usuário visualiza um modal com o lembrete de que poderá visualizar os detalhes da consulta na tela principal do app
```

## Cenário 3: Impedir agendamento da terceira consulta no mesmo mês (Titular)

```gherkin
Given que o usuário (titular) está logado no aplicativo na Tela Inicial
And que ele já possui 2 consultas agendadas neste mês
When o usuário seleciona “Agendar Consulta”
And tenta repetir o fluxo de escolha de especialidade, data, horário, profissional e motivo
And tenta confirmar o agendamento na tela de "Confirmação"
Then o sistema deve bloquear a tentativa de agendar a terceira consulta no mês
And deve exibir a mensagem de erro "Limite mensal atingido"
And não deve permitir que o usuário avance para o envio de exames
```

## Cenário 4: Impedir agendamento de duas consultas na mesma semana (Titular)

```gherkin
Given que o usuário (titular) está logado no aplicativo na Tela Inicial
And que ele já possui uma consulta agendada nessa mesma semana
When o usuário seleciona “Agendar Consulta”
And tenta marcar outra consulta na mesma semana (escolhendo data, horário, profissional)
And clica no botão "Avançar" até chegar na tela de "Confirmação"
Then o sistema deve bloquear a tentativa de agendar a segunda consulta na mesma semana
And deve exibir a mensagem de erro "Apenas 1 consulta por semana"
And não deve permitir que o usuário conclua o agendamento
```

## Cenário 5: Agendar a primeira consulta do mês para um dependente

```gherkin
Given que o usuário (titular) está logado no aplicativo na Tela Inicial
And que existe pelo menos um dependente cadastrado
And o dependente não tem nenhuma consulta agendada neste mês
When o titular seleciona “Agendar Consulta”
And altera o perfil para o dependente na tela de seleção de dependentes
And escolhe a especialidade desejada
And clica em "Avançar"
And seleciona a data e horário disponíveis
And escolhe o profissional de saúde
And clica em "Avançar"
And informa o motivo da consulta para o dependente
And clica em "Avançar"
And confirma todas as informações na tela de "Confirmação"
Then o sistema deve registrar a primeira consulta do mês para o dependente
And deve exibir "Consulta Agendada"
And o titular (ou dependente) poderá enviar exames antes da consulta ao clicar nos botões "Enviar depois" e "Enviar agora"
And o usuário visualiza um modal com o lembrete de que poderá visualizar os detalhes da consulta na tela principal do app
```

## Cenário 6: Agendar a segunda consulta do mês para um dependente

```gherkin
Given que o usuário (titular) está logado no aplicativo na Tela Inicial
And que o dependente já possui 1 consulta agendada neste mês
And a nova consulta será marcada em uma semana diferente da primeira
When o titular seleciona “Agendar Consulta”
And altera o perfil para o dependente na tela de seleção de dependentes
And escolhe a especialidade desejada
And clica no botão "Avançar"
And seleciona uma data disponível para o agendamento em outra semana
And escolhe um profissional de saúde
And escolhe um horário
And clica no botão "Avançar"
And informa o motivo da consulta
And clica no botão "Avançar"
And confirma todas as informações de agendamento na tela de "Confirmação"
Then o sistema deve registrar a segunda consulta do mês para o dependente
And deve exibir "Consulta Agendada"
And o titular (ou dependente) poderá enviar exames antes da consulta ao clicar nos botões "Enviar depois" ou "Enviar agora"
And o usuário visualiza um modal com o lembrete de que poderá visualizar os detalhes da consulta na tela principal do app
```

## Cenário 7: Impedir terceira consulta no mês para um dependente

```gherkin
Given que o usuário (titular) está logado no aplicativo na Tela Inicial
And o dependente já possui 2 consultas agendadas neste mês
When o titular seleciona “Agendar Consulta”
And escolhe o perfil do dependente
And tenta repetir o fluxo de escolha de especialidade, data, horário, profissional
And tenta confirmar a nova consulta na tela de "Confirmação"
Then o sistema deve bloquear a terceira consulta do dependente no mesmo mês
And deve exibir a mensagem "Limite mensal atingido"
And não deve permitir a finalização do agendamento
```

## Cenário 8: Impedir duas consultas na mesma semana para um dependente

```gherkin
Given que o usuário (titular) está logado no aplicativo na Tela Inicial
And o dependente já possui 1 consulta marcada naquela semana
When o titular seleciona “Agendar Consulta”
And seleciona o perfil do dependente
And escolhe o mesmo intervalo de semana (data, horário e profissional)
And tenta confirmar o agendamento na tela de "Confirmação"
Then o sistema deve bloquear a segunda consulta na mesma semana para o dependente
And deve exibir a mensagem "Apenas 1 consulta por semana"
And não deve permitir a finalização do agendamento
```

## Cenário 9: Verificar o recebimento da confirmação via WhatsApp

```gherkin
Given que o usuário (titular ou dependente) concluiu o agendamento com sucesso
When o sistema finaliza o processo de agendamento
Then deve ser exibida a mensagem "Consulta Agendada" no app
And deve enviar uma notificação de confirmação via WhatsApp
And a mensagem deve conter a especialidade, data e horário corretos
And o usuário visualiza um modal com o lembrete de que poderá visualizar os detalhes da consulta na tela principal do app
```

