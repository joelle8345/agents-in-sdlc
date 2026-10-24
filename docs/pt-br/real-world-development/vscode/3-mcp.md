---
title: "Exercício 3 - Teste seu recurso com o servidor Playwright MCP"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lição anterior: Modo agente][previous-lesson] · [Próxima lição: Agentes personalizados →][next-lesson]

Você acabou de criar o recurso de filtragem com o modo agente. Antes de abrir um pull request, confirme se ele funciona no navegador. Em vez de testar o aplicativo manualmente, conecte o **servidor Playwright MCP** e deixe o Copilot controlar um navegador real para testar o recurso. Em seguida, publique a branch e abra o PR.

Neste exercício, você vai:

- aprender o que é Model Context Protocol (MCP) e como os servidores MCP adicionam ferramentas ao Copilot;
- adicionar o servidor Playwright MCP ao seu espaço de trabalho;
- pedir ao Copilot que use o servidor para testar manualmente o recurso de filtragem no navegador;
- publicar sua branch e abrir um pull request para o trabalho de filtragem.

## O que é Model Context Protocol (MCP)?

O modo agente fica muito mais poderoso quando pode acessar recursos além do editor. O Model Context Protocol (MCP) permite que o Copilot faça isso: é um padrão para o agente se comunicar com ferramentas e serviços externos.

![Diagrama que mostra o funcionamento interno do modo agente e como ele interage com contexto, LLM e ferramentas, incluindo ferramentas fornecidas por servidores MCP e extensões do VS Code](../../../_images/ex1-mcp-diagram.png)

O [Model Context Protocol (MCP)](https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/) permite que agentes de IA se comuniquem com ferramentas e serviços externos em tempo real. Assim, eles podem acessar informações atualizadas (usando recursos) e realizar ações em seu nome (usando ferramentas).

Essas ferramentas e esses recursos são acessados por meio de um servidor MCP, que atua como uma ponte entre o agente de IA e as ferramentas e os serviços externos. O servidor MCP gerencia a comunicação entre o agente de IA e as ferramentas externas, como APIs existentes ou ferramentas locais, por exemplo, pacotes npm. Cada servidor MCP oferece um conjunto diferente de ferramentas e recursos ao agente de IA.

Alguns servidores MCP conhecidos:

