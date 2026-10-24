---
title: "Exercício 2 - Adicione funcionalidades com o modo agente do Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Até mesmo as atualizações mais simples de um aplicativo costumam exigir mudanças em vários arquivos e operações como executar testes. O fluxo de trabalho de uma pessoa desenvolvedora normalmente envolve localizar todos os arquivos necessários, fazer as alterações, executar os testes, depurar, descobrir qual arquivo ficou faltando, fazer outra atualização... E assim por diante.

É aqui que entra o modo agente do Copilot.

O modo agente do Copilot foi criado para trabalhar com mais autonomia no IDE. Ele funciona de maneira semelhante a uma pessoa desenvolvedora: começa explorando a estrutura existente do projeto, faz as atualizações necessárias, executa tarefas como testes e corrige automaticamente os problemas encontrados. Vamos explorar como usar o modo agente para adicionar funcionalidades ao site.

> [!NOTE]
> Apesar dos nomes semelhantes, o modo agente e o agente de nuvem oferecem experiências diferentes. O modo agente trabalha no IDE, permitindo ciclos rápidos de feedback e interação. O agente de nuvem foi projetado para trabalhar de forma assíncrona, como uma pessoa da equipe, interagindo com você por meio de issues e pull requests.

Neste exercício, você aprenderá como:

- o modo agente do Copilot pode explorar o projeto, identificar os arquivos relevantes e fazer mudanças coordenadas;
- o modo agente do GitHub Copilot pode implementar recursos na interface do usuário e na camada de dados;
- revisar as mudanças e os testes gerados pelo modo agente do Copilot antes de fazer merge na base de código.

## Cenário

À medida que a lista de jogos cresce, você quer permitir que as pessoas filtrem por categoria e editora. Você já adicionou um helper de editoras no exercício anterior e agora concluirá o restante do trabalho na camada de dados, na interface e nos testes usando o modo agente do Copilot.

## Execute o site Tailspin Toys

Antes de fazer mudanças, vamos explorar o site Tailspin Toys para entender a funcionalidade atual.

O site é uma plataforma de financiamento coletivo para jogos de tabuleiro com temática de desenvolvimento. Ele permite listar jogos e exibir detalhes sobre eles. O site é um único aplicativo Astro que renderiza as páginas como HTML estático durante o build. As páginas consultam um banco de dados SQLite local diretamente no frontmatter, usando o Drizzle ORM — não há uma API de back-end separada nem uma estrutura de interface do lado do cliente. Os helpers reutilizáveis de acesso a dados ficam em `src/lib/`, e a interatividade é adicionada com um pequeno elemento `<script>` do Astro, com escopo definido e usando as APIs padrão do Document Object Model (DOM).

### Inicie o site

Para facilitar a execução do site, há uma tarefa `npm run dev` que inicia o servidor de desenvolvimento do Astro. Execute-a no GitHub Codespace:

1. Volte ao Codespace. Você deve estar na branch `main` depois do exercício anterior.
2. Abra um novo terminal no Codespace pressionando <kbd>Control</kbd>+<kbd>`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
3. Crie uma branch para o trabalho de filtragem e mude para ela:

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. Execute o seguinte comando para iniciar o site:

   ```bash
   npm run dev
   ```

   Quando o servidor de desenvolvimento Astro estiver pronto, você verá um banner com a URL, semelhante ao seguinte:

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> Se uma caixa de diálogo perguntar se você quer abrir uma janela do navegador para `http://localhost:4321`, feche-a selecionando **x**.

5. Abra o site mantendo pressionada a tecla <kbd>Command</kbd> (Mac) ou <kbd>Ctrl</kbd> (Windows/Linux) e selecionando o endereço do servidor Astro `http://localhost:4321` no terminal.

> [!NOTE]
> Em um Codespace, selecionar um link localhost no terminal redireciona automaticamente para `https://<your-codespace-name>-4321.app.github.dev/`. Esse é um túnel privado para o Codespace, que agora hospeda o servidor Web.

### Explore o site

Com o site em execução, explore as funcionalidades disponíveis. Os principais recursos incluem:

