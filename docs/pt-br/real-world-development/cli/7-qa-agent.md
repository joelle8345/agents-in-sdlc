---
title: "Lição 7 - Crie e use um agente de garantia de qualidade (QA)"
description: "Crie um agente personalizado de garantia de qualidade (QA) que combine os requisitos da issue, a skill quality-checks e o Playwright MCP."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Você usou a skill `quality-checks` para executar verificações automatizadas e o Playwright MCP para observar a experiência de filtragem no navegador. Agora, combinará esses recursos em um agente personalizado com um processo de QA bem definido.

Nesta lição, você vai:

- explorar como um agente personalizado trabalha com instruções, skills e ferramentas MCP;
- criar e inspecionar um perfil reutilizável de garantia de qualidade;
- selecionar o agente de QA e revisar as constatações em relação à issue de filtragem.

## Cenário

A Tailspin Toys quer uma revisão consistente dos requisitos, da qualidade do código, das verificações automatizadas, da cobertura de testes e do comportamento no navegador antes de abrir um pull request (PR). Um agente personalizado pode coordenar esse processo de QA e fornecer um relatório reutilizável.

## O que é um agente personalizado?

Um agente personalizado é uma versão especializada do Copilot definida em um perfil Markdown. O perfil descreve a finalidade, as instruções e as ferramentas disponíveis para o agente. Neste workshop, você definirá uma função de QA em `.github/agents/qa.agent.md` e a selecionará no Copilot CLI.

As personalizações usadas até agora têm funções diferentes. As instruções do repositório descrevem os padrões da equipe. A skill `quality-checks` agrupa verificações repetíveis. O Playwright MCP fornece ferramentas de navegador. O perfil de QA orienta o Copilot a usar esses recursos para avaliar requisitos e relatar resultados. O perfil não substitui esses recursos nem exige outra conversa.

## Crie o perfil de QA

Antes de abrir o PR do recurso, peça ao Copilot que crie um perfil de QA reutilizável. O perfil definirá as verificações e os limites que o QA deve respeitar.

1. Volte ao Codespace e confirme que a conversa de filtragem está no modo Interactive.
2. Peça ao agente padrão que crie o novo agente personalizado:

   ```plaintext
   Crie um agente personalizado chamado QA em .github/agents/qa.agent.md. Ele deve verificar recursos em relação às issues e aos requisitos acordados, seguir as instruções do repositório, executar a skill quality-checks, usar o Playwright MCP para verificar o comportamento e adicionar testes quando a cobertura estiver incompleta.

   Peça que informe cada requisito como aprovado, reprovado ou bloqueado, com evidências. O agente deve pedir autorização antes de alterar o código da implementação e não deve fazer commit nem abrir pull requests.

   Crie apenas o perfil por enquanto para que eu possa revisá-lo.
   ```

## Inspecione o perfil

Antes de usar o agente, revise o perfil para confirmar que o Copilot registrou o fluxo de trabalho e os limites pretendidos. Assim, você evita que um perfil incompleto ou amplo demais altere o recurso quando o objetivo é apenas verificá-lo.

1. Digite `/diff` e abra `.github/agents/qa.agent.md`.
2. Leia o frontmatter. `description` é obrigatório; `name` é opcional, mas ajuda a definir um nome de exibição claro para o agente.
3. Leia as instruções do perfil e confirme que o QA começa pelos requisitos, segue as instruções do repositório, executa a skill `quality-checks` e usa o Playwright MCP.
4. Confirme que o QA relata evidências, pede autorização antes de alterar o código da implementação e não faz commits nem abre pull requests.
5. Se o perfil gerado não incluir nenhuma dessas responsabilidades ou limites, peça ao agente padrão que o revise antes de continuar.

## Execute o QA em relação à issue

O Copilot CLI carrega os agentes do projeto quando uma conversa é iniciada. Retome a mesma conversa de filtragem depois de criar o perfil e selecione o agente de QA para que ele possa usar a issue e as decisões de planejamento já disponíveis no contexto.

1. Ative o agente usando este prompt:

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> Como o agente acabou de ser criado, talvez ele não apareça na lista de agentes disponíveis. Ainda assim, o comando acima o ativará.

2. Use este prompt para pedir ao agente de QA que revise o recurso:

   ```plaintext
   Revise o recurso de filtragem em relação à issue e às decisões do nosso plano. Ele está pronto para um PR?
   ```

3. O agente de QA começará a trabalhar.
4. Quando terminar, leia o relatório.

## Resumo e próximas etapas

Você adicionou uma função especializada reutilizável ao fluxo e revisou o resultado. Nesta lição, você:

- explorou como um agente personalizado trabalha com instruções, skills e ferramentas MCP;
- criou e inspecionou um perfil reutilizável de garantia de qualidade;
- selecionou o agente de QA e revisou as constatações em relação à issue de filtragem.

Agora, a implementação, a atualização da skill, o perfil de QA, os testes e o relatório de verificação estão prontos para revisão. Em seguida, você [reunirá tudo em um PR do recurso e usará o Agent Merge][next-lesson].

## Recursos

- [Criação de agentes personalizados para o Copilot CLI][create-agents]
- [Configuração de agentes personalizados][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