- **[Servidor MCP do GitHub](https://github.com/github/github-mcp-server)**: oferece acesso a APIs para gerenciar repositórios do GitHub, como criar repositórios, atualizar os existentes e gerenciar issues e pull requests.
- **[Servidor Playwright MCP](https://github.com/microsoft/playwright-mcp)**: oferece recursos de automação de navegador usando o Playwright, como navegar por páginas, preencher formulários e selecionar botões.

Há vários outros servidores MCP que oferecem acesso a ferramentas e recursos diferentes. O GitHub hospeda um [registro de MCP](https://github.com/mcp) para facilitar a descoberta e as contribuições ao ecossistema.

> [!CAUTION]
> Do ponto de vista da segurança, trate os servidores MCP como qualquer outra dependência do projeto. Antes de usar um servidor MCP, revise cuidadosamente o código-fonte, verifique o publicador e considere as implicações de segurança. Use somente servidores MCP confiáveis e tenha cuidado ao conceder acesso a recursos ou operações confidenciais.

## Revise a configuração do MCP

O arquivo `.vscode/mcp.json` configura os servidores MCP disponíveis neste espaço de trabalho do VS Code.

1. Abra `.vscode/mcp.json` no Codespace.
2. Você deverá ver um servidor `github` já configurado:

    ```json
    {
      "servers": {
        "github": {
          "type": "http",
          "url": "https://api.githubcopilot.com/mcp/"
        }
      }
    }
    ```

A entrada `github` vem com o modelo do projeto. Por isso, o Copilot conseguiu acessar o backlog de issues no exercício anterior. Ela usa o [servidor MCP remoto do GitHub][remote-github-mcp-server], então não é necessário instalar nada localmente: o VS Code se conecta por HTTP e você se autentica no GitHub na primeira vez que o Copilot usa uma das ferramentas.

## Adicione o servidor Playwright MCP

Agora você adicionará um segundo servidor. O [servidor Playwright MCP][playwright-mcp-server] oferece ao Copilot um navegador que ele pode controlar, exatamente o que você precisa para testar o recurso.

1. Em `.vscode/mcp.json`, adicione uma entrada `playwright` junto com `github`, deixando o arquivo assim:

    ```json
    {
      "servers": {
        "github": {
          "type": "http",
          "url": "https://api.githubcopilot.com/mcp/"
        },
        "playwright": {
          "command": "npx",
          "args": ["@playwright/mcp@latest", "--headless"]
        }
      }
    }
    ```

2. Salve o arquivo.

Diferentemente do servidor remoto `github`, `playwright` é um servidor **local**: o VS Code o inicia no computador executando `npx @playwright/mcp@latest`. O sinalizador `--headless` indica ao Playwright que execute o navegador sem uma janela visível, algo necessário em um Codespace, que não tem uma área de trabalho para exibi-la.

> [!NOTE]
> O projeto Tailspin Toys já usa Playwright nos testes de ponta a ponta, então normalmente o navegador necessário já está instalado. Se o Copilot informar mais tarde que falta um navegador, peça que execute `npx playwright install chromium` e tente novamente.

## Inicie e confie no servidor

O VS Code inicia servidores MCP **sob demanda** — na primeira vez que o Copilot precisa das ferramentas de um servidor, o VS Code o inicia e pede que você confirme se confia nele.

1. Em `.vscode/mcp.json`, uma ação **Start** aparece acima da entrada `playwright`. Selecione-a para iniciar o servidor agora e confirmar se a configuração está correta.
2. Se o VS Code perguntar se você confia no servidor, revise a configuração e confirme a confiança para permitir que ele seja iniciado.

Iniciar o servidor manualmente é opcional. Se você pular esta etapa, o VS Code iniciará o servidor e pedirá que você confirme a confiança na primeira vez que o Copilot precisar das ferramentas, na próxima etapa.

## Teste a funcionalidade de filtragem

O [servidor Playwright MCP][playwright-mcp-server] oferece ao Copilot um navegador real para controlar. Em vez de testar as alterações manualmente, o agente pode abrir uma página, navegar, aplicar filtros e ler os resultados, depois resumir o que observou. Essa é uma maneira rápida de confirmar se o recurso funciona como esperado sem sair da conversa.

Internamente, o servidor Playwright MCP usa a [árvore de acessibilidade][playwright-mcp-server] da página, não capturas de tela. Isso significa que o agente interpreta elementos estruturados e rotulados, como botões, links e itens de lista, de maneira semelhante às tecnologias assistivas. Assim, uma verificação funcional rápida também serve como uma verificação básica de acessibilidade.

Com o servidor conectado e o aplicativo em execução, peça ao Copilot que teste o recurso de filtragem criado:

```text
Usando o servidor Playwright MCP, abra um navegador para o aplicativo em execução em http://localhost:4321 e verifique o novo recurso de filtragem de jogos:

1. Acesse a página de jogos e informe quantos jogos estão listados.
2. Aplique um filtro de categoria e confirme que a lista é atualizada para exibir somente os jogos dessa categoria.
3. Limpe o filtro e aplique um filtro de editora. Confirme que a lista é atualizada para exibir somente os jogos dessa editora.
4. Combine um filtro de categoria e um de editora e confirme que os resultados respeitam ambos.

Informe o que observou em cada etapa e destaque qualquer comportamento inesperado.
```

O Copilot abrirá um navegador pelo servidor Playwright MCP, percorrerá as etapas e relatará o que encontrou. Compare o resumo com os critérios de aceitação da issue. Se algo parecer incorreto, faça perguntas adicionais ou peça ao Copilot que corrija o código antes de abrir um pull request.

> [!NOTE]
> O aplicativo precisa estar em execução em `http://localhost:4321` para este teste. Se você parou o servidor de desenvolvimento, inicie-o novamente antes de enviar o prompt. Na primeira vez que o Copilot usar o servidor Playwright MCP, talvez seja necessário baixar um navegador. Se ele informar que falta um navegador, peça que execute `npx playwright install chromium` e tente novamente.

[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp

## Publique a branch e crie um pull request

Agora que você confirmou que o recurso funciona, está pronto para abrir um pull request (PR) para que a equipe o revise. Primeiro, publique a branch `filtering-vscode`.

1. Acesse o painel **Source Control** no Codespace e revise as alterações feitas pelo Copilot.
2. Prepare as alterações selecionando o ícone **+**.
3. Gere uma mensagem de commit usando o botão **Sparkle**.

   ![Captura de tela do painel Source Control mostrando as alterações feitas](../../../_images/ex3-source-control-changes.png)

4. Selecione **Publish** para enviar a branch ao repositório.

## Crie o pull request

Há várias maneiras de criar um pull request, incluindo o github.com e a interface de linha de comando (CLI) do GitHub. Como você já está usando o GitHub Copilot, peça a ele que crie o PR. Ele pode localizar a issue relacionada e associá-la ao PR.

1. Acesse o painel Copilot Chat e selecione **New Chat** para iniciar uma nova sessão.
2. Confirme que **Agent** está selecionado no menu de agentes para que o Copilot possa usar as ferramentas do GitHub.
3. Peça ao Copilot que crie um PR:

   ```plaintext
   Encontre a issue do repositório relacionada à filtragem por categoria e editora. Crie um pull request para a branch atual e associe-o à issue correta.
   ```

4. Quando necessário, selecione **Continue** para permitir que o Copilot colete informações e realize operações. Na primeira vez que ele usar uma ferramenta do GitHub, talvez seja solicitado que você se autentique — siga as instruções.
5. Observe como o Copilot pesquisa as issues, encontra a correta e cria o PR.
6. Selecione o link criado pelo Copilot para revisar o pull request, mas **não faça o merge ainda**.

## Resumo e próximas etapas

Parabéns! Neste exercício, você:

- aprendeu o que é Model Context Protocol (MCP) e como os servidores MCP adicionam ferramentas ao Copilot;
- adicionou o servidor Playwright MCP ao espaço de trabalho;
- usou o servidor para testar manualmente o recurso de filtragem no navegador antes de publicá-lo;
- publicou a branch e abriu um pull request para o trabalho de filtragem.

Você usou um servidor MCP para *testar* um recurso — mas o MCP é apenas uma das maneiras de ampliar os recursos do Copilot. Em seguida, vamos [criar um agente personalizado][next-lesson] para otimizar tarefas focadas, como revisões de acessibilidade.

## Recursos

- [O que é MCP e por que todo mundo está falando sobre isso?][mcp-blog-post]
- [Servidor Microsoft Playwright MCP][playwright-mcp-server]
- [Servidor MCP do GitHub][github-mcp-server]
- [Registro MCP do GitHub][mcp-registry]
- [Servidores MCP no VS Code][vscode-mcp-config]

[previous-lesson]: ../2-agent-mode/
[next-lesson]: ../4-custom-agents/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[github-mcp-server]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[remote-github-mcp-server]: https://github.blog/changelog/2025-06-12-remote-github-mcp-server-is-now-available-in-public-preview/
[vscode-mcp-config]: https://code.visualstudio.com/docs/agents/reference/mcp-configuration