- **Página inicial**: exibe uma lista de jogos de tabuleiro com títulos, imagens e descrições.
- **Página de detalhes do jogo**: quando você seleciona um jogo, abre uma página com mais informações, incluindo título, descrição, editora e categoria.

## Explore o backlog com o Copilot

> [!TIP]
> **Abra o Copilot Chat**
>
> Antes de começar os exercícios abaixo, volte ao Codespace, abra o painel Copilot Chat e selecione **New Chat** para iniciar uma conversa limpa. A seleção de modo e modelo varia por exercício — cada etapa indica essas opções quando forem relevantes.

A implementação inicial do site funciona, mas queremos adicionar novas funcionalidades. Vamos começar examinando o backlog. Ao criar o projeto a partir do modelo, um backlog de issues foi criado automaticamente. Peça ao GitHub Copilot para mostrar esses itens.

1. Selecione **Agent** no menu de agentes da visualização Chat. O agente executa ações de forma autônoma: planeja e implementa mudanças em vários arquivos, executa comandos de terminal e invoca ferramentas.

   ![Captura de tela do seletor de agentes na visualização Chat.](../../../_images/shared-chat-mode-selector.png)

2. Selecione **Claude Sonnet 4.5** na lista de modelos disponíveis.

> [!CAUTION]
> Os autores deste workshop não estão indicando preferência por um modelo em particular. Durante a criação do workshop, usamos Claude Sonnet 4.5 e o incluímos nas instruções para que as sugestões de código fossem relativamente consistentes e proporcionassem uma boa experiência. Como os modelos de linguagem grandes (LLMs) são probabilísticos, as sugestões recebidas podem ser diferentes das descritas no workshop. Isso é normal e esperado.

> [!NOTE]
> Devido à natureza probabilística dos LLMs, o Copilot pode usar um comando MCP diferente e ainda assim concluir a tarefa.

3. Envie o seguinte prompt ao Copilot para perguntar sobre o backlog de issues:

   ```plaintext
   Mostre o backlog de itens do meu repositório GitHub. Ajude-me a priorizá-los de acordo com a utilidade para o usuário.
   ```

4. Selecione **Continue** para executar o comando que lista todas as issues.
5. Revise a lista gerada.

Observe que o Copilot também priorizou os itens com base no que considera mais útil para o usuário.

## Revise os arquivos de instruções

Antes de pedir ao agente que gere o código, revise o arquivo de instruções que fornecerá contexto ao Copilot. Você usará o arquivo de [interface do usuário (UI)](https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md), que descreve como adicionar funcionalidades ao site.

1. No Codespace, acesse `.github/instructions/ui.instructions.md`.
2. Observe as orientações gerais para adicionar funcionalidades, incluindo:
   - uma visão geral da arquitetura;
   - princípios de design de componentes, testabilidade e acessibilidade;
   - links para arquivos de instruções específicos dos tipos de arquivo, incluindo Astro, Tailwind CSS e Drizzle.

> [!TIP]
> Os arquivos de instruções podem referenciar outros arquivos de instruções e arquivos do projeto. Os caminhos são relativos ao arquivo de instruções. Isso permite reutilizar orientações, dividir conjuntos complexos em partes menores e usar exemplos e modelos para orientar a geração de código.

## Implemente a funcionalidade de filtragem

Para concluir a filtragem, serão necessárias pelo menos três atualizações no aplicativo:

- adicionar ou aprimorar a lógica de filtragem restante na camada de dados (`src/lib/`);
- adicionar ou atualizar testes do comportamento de filtragem;
- atualizar a página de listagem de jogos para incluir a interface de filtragem.

Além disso, os testes precisam ser executados e aprovados antes do merge na base de código. O modo agente do Copilot pode realizar essas tarefas. Vamos adicionar a funcionalidade.

1. Continue a conversa atual com o Copilot ou selecione **New Chat** para iniciar outra.
2. Selecione **Add Context**, **Instructions** e **ui** como o arquivo de instruções.

   ![Captura de tela da seleção do arquivo de instruções da interface do usuário](../../../_images/ex3-select-instructions-file.png)

