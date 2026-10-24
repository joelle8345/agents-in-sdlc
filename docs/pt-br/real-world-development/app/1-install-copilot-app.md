---
title: "Lição 1 - Instale o aplicativo GitHub Copilot"
description: "Instale o aplicativo GitHub Copilot, conecte o repositório criado a partir do modelo, conheça o espaço de trabalho e experimente uma conversa rápida."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

O **[aplicativo GitHub Copilot][about-copilot-app]** é um aplicativo para desktop voltado ao desenvolvimento agêntico. Ele é baseado no GitHub Copilot CLI e integra-se nativamente ao GitHub, então seus repositórios, branches e pipelines de integração contínua (CI) funcionam imediatamente. O aplicativo foi desenvolvido para fluxos de trabalho em que você orienta vários agentes em paralelo — cada um em seu próprio espaço de trabalho isolado — em vez de fazer todo o trabalho sozinho, além de automatizar tarefas repetitivas. Com o Node.js instalado e a cópia do projeto pronta, agora você instalará o aplicativo e conectará o repositório.

Nesta lição, você vai:

- instalar o aplicativo GitHub Copilot e entrar na sua conta;
- adicionar o projeto ao aplicativo a partir do repositório do GitHub;
- conhecer o espaço de trabalho, incluindo o backlog criado pelo modelo;
- experimentar uma conversa rápida para conhecer o próprio aplicativo.

## Cenário

Sua equipe está adotando agentes de IA para avançar em um backlog crescente. O aplicativo Copilot oferece um lugar para orientar esse trabalho: escolher issues, executar agentes, revisar alterações e fazer merge de pull requests. Nesta lição, você instalará e conectará o aplicativo e aprenderá a iniciar uma conversa sobre o projeto.

> [!NOTE]
> É necessário ter um plano qualificado do Copilot: Copilot Free, Copilot Student ou qualquer plano pago (Pro, Pro+, Business ou Enterprise). Se você usa o Copilot Business ou o Copilot Enterprise, o administrador precisa manter habilitada a política **GitHub Copilot app**.

## Instale e configure o aplicativo GitHub Copilot

O primeiro passo para usar o aplicativo GitHub Copilot é instalá-lo. Há versões para Windows, macOS e Linux. Vamos instalar o aplicativo, autenticar e adicionar o repositório Tailspin Toys.

1. Em um navegador, abra a [página inicial do aplicativo GitHub Copilot][download-app].
2. Baixe o aplicativo para sua plataforma e instale-o seguindo as instruções da página.
3. Abra o aplicativo depois da instalação.
4. Selecione **Sign in to GitHub** e siga as instruções para autenticar. Se você usa o GitHub Enterprise Cloud com residência de dados, escolha **Use GitHub Enterprise** e informe o nome do host `*.ghe.com` quando solicitado. O GitHub Enterprise Server não é compatível.
5. Se o processo inicial permitir selecionar um repositório, selecione o repositório Tailspin Toys que você criou a partir do modelo. Você também pode pular essa seleção e adicionar o projeto depois.
6. Escolha um tema quando solicitado e conclua a configuração inicial.
7. Procure o repositório em **Sessions** na barra lateral. Se ele já estiver listado, não é necessário adicioná-lo novamente.
8. Se o repositório ainda não estiver conectado, selecione **+** ao lado de **Sessions** para criar uma sessão e, em seguida, selecione **Add GitHub repository**. Use o nome do proprietário e do repositório anotado na lição de pré-requisitos.
9. Confirme que o repositório aparece na barra lateral. No layout usado aqui, pastas de repositórios como `tailspin-toys` ficam agrupadas em **Sessions**, com sessões individuais abaixo de cada repositório.

## Conheça o espaço de trabalho

Com o projeto conectado, conheça a interface. O aplicativo organiza o trabalho em algumas áreas na barra lateral:

