---
title: "Exercício 4 - Agentes personalizados"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## O que são agentes personalizados?

Os [agentes personalizados][custom-agents-concept] do GitHub Copilot permitem criar assistentes de IA especializados para tarefas ou domínios específicos do fluxo de desenvolvimento. Ao definir agentes em arquivos Markdown na pasta `.github/agents` do repositório, você pode fornecer instruções focadas, práticas recomendadas, padrões de codificação e conhecimento específico do domínio para orientar o Copilot a realizar determinados tipos de trabalho com mais eficiência. As equipes podem registrar seus conhecimentos em agentes reutilizáveis — por exemplo, um agente de acessibilidade que aplica a conformidade com as [Diretrizes de Acessibilidade para Conteúdo da Web (WCAG)][wcag], um agente de segurança que segue práticas de codificação segura ou um agente de testes que mantém padrões consistentes.

Os agentes personalizados são definidos em arquivos Markdown na pasta `.github/agents` do projeto ou globalmente em `~/.copilot/agents`. Cada arquivo inclui frontmatter YAML com pelo menos `name` e `description`, seguido por um prompt Markdown que define o comportamento, a especialidade e as instruções do agente.

### Agentes personalizados e skills de agente

Há alguma sobreposição entre agentes personalizados e [skills de agente][agent-skills-concept]. Ambos são definidos principalmente em arquivos Markdown e ensinam uma IA a executar tarefas. A distinção mais simples é: um **agente personalizado** é quem executa o trabalho; as **skills** são as ferramentas.

Os agentes personalizados têm sua própria janela de contexto e podem orquestrar skills (e até outros agentes) durante o trabalho. Neste laboratório, o agente personalizado de acessibilidade revisará e atualizará o site de acordo com diretrizes de acessibilidade; como parte desse trabalho, ele poderá chamar skills, como uma skill de fluxo de trabalho de pull request ou outra para executar e gerenciar testes.

> [!NOTE]
> Não existe uma única maneira correta de criar um agente personalizado. Como em qualquer recurso de IA, teste e itere para encontrar o que funciona em seus ambientes e cenários.

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

## Cenário

A Tailspin Toys está comprometida em tornar sua plataforma de financiamento coletivo acessível a todas as pessoas, independentemente de suas capacidades ou preferências visuais. Comentários recentes de usuários indicaram que algumas pessoas têm dificuldade para ler o tema escuro atual devido ao contraste insuficiente entre as cores do texto e do plano de fundo. Para resolver essa questão de acessibilidade, a equipe de design solicitou um modo de alto contraste que as pessoas possam ativar e desativar.

Como a acessibilidade é fundamental, você quer implementar esse recurso o mais rápido possível. Para isso, usará um agente personalizado.

Neste exercício, você vai:

- revisar um agente personalizado de acessibilidade existente;
- usar o agente de acessibilidade no Copilot Chat para implementar um modo de alto contraste.

## Revise o agente personalizado de acessibilidade

Um agente personalizado de acessibilidade já foi criado. Revise o arquivo para entender como ele orientará o Copilot.

Volte ao Codespace e abra um terminal para mudar para uma nova branch criada a partir de `main` para o trabalho de acessibilidade (assim, o PR de filtragem do Exercício 3 continuará separado):

```bash
git checkout main
git pull
git checkout -b accessibility-vscode
```

1. Abra `.github/agents/accessibility.md`.
2. Observe o frontmatter YAML com os campos `name` e `description`.

> [!CAUTION]
> O frontmatter com `name` e `description` é obrigatório para agentes personalizados.

3. Examine as próximas seções, que destacam:
   - responsabilidades principais ao gerar código para um site acessível;
   - práticas recomendadas de acessibilidade;
   - exemplos de código para HTML, CSS e JavaScript;
   - erros e armadilhas comuns.

## Use o agente personalizado no Copilot Chat

O VS Code mostra todos os agentes personalizados definidos em `.github/agents` no menu de agentes, na parte inferior da visualização Copilot Chat. Você pode selecionar um agente personalizado para limitar o escopo da sessão de chat às instruções e ferramentas desse agente.

> [!TIP]
> **Abra o Copilot Chat**
>
> Antes de começar os exercícios abaixo, volte ao Codespace, abra o painel Copilot Chat e selecione **New Chat** para iniciar uma conversa limpa. A seleção de modo e modelo varia por exercício — cada etapa indica essas opções quando forem relevantes.

1. Selecione **Agent** no menu de agentes da visualização Chat, caso ainda não esteja selecionado.

   ![Captura de tela do seletor de agentes na visualização Chat.](../../../_images/shared-chat-mode-selector.png)

2. Selecione o menu de agentes na parte inferior da visualização Chat (ele mostra o agente ativo, que por padrão é **default**).
3. Selecione **Accessibility agent** na lista de agentes disponíveis.
4. Envie este prompt ao agente de acessibilidade:

    ```plaintext
    Adicione um modo de alto contraste ao site. Inclua uma opção que o usuário possa ativar para usar o alto contraste e salve essa configuração no armazenamento local do navegador para que ela persista após recarregar a página.
    ```

5. O Copilot Chat começará a trabalhar: explorará a base de código, proporá mudanças e aplicará edições aos arquivos do projeto. Cada edição aparecerá no chat com o caminho do arquivo e um diff para revisão.
6. À medida que as edições forem aplicadas, o indicador **Files changed** será atualizado para mostrar o conjunto de arquivos alterados pelo agente.

> [!NOTE]
> Esse processo provavelmente levará alguns minutos. O Copilot está fazendo mudanças reais no repositório: editará arquivos existentes, como componentes Astro e CSS, e quaisquer testes relacionados.

Você revisará e orientará esse trabalho em andamento no próximo exercício.

## Resumo e próximas etapas

Neste exercício, você explorou os [agentes personalizados][custom-agents] do GitHub Copilot, assistentes de IA especializados em tarefas e domínios específicos. Com agentes personalizados, você pode registrar o conhecimento e os padrões da equipe em agentes reutilizáveis que orientam o Copilot na execução de diferentes tipos de trabalho.

Você explorou os seguintes conceitos:

- como os agentes personalizados são definidos;
- como usar um agente personalizado no modo agente do Copilot Chat.

Em seguida, você vai [monitorar e orientar o trabalho do agente][next-lesson], revisando as mudanças enquanto são feitas e adicionando uma opção de modo claro à mesma sessão.

## Recursos

- [Sobre agentes personalizados][custom-agents]
- [Criação de agentes personalizados no IDE][creating-custom-agents-ide]
- [Agentes personalizados no VS Code][custom-agents-vscode]
- [Configuração de agentes personalizados][custom-agents-config]
- [Agentes personalizados no awesome-copilot][awesome-copilot-agents]

---

| [← Lição anterior: Teste seu recurso com o servidor Playwright MCP][previous-lesson] | [Próxima lição: Monitoramento e gerenciamento de agentes →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-mcp/
[next-lesson]: ../5-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[creating-custom-agents-ide]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/create-custom-agents-in-your-ide
[custom-agents-vscode]: https://code.visualstudio.com/docs/copilot/customization/custom-agents
[custom-agents-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
[awesome-copilot-agents]: https://github.com/github/awesome-copilot/tree/main/agents