3. Confirme que **Agent** continua selecionado no menu de agentes da visualização Chat.

   ![Captura de tela do seletor de agentes na visualização Chat.](../../../_images/shared-chat-mode-selector.png)

4. Confirme que **Claude Sonnet 4.5** continua selecionado como modelo.
5. Peça ao Copilot para implementar a funcionalidade com base na issue relacionada do backlog:

   ```plaintext
   Atualize o site para incluir filtros por editora e categoria com base nos requisitos da issue correspondente no backlog. Um helper de editoras já existe do exercício anterior; preserve e aprimore esse trabalho conforme necessário ao concluir as mudanças restantes na camada de dados, na interface e nos testes. Confirme que todos os testes foram aprovados. O servidor já está em execução, então não precisa iniciá-lo.
   ```

6. Acompanhe o Copilot enquanto ele explora o projeto e localiza os arquivos relacionados à funcionalidade. Você deverá vê-lo encontrar os helpers da camada de dados, a interface e os testes. Em seguida, ele modificará os arquivos e executará os testes.

   ![Captura de tela do Copilot explorando os arquivos do projeto](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> O Copilot executará várias tarefas, como explorar o projeto, modificar arquivos e executar testes. Isso pode levar alguns minutos, dependendo da complexidade da tarefa e da base de código. Durante esse processo, os botões **Keep** e **Undo** podem aparecer no editor. Quando o Copilot terminar, você poderá selecionar **Keep** ou **Undo** para cada alteração; não é necessário selecioná-los enquanto o agente ainda está trabalhando.

7. Quando solicitado pelo Copilot, selecione **Continue** para executar os testes.

   ![Captura de tela de uma caixa de diálogo no painel Copilot Chat perguntando se você quer executar os testes](../../../_images/ex3-agent-mode-run-tests.png)

8. Pode haver pausas e alguns testes podem falhar durante o processo. Tudo bem: o Copilot alterna entre gerar código e executar testes até concluir a tarefa sem detectar erros.

   ![Captura de tela de uma sessão concluída do Copilot Chat no modo agente](../../../_images/ex3-agent-mode-proposed-changes.png)

9. Explore o código gerado e procure possíveis problemas.

> [!CAUTION]
> É sempre importante revisar o código gerado pelo Copilot ou por qualquer ferramenta de IA.

10. Volte ao navegador onde o site está em execução e explore a nova funcionalidade.
11. Depois de confirmar que tudo funciona e revisar o código, selecione **Keep** na janela do Copilot Chat.

## Resumo e próximas etapas

Parabéns! Neste exercício, exploramos como usar o modo agente do GitHub Copilot para adicionar recursos ao site Tailspin Toys. Vimos como:

- o modo agente do GitHub Copilot pode implementar recursos na interface e na camada de dados;
- o modo agente do Copilot pode explorar o projeto, identificar os arquivos relevantes e fazer mudanças coordenadas;
- revisar as mudanças e os testes gerados pelo modo agente do Copilot antes de fazer merge na base de código.

Agora vamos [testar o recurso com o servidor Playwright MCP][next-lesson] e abrir um pull request.

### Exercício extra de exploração — implemente paginação

À medida que a lista de jogos cresce, será necessário habilitar a paginação. Usando as habilidades deste exercício, peça ao Copilot para atualizar o site e implementar paginação. Algumas considerações:

- siga as práticas recomendadas existentes, inclusive usando os arquivos de instruções disponíveis;
- considere como implementar a paginação: se o usuário poderá selecionar o tamanho da página ou se ele será fixo;
- ao criar o prompt, forneça ao Copilot as orientações necessárias para que a implementação atenda às suas expectativas;
- talvez seja necessário iterar com o GitHub Copilot, pedindo mudanças e fornecendo contexto. Esse é o fluxo normal ao trabalhar com o Copilot.

## Recursos

- [Modos Ask, Edit e Agent do Copilot: para que servem e quando usá-los][choose-mode]
- [Modo agente no VS Code][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