- **New** — inicie uma nova sessão de chat com o Copilot.
- **Pull requests** — acesse seus pull requests pela integração nativa com o GitHub. Você pode navegar pelos PRs, filtrá-los, verificar o status de CI e revisá-los sem sair do aplicativo.
- **Issues** — acesse suas issues da mesma maneira. Você pode navegar pelas issues, filtrá-las e iniciar uma sessão a partir de uma issue.
- **Automations** — tarefas de agente salvas para execução agendada ou sob demanda. Elas são úteis para gerenciar listas de tarefas, fazer manutenção regular do projeto ou delegar outras tarefas repetitivas. O resumo apresenta esse recurso como próxima etapa, não como outro exercício do workshop.
- **Customize** — adicione recursos e funções ao aplicativo Copilot por meio de servidores MCP, plugins, skills e outros componentes. Você usará esta opção para configurar o Playwright MCP.
- **Chats** — conversas rápidas para perguntas e brainstorming que não precisam de uma branch ou de um espaço de trabalho próprio. Essa seção aparece depois da primeira conversa. Se ela não estiver visível, selecione **+** ao lado de **Sessions** para iniciar uma conversa.
- **Sessions** — agrupa as pastas dos repositórios e as sessões dos agentes. Selecione o nome de um repositório, como `tailspin-toys`, para abrir a visualização dele, ou selecione uma sessão abaixo para voltar à conversa. Cada sessão é executada em um espaço de trabalho isolado para que você possa executar várias ao mesmo tempo sem conflito entre as alterações. Você iniciará sua primeira sessão ao adicionar as avaliações por estrelas.

Ao longo do workshop, você explorará o espaço de trabalho.

> [!TIP]
> Em caso de dúvida, pergunte ao Copilot. Se você não souber como fazer algo ou quiser saber se é possível, o Copilot poderá ajudar.

### Localize o backlog predefinido

Quase todo projeto tem um backlog, e a Tailspin Toys não é diferente. Vamos explorar o backlog criado quando você criou o repositório a partir do modelo.

1. Em **Sessions** na barra lateral, selecione a pasta do repositório Tailspin Toys, não uma sessão individual abaixo dela. Em seguida, selecione **Issues** na navegação superior do repositório.
2. Localize estas issues pelo título, sem presumir quais são os números:

   - Allow users to filter games by category and publisher
   - Update our repository coding standards

3. Selecione uma issue para ler os detalhes. Cada issue também permite iniciar uma sessão de agente. Você começará pela issue de filtragem depois de fazer uma pequena alteração inicial.

> [!NOTE]
> As listas de **Issues** e **Pull requests** são filtradas automaticamente para mostrar somente itens dos repositórios adicionados ao aplicativo Copilot. Para ver itens de trabalho de outros repositórios, adicione-os ao aplicativo.

## Experimente uma conversa rápida

Uma ótima maneira de conhecer o aplicativo é usá-lo para aprender sobre o *próprio aplicativo* — e uma **conversa rápida** é a ferramenta certa para isso. As conversas rápidas permitem fazer uma pergunta ou trocar ideias sem criar uma branch ou worktree, então são ideais para perguntas breves e descartáveis, sem precisar iniciar uma sessão.

1. Na barra lateral, selecione **+** ao lado de **Chats** para abrir uma nova conversa. Se **Chats** ainda não estiver visível, selecione **+** ao lado de **Sessions** para iniciar a primeira conversa; **Chats** aparecerá depois disso.
2. Pergunte ao aplicativo como funcionam as sessões:

   ```plaintext
   Como o aplicativo GitHub Copilot usa worktrees?
   ```

3. Leia a resposta na visualização da conversa. Você verá que cada sessão é executada em uma worktree Git isolada, o que permite executar vários agentes em paralelo sem conflitos entre as alterações. Você pode continuar a conversa ou iniciar outra quando quiser.

## Resumo e próximas etapas

Parabéns! Você instalou o aplicativo GitHub Copilot, conectou o projeto e explorou o espaço de trabalho. Você aprendeu a:

- instalar o aplicativo e entrar na sua conta do GitHub;
- adicionar um projeto a partir do repositório correspondente no GitHub;
- conhecer o espaço de trabalho e localizar o backlog predefinido em **Issues**;
- usar uma conversa rápida para fazer uma pergunta breve.

Em seguida, você [iniciará sua primeira sessão de agente][next-lesson] e a usará para exibir avaliações por estrelas nos cards dos jogos.

## Recursos

- [Sobre o aplicativo GitHub Copilot][about-copilot-app]
- [Introdução ao aplicativo GitHub Copilot][getting-started]
- [Trabalho com sessões de agente no aplicativo GitHub Copilot][agent-sessions]

[next-lesson]: ../2-add-star-rating/
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
[getting-started]: https://docs.github.com/copilot/how-tos/github-copilot-app/getting-started
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
[download-app]: https://gh.io/app
