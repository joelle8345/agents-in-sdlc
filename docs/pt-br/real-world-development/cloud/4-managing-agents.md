---
title: "Exercício 4 - Monitoramento e gerenciamento de agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lição anterior: Agentes personalizados][previous-lesson] |
|:--|

Nos últimos exercícios, você pediu ao agente de nuvem do Copilot que realizasse três tarefas diferentes para melhorar a experiência do usuário e adicionar funcionalidades. Embora o agente de nuvem trabalhe de forma assíncrona e autônoma, ainda é importante monitorar essas tarefas.

Há várias ferramentas para gerenciar tarefas atribuídas ao agente de nuvem, incluindo a [página de agentes][agents-page] no GitHub.com. Nesse centro de controle, você pode ver todas as tarefas de agentes com pull requests (PRs) abertos. Também pode explorar as operações realizadas e orientar uma sessão em andamento.

Nesta lição, você vai:

- explorar a página de agentes para monitorar as tarefas do agente de nuvem;
- orientar uma sessão em andamento para solicitar funcionalidades adicionais.

## Cenário

Depois de atribuir ao agente a criação de um modo de alto contraste, a equipe percebeu que também seria um bom momento para adicionar um modo claro. Como o trabalho já incluía atualizações de estilo do site e a criação de opções para alternar entre modos, pareceu lógico incluir essa funcionalidade. Você vai orientar o agente para garantir que ele adicione o modo claro junto com o modo de alto contraste.

## Revise as tarefas do agente de nuvem do Copilot

Vamos verificar o status atual de todas as tarefas atribuídas ao agente de nuvem do Copilot.

1. Acesse a [página de agentes do Copilot](https://github.com/copilot/agents).
2. Observe a lista de tarefas nos painéis principal e esquerdo. Você deverá ver as tarefas atribuídas ao Copilot, incluindo:
    - atualização da documentação da base de código;
    - geração de APIs para modificar jogos;
    - adição de um modo de alto contraste ao site.
3. Selecione uma das tarefas em andamento. Revise as operações que o Copilot realizou. Elas podem incluir:
    - clonar o código do repositório;
    - criar o ambiente de trabalho do Copilot;
    - configurar servidores MCP;
    - executar várias etapas para concluir a tarefa atribuída.

> [!NOTE]
> As etapas exibidas variam de acordo com o estado do trabalho do Copilot e a abordagem usada.

4. Observe também o painel de pull request exibido à direita. Nele, você pode acompanhar o PR e os arquivos alterados.

## Oriente o agente de nuvem

Agora que você viu as tarefas ativas, vamos pedir ao Copilot que inclua a opção de modo claro enquanto trabalha no modo de alto contraste.

1. Selecione a sessão referente à criação do modo de alto contraste. O título exato varia de acordo com o nome usado pelo Copilot e o estado atual do trabalho.

    ![Sessão de acessibilidade no centro de controle](../../../_images/ex6-accessibility-session.png)

2. Acompanhe a sessão por alguns minutos, até que ela indique que a configuração foi concluída e o trabalho começou. Você verá mensagens semelhantes às exibidas abaixo.
3. Na caixa de diálogo **Steer active session while Copilot is working**, adicione este prompt:

    ```plaintext
    While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
    ```

    ![Captura de tela da tarefa do agente de nuvem na página de agentes, com a caixa de diálogo Steer active session while Copilot is working destacada](../../../_images/ex6-steer-cloud-agent-task.png)

4. Pressione <kbd>Enter</kbd> para enviar o prompt.
5. Observe como o Copilot confirma o recebimento do prompt e o inclui no fluxo de trabalho.

## Deixe o Copilot trabalhar

Como antes, o Copilot começará a trabalhar na tarefa atualizada. Ele incorporará a nova solicitação ao fluxo depois de concluir a etapa que estava executando quando você enviou a mensagem.

Isso levará alguns minutos, então aproveite para fazer uma pausa e refletir sobre o que aprendeu e explorou até aqui.

## Resumo e próximas etapas

Nesta lição, você explorou a página de agentes do Copilot, o centro de controle para monitorar e orientar as tarefas do agente de nuvem do GitHub Copilot. Você pode acompanhar todas as tarefas ativas e concluídas, revisar o trabalho e até redirecionar tarefas em andamento para ajustar o escopo ou fornecer orientações adicionais.

Você explorou os seguintes conceitos:

- explorar o centro de controle e a página de agentes para monitorar as tarefas do agente de nuvem;
- redirecionar uma sessão em andamento para solicitar funcionalidades adicionais.

Enquanto o Copilot conclui o trabalho nos recursos de acessibilidade, vamos [iterar sobre os pull requests criados por ele][next-lesson].

## Recursos

- [Página de agentes do Copilot][agents-page]
- [Sobre agentes personalizados][custom-agents]

---

| [← Lição anterior: Agentes personalizados][previous-lesson] | [Próxima lição: Iteração sobre o trabalho do Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
