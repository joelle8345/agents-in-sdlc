---
title: "Exercício 5 - Monitoramento e gerenciamento de agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lição anterior: Agentes personalizados][previous-lesson] |
|:--|

No modo agente, o GitHub Copilot trabalha de forma autônoma: explora a base de código, propõe mudanças, edita arquivos e executa comandos. Como esse trabalho acontece em tempo real no seu computador, o Copilot Chat no VS Code mostra cada chamada de ferramenta e edição de arquivo. Você pode revisar cada diff no chat, aceitar ou rejeitar mudanças individuais e orientar a conversa com prompts adicionais para refinar ou ampliar o trabalho sem sair do editor.

Neste exercício, você vai:

- monitorar em tempo real o trabalho do agente de acessibilidade;
- revisar e aceitar as edições propostas nos arquivos;
- orientar o agente durante a sessão para adicionar uma opção de modo claro junto com a de alto contraste.

## Cenário

O agente personalizado de acessibilidade usado no [Exercício 4][previous-lesson] está implementando o modo de alto contraste. Enquanto o trabalho está em andamento, a equipe de design fez outra solicitação: também gostaria de uma opção de modo claro para as pessoas que consideram o tema padrão escuro demais. Em vez de iniciar uma nova conversa, você orientará a sessão existente para ampliar o trabalho.

## Acompanhe o progresso do Copilot

A visualização Copilot Chat mostra cada etapa realizada pelo agente: os arquivos que ele explora, os comandos que executa e as edições que propõe. Cada edição aparece no chat com um diff e os controles **Keep** e **Undo**.

1. Volte à visualização Copilot Chat do Exercício 4.
2. Enquanto o agente trabalha, role o chat para acompanhar cada chamada de ferramenta. Você verá leituras e edições de arquivos e os comandos de terminal que ele solicitar para executar.
3. Quando o agente propor a edição de um arquivo, o diff aparecerá no chat:
    - Selecione **Keep** para aceitar a alteração.
    - Selecione **Undo** para desfazer a alteração e permitir que o agente tente novamente.
4. Você também pode abrir o indicador **Files changed** na parte superior do chat para ver todo o conjunto de arquivos alterados durante a sessão.

> [!NOTE]
> Se uma chamada de ferramenta solicitar permissão, por exemplo, para executar um comando de terminal, o agente pausará e mostrará um prompt **Allow**. Aprove somente os comandos que considerar seguros.

5. Aguarde até que o agente termine de implementar o modo de alto contraste. Você deverá ver uma mensagem final resumindo as alterações.

## Oriente o agente para adicionar o modo claro

Agora que o modo de alto contraste está pronto, você ampliará a mesma conversa para adicionar uma opção de modo claro. Como continuará na mesma sessão de chat, o agente manterá todo o contexto do trabalho anterior, incluindo os componentes alterados, a abordagem de estilo e o padrão de armazenamento local.

1. Na caixa de entrada do Copilot Chat, envie este prompt complementar:

    ```plaintext
    Bom trabalho! Agora adicione uma opção de modo claro junto com a opção de alto contraste. O modo claro deve seguir o mesmo padrão: persistir no armazenamento local e ficar disponível na mesma área da interface. O usuário deve poder ativar o alto contraste e o modo claro de maneira independente.
    ```

2. O agente retomará o trabalho, explorará as mudanças já feitas e proporá as adições para o modo claro.
3. Revise cada nova edição conforme ela aparecer, como fez para o modo de alto contraste. Use **Keep** ou **Undo** em cada diff.
4. Se o agente seguir uma direção indesejada — por exemplo, tentar refatorar a interface das opções de uma maneira que você não quer — interrompa-o com o botão **Stop** ao lado da caixa de entrada e envie uma mensagem complementar para esclarecer o pedido.

> [!TIP]
> Orientar uma sessão em andamento é mais rápido do que começar de novo. Use prompts complementares para solicitar ajustes ("simplifique o CSS — use variáveis CSS em vez de duplicar seletores"), corrigir o rumo ("não adicione uma terceira opção; integre o modo claro ao painel de configurações existente") ou ampliar o escopo ("adicione também atalhos de teclado para as duas opções").

## Revise o conjunto de trabalho

Antes de fazer commit, revise rapidamente tudo o que o agente alterou.

1. Abra a visualização **Source Control** no VS Code.
2. Revise a lista completa de arquivos alterados. Você deverá ver atualizações nos componentes Astro, nos estilos e em quaisquer testes relacionados.
3. Abra alguns dos arquivos alterados e examine os diffs. Confirme se eles refletem os padrões de acessibilidade do agente personalizado: atributos ARIA, navegação pelo teclado, HTML semântico e persistência no armazenamento local.
4. Quando estiver satisfeito, prepare e faça commit das mudanças no painel Source Control. Você as publicará na [próxima lição][next-lesson].

## Resumo e próximas etapas

Você usou o modo agente do Copilot Chat para monitorar e orientar uma sessão em andamento: revisou cada edição de arquivo, aceitou ou rejeitou mudanças e enviou prompts complementares para ampliar o trabalho sem perder o contexto.

Nesta lição, você explorou:

- como monitorar o trabalho de um agente em tempo real;
- como aceitar e rejeitar edições individuais;
- como orientar uma sessão durante a execução usando prompts complementares.

Na [próxima lição][next-lesson], você publicará o trabalho de acessibilidade como um pull request e revisará as mudanças produzidas pelo agente personalizado local ao longo deste laboratório.

## Recursos

- [Copilot Chat no VS Code][copilot-chat-vscode]
- [Uso do modo agente][agent-mode]

---

| [← Lição anterior: Agentes personalizados][previous-lesson] | [Próxima lição: Iteração sobre o trabalho do Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../4-custom-agents/
[next-lesson]: ../6-iterating/
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
