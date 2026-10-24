---
title: "Lição 6 - Valide a funcionalidade com o Playwright MCP"
description: "Inspecione ou configure o Playwright MCP no Copilot CLI e use-o para explorar o recurso de filtragem no navegador."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Como já destacamos, escrever código envolve mais do que simplesmente programar. Precisamos trabalhar com dados, serviços externos e automações adicionais disponíveis para o Copilot. É aí que entram os servidores MCP. Eles permitem que o Copilot ultrapasse os recursos integrados à CLI e acesse mais ferramentas e serviços.

Nesta lição, você vai:

- entender o que é Model Context Protocol (MCP) e como o Copilot CLI o utiliza;
- adicionar o servidor Playwright MCP, caso ele ainda não esteja disponível;
- pedir ao agente que controle um navegador e explore o recurso de filtragem.

## Cenário

Testes unitários e de ponta a ponta são importantes, mas a validação de atualizações da interface do usuário exige interação real com a interface. Você quer permitir que o Copilot use o site como uma pessoa usuária, automatizando a validação das alterações e aumentando a confiança de que elas funcionam como esperado.

## O que é Model Context Protocol (MCP)?

O [Model Context Protocol (MCP)][mcp-blog-post] permite que agentes de IA se comuniquem com ferramentas e serviços externos em tempo real. Assim, eles podem acessar informações atualizadas e realizar ações em seu nome.

As ferramentas e os recursos são acessados por meio de um servidor MCP, que atua como uma ponte entre o agente de IA e as ferramentas e os serviços externos. Cada servidor MCP oferece um conjunto diferente de ferramentas e recursos ao agente.

Alguns servidores MCP conhecidos:

- **[Servidor MCP do GitHub][github-mcp]**: oferece acesso a APIs para gerenciar repositórios, issues e pull requests do GitHub.
- **[Servidor Playwright MCP][playwright-mcp-server]**: oferece recursos de automação de navegador usando o Playwright.

Há vários outros servidores MCP disponíveis. O GitHub hospeda um [registro MCP][mcp-registry] para facilitar a descoberta e as contribuições ao ecossistema.

> [!CAUTION]
> Trate os servidores MCP como qualquer outra dependência do projeto. Antes de usar um, revise o código-fonte, verifique o publicador e considere as implicações de segurança.

## Adicione o servidor Playwright MCP

Se o servidor Playwright MCP ainda não estiver disponível, adicione-o para que o Copilot possa interagir com o site como uma pessoa usuária.

> [!NOTE]
> Se o Playwright MCP já estiver configurado no Copilot CLI, pule estas etapas de configuração e continue na próxima seção.

1. Volte ao Codespace.
2. No Copilot CLI, digite o seguinte comando para abrir a caixa de diálogo de adição de servidor MCP:

   ```plaintext
   /mcp add
   ```

3. Digite `playwright` como nome e pressione <kbd>Tab</kbd>.
4. Confirme o tipo **STDIO** do servidor pressionando <kbd>Enter</kbd> e, em seguida, pressione <kbd>Tab</kbd>.
5. Cole o seguinte na caixa de diálogo **Command**:

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

6. Pressione <kbd>Control</kbd>+<kbd>S</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>S</kbd> (Windows/Linux) para salvar o novo servidor MCP.
7. Pressione <kbd>Esc</kbd> para sair da caixa de diálogo do MCP.

## Peça ao Copilot que explore o recurso com o Playwright

Antes, você confirmou manualmente que a funcionalidade estava correta. Agora, use o servidor Playwright MCP disponível no Copilot para fazer a mesma verificação.

1. Use este prompt para pedir ao Copilot que valide a funcionalidade com o servidor Playwright MCP:

   ```plaintext
   Inicie o aplicativo e use o Playwright MCP para verificar os filtros de acordo com a issue e o nosso plano. Informe o que funciona e o que não funciona, sem fazer alterações. Quando terminar, pare o servidor iniciado.
   ```

> [!NOTE]
> Não é necessário dizer ao Copilot para usar o servidor MCP; normalmente ele identificará a ferramenta apropriada. Mas, como você sabe qual ferramenta deve ser usada, vale a pena especificá-la para obter resultados mais consistentes e economizar alguns tokens.

2. Observe as etapas que o Copilot executa no navegador para confirmar se a funcionalidade está correta.
3. Leia o relatório e confirme se tudo funciona como esperado.

O Copilot iniciará o servidor, usará o Playwright para interagir com o site, parará o servidor e apresentará um relatório.

## Resumo e próximas etapas

Parabéns! Você usou o servidor Playwright MCP para explorar o recurso em um navegador real controlado pelo Copilot CLI. Em resumo, você:

- aprendeu o que é Model Context Protocol (MCP) e como o Copilot CLI o utiliza;
- adicionou o servidor Playwright MCP, caso ele ainda não estivesse disponível;
- pediu ao agente que controlasse um navegador e explorasse o recurso de filtragem.

Em seguida, você [criará um agente personalizado de QA][next-lesson] para combinar a skill e as ferramentas de navegador em uma função especializada.

## Recursos

- [O que é MCP e por que todo mundo está falando sobre isso?][mcp-blog-post]
- [Servidor Microsoft Playwright MCP][playwright-mcp-server]
- [Adição de servidores MCP ao Copilot CLI][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
