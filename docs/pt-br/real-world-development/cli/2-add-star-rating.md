---
title: "Lição 2 - Adicione avaliações por estrelas: uma vitória rápida"
description: "Use o Copilot CLI para fazer uma pequena alteração nos cards dos jogos, revise o diff em um navegador encaminhado e faça o merge do primeiro pull request."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Agora que você instalou o Copilot CLI e iniciou uma conversa, chegou a hora de fazer sua primeira alteração no projeto. Ela será pequena: os dados dos jogos já incluem uma avaliação por estrelas, mas os cards da página inicial ainda não a mostram. Você pedirá ao agente que a exiba, revisará a alteração e fará o merge do primeiro pull request.

Nesta lição, você vai:

- iniciar uma conversa focada do Copilot em uma branch de recurso;
- pedir ao agente que faça uma pequena alteração no projeto;
- revisar a alteração com `/diff`;
- executar o aplicativo para confirmar a mudança em um navegador encaminhado;
- abrir e fazer merge do primeiro pull request.

## Cenário

Cada jogo da Tailspin Toys pode ter uma avaliação por estrelas, que já aparece na página de detalhes. Os cards da página inicial mostram apenas o título, a categoria, a editora e a descrição. Como aquecimento, você pedirá ao agente que exiba a avaliação existente em cada card — uma alteração pequena e independente, ideal para sua primeira sessão.

## Anatomia de uma conversa

Uma **conversa** é o espaço onde você trabalha com o Copilot CLI em uma tarefa. Diferentemente do aplicativo Copilot, uma conversa normal da CLI usa o repositório e a branch atualmente selecionados no terminal, em vez de criar uma worktree dedicada. As conversas salvas permitem retomar o diálogo mais tarde, enquanto os arquivos e a branch continuam no disco como estado comum do Git.

Em uma conversa, você verá três elementos: seus prompts e as respostas do agente; a atividade das ferramentas usadas pelo agente para explorar e editar arquivos; e as alterações que você pode inspecionar com `/diff`.

## Inicie uma conversa e solicite a alteração

Vamos iniciar uma nova conversa para implementar o recurso.

1. Volte ao Codespace.
2. Se o terminal não estiver aberto, pressione <kbd>Control</kbd>+<kbd>`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
3. Se ainda não estiver em execução, inicie o Copilot com o seguinte comando:

   ```bash
   copilot --yolo
   ```

4. Confirme que uma nova sessão foi iniciada usando o comando slash `/new` e pressionando <kbd>Enter</kbd>.
5. Use este prompt para solicitar a alteração:

   ```plaintext
   Mostre a avaliação de cada jogo, `starRating` de 5, nos cards da página de listagem. Se a avaliação for null, mostre "No rating yet". Mantenha o layout dos cards, adicione testes e execute as verificações relevantes.
   ```

O Copilot explorará o projeto, localizará os arquivos usados para exibir os detalhes dos jogos e criará o código necessário. Você acabou de adicionar um recurso com o Copilot CLI.

## Revise o diff

Todas as alterações geradas por IA devem ser revisadas antes do merge, mesmo as pequenas. Vamos examinar as mudanças diretamente no Copilot CLI.

1. Digite `/diff` e inspecione todos os arquivos alterados.
2. Confirme que o card do jogo mostra a avaliação numérica quando ela existe e `No rating yet` quando `starRating` é `null`.
3. Confirme que os testes cobrem os dois estados.
4. Revise os resultados das verificações executadas pelo Copilot e peça que corrija qualquer falha.
5. Quando terminar a revisão, pressione <kbd>Esc</kbd> para sair da tela do diff.

> [!NOTE]
> Como todas as ferramentas de IA generativa, o Copilot é probabilístico, não determinístico, então o código exato pode variar. Revise o comportamento em vez de esperar uma implementação idêntica.

## Verifique as alterações

Não basta ler o código e presumir que funciona. Vamos pedir ao Copilot que inicie o site para examinarmos a interface atualizada no navegador encaminhado pelo Codespaces.

1. Peça ao Copilot que inicie o aplicativo:

   ```plaintext
   Inicie o aplicativo para que eu possa inspecionar no navegador a alteração das avaliações por estrelas. Informe a URL e deixe o servidor em execução.
   ```

2. Quando o Codespaces informar que a porta `4321` está disponível, selecione **Open in Browser**.
3. Confirme que os cards dos jogos exibem as avaliações em uma escala de cinco estrelas.
4. Volte ao Copilot e peça que pare o servidor que iniciou:

   ```plaintext
   Pare o servidor de desenvolvimento que você iniciou.
   ```

## Abra e faça merge do primeiro pull request

Você criou o recurso. Agora, crie um pull request (PR) para fazer merge do novo código no projeto.

1. Peça ao agente padrão que faça commit da alteração:

   ```plaintext
   Faça commit das alterações revisadas das avaliações por estrelas com uma mensagem de commit apropriada.
   ```

2. Digite `/pr create`. O Copilot CLI enviará o commit existente ao criar o PR e exibirá a URL do PR.
3. Abra o PR mantendo pressionada a tecla <kbd>Command</kbd> (Mac) ou <kbd>Ctrl</kbd> (Windows/Linux) e selecionando a URL exibida pelo Copilot CLI.
4. Revise os arquivos alterados e as verificações.
5. Quando estiver pronto, selecione **Merge pull request** e confirme o merge.
6. Volte ao Codespace e saia do Copilot CLI com `/exit`.
7. Atualize sua `main` local:

   ```bash
   git checkout main
   git pull
   ```

## Resumo e próximas etapas

Parabéns! Você entregou sua primeira alteração usando o GitHub Copilot CLI. Especificamente, você:

- iniciou uma conversa focada do Copilot em uma branch de recurso;
- orientou o agente a fazer uma pequena alteração nos cards dos jogos;
- revisou a mudança com `/diff`;
- executou o aplicativo para confirmar as avaliações por estrelas em um navegador encaminhado;
- abriu e fez merge do primeiro pull request.

Em seguida, você [começará pela issue de filtragem e usará os modos Plan e Autopilot][next-lesson] para desenvolver um recurso maior.

## Recursos

- [Sobre o GitHub Copilot CLI][about-copilot-cli]
- [Referência de comandos do Copilot CLI][cli-reference]

[previous-lesson]: ../1-install-copilot-cli/
[next-lesson]: ../3-agent-modes/
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
