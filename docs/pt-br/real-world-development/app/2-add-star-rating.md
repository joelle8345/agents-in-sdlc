---
title: "Lição 2 - Adicione avaliações por estrelas: uma vitória rápida"
description: "Inicie sua primeira sessão de agente no aplicativo GitHub Copilot, faça uma pequena alteração nos cards dos jogos e mescle-a no primeiro pull request."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

Agora que você explorou o espaço de trabalho e usou uma conversa rápida, chegou a hora de iniciar uma **sessão de agente** e fazer sua primeira alteração no projeto. Ela será pequena: os dados dos jogos já incluem uma avaliação por estrelas, mas os cards da página inicial ainda não a mostram. Você pedirá ao agente que a exiba, revisará a alteração e fará o merge do primeiro pull request.

Nesta lição, você vai:

- iniciar uma sessão de agente e conhecer sua estrutura;
- pedir ao agente que faça uma pequena alteração específica no projeto;
- revisar a alteração na visualização de diff do espaço de trabalho;
- executar o aplicativo localmente para confirmar a mudança no navegador;
- abrir e fazer merge do primeiro pull request.

## Cenário

Cada jogo da Tailspin Toys pode ter uma avaliação por estrelas, que já aparece na página de detalhes. Os cards da página inicial mostram apenas o título, a categoria, a editora e a descrição. Como aquecimento, você pedirá ao agente que exiba a avaliação existente em cada card — uma alteração pequena e independente, ideal para sua primeira sessão.

## Anatomia de uma sessão

Uma **sessão** é uma conversa com um agente executada em um espaço de trabalho isolado. Cada sessão tem uma **worktree e uma branch Git dedicadas**, o que permite executar várias sessões ao mesmo tempo — uma para adicionar um recurso e outra para corrigir um bug — sem que as alterações entrem em conflito. As sessões aparecem agrupadas por repositório na barra lateral; selecione uma para alternar para ela.

Em uma sessão, você verá três elementos: a **conversa** com o agente; a **atividade das ferramentas** usadas pelo agente para explorar e editar arquivos; e a lista de **arquivos alterados** com seus diffs.

## Inicie uma sessão e solicite a alteração

Vamos iniciar uma nova sessão para explorar o projeto e implementar o recurso. Durante a [configuração do aplicativo][prior-lesson], você adicionou o projeto a partir do repositório do GitHub. Agora, criaremos uma sessão para esse repositório e solicitaremos a alteração.

1. Volte ao aplicativo GitHub Copilot ou abra-o.
2. Selecione **+** na parte superior da barra lateral para iniciar uma sessão.
3. Selecione `tailspin-toys` como repositório.
4. Escolha uma **new working tree** e o modo **Interactive** abaixo da caixa de prompt. Use este prompt para solicitar a alteração:

    ```plaintext
    Mostre nos cards da página de listagem a avaliação `starRating` de cada jogo em uma escala de 5. Se a avaliação for `null`, mostre "No rating yet". Mantenha o layout dos cards, adicione testes e execute as verificações relevantes.
    ```

5. Pressione <kbd>Enter</kbd> para enviar o prompt ao Copilot.

O aplicativo Copilot começará criando uma nova worktree, uma cópia isolada do projeto. Em seguida, explorará o projeto e localizará os arquivos que precisam ser atualizados para adicionar o recurso. Depois, criará o código necessário. Você acabou de adicionar um novo recurso com o aplicativo Copilot.

## Revise o diff

Todas as alterações geradas por IA devem ser revisadas antes do merge, mesmo as pequenas. Vamos examinar as mudanças diretamente no aplicativo Copilot.

1. No canto superior direito do aplicativo, selecione **Toggle review panel**. No painel aberto, selecione **Changes** para ver os arquivos alterados e seus diffs.

    ![Barra de ferramentas superior do aplicativo GitHub Copilot com uma seta apontando para o botão Toggle review panel à direita de Create PR](../../../_images/app-2-review-panel.png)

2. Você deverá ver código adicionado a `GameCard.astro`, o arquivo principal usado para exibir os detalhes dos jogos. Deve ser semelhante ao seguinte: um pequeno bloco que mostra a avaliação quando ela existe e usa "No rating yet" quando `starRating` é `null`:

   ```astro
   {game.starRating !== null ? (
       <span class="text-xs font-medium px-2.5 py-0.5 rounded bg-amber-900/60 text-amber-300" data-testid="game-rating">
           ★ {game.starRating} / 5
       </span>
   ) : (
       <span class="text-xs font-medium text-slate-500" data-testid="game-rating-empty">
           No rating yet
       </span>
   )}
   ```

> [!NOTE]
> Como o Copilot, assim como todas as ferramentas de IA generativa, é probabilístico e não determinístico, o código exato pode variar. Ainda assim, deverá ser relativamente parecido.

## Verifique as alterações

Revise os resultados das verificações automatizadas do agente antes de abrir um navegador. Confirme que os testes cobrem um valor numérico de `starRating` e o estado alternativo `null`. Um pré-requisito ausente ou uma verificação ignorada não significa aprovação; revise qualquer solicitação de instalação antes de autorizá-la.

Não basta ler o código e presumir que funciona. Vamos pedir ao Copilot que abra o site para examinarmos a interface atualizada. Para isso, peça que inicie o site e o abra em um canvas de navegador.

> [!TIP]
> Um canvas é um widget interativo disponível no próprio aplicativo Copilot. Você explorará canvases personalizados e criará um mais adiante; por enquanto, usaremos o canvas de navegador integrado.

1. Use este prompt para pedir ao Copilot que inicie o aplicativo e abra a página no canvas de navegador:

    ```plaintext
    Inicie o aplicativo e abra-o no canvas de navegador.
    ```

2. Em alguns instantes, o aplicativo será iniciado e uma janela do navegador será aberta dentro do aplicativo Copilot.
3. Confirme que os cards dos jogos com avaliação mostram o valor em uma escala de cinco estrelas.
4. Quando terminar, peça ao Copilot que pare o servidor de desenvolvimento iniciado para esta sessão e feche o canvas:

    ```plaintext
    Pare o servidor de desenvolvimento e feche o canvas de navegador.
    ```

## Abra e faça merge do primeiro pull request

Você criou o recurso. Agora, crie um pull request (PR) para integrar o novo código à base existente.

1. Selecione **Create PR** no canto superior direito.
2. Se solicitado, selecione **Sign in with your browser** e siga as instruções para autenticar.
3. Se o Copilot explicar que a política do repositório exige uma issue correspondente antes de criar o PR, confirme que ele deve seguir esse processo.
4. O Copilot começará a criar o PR.
5. Selecione o balão **PR** logo acima do chat para abrir o PR no painel de revisão e consultá-lo. Revise o PR conforme necessário.
6. Quando estiver pronto, selecione **Ready to merge**.
7. Na nova janela de diálogo, selecione **Merge pull request** para fazer o merge.

## Resumo e próximas etapas

Parabéns! Você entregou sua primeira alteração usando o aplicativo GitHub Copilot. Especificamente, você:

- iniciou uma sessão de agente e conheceu sua estrutura;
- orientou o agente a fazer uma pequena alteração específica nos cards dos jogos;
- revisou a alteração na visualização de diff do espaço de trabalho;
- executou o aplicativo localmente para confirmar as avaliações por estrelas no navegador;
- abriu o primeiro PR, revisou as verificações e fez o merge explicitamente.

Em seguida, você [começará pela issue de filtragem e usará os modos Plan e Autopilot][next-lesson] para desenvolver um recurso maior.

## Recursos

- [Trabalho com sessões de agente no aplicativo GitHub Copilot][agent-sessions]
- [Sobre o aplicativo GitHub Copilot][about-copilot-app]
- [Gerenciamento de issues e pull requests no aplicativo GitHub Copilot][managing-issues-prs]

[prior-lesson]: ../1-install-copilot-app/#instale-e-configure-o-aplicativo-github-copilot
[next-lesson]: ../3-agent-modes/
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
[managing-issues-prs]: https://docs.github.com/copilot/how-tos/github-copilot-app/managing-issues-and-pull-requests
