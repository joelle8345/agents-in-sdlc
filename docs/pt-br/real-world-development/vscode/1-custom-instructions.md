---
title: "Exercício 1 - Instruções personalizadas (VS Code)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lição anterior: Pré-requisitos][previous-lesson] · [Próxima lição: Modo agente →][next-lesson]

O contexto é essencial ao trabalhar com IA generativa. Se uma tarefa precisa ser feita de uma maneira específica — ou se o Copilot deve conhecer informações de contexto — você precisa garantir que esse contexto esteja acessível. Há várias maneiras de compartilhar um contexto específico com o Copilot. Uma das principais são os [arquivos de instruções][instruction-files], que orientam a geração de código.

Neste exercício, você vai:

- explorar como o contexto específico do projeto, as diretrizes de codificação e os padrões de documentação chegam ao Copilot por meio das instruções personalizadas do repositório e de arquivos de instruções com escopo por caminho;
- gerar a primeira parte da camada de dados para filtros (um helper de editoras) com as instruções atuais;
- adicionar um novo padrão para todo o repositório a `.github/copilot-instructions.md`;
- enviar o mesmo prompt novamente e observar o código gerado seguir o novo padrão;
- fazer commit das instruções e da parte de filtragem em `main` para que o Copilot use as orientações atualizadas no próximo exercício.

> [!CAUTION]
> O código gerado pode não seguir todos os padrões definidos. O Copilot é não determinístico. O objetivo deste exercício é observar a *tendência* de mudança no comportamento após a atualização das instruções, não obter exatamente o mesmo resultado caractere por caractere.

## Arquivos de instruções

### Cenário

Como toda boa empresa de desenvolvimento, a Tailspin Toys tem diretrizes e requisitos para as práticas de desenvolvimento. Entre eles:

- A camada de dados sempre precisa de testes unitários.
- A interface do usuário deve usar o modo escuro e ter uma aparência moderna.
- O código deve incluir documentação na forma de comentários TSDoc.
- Um bloco de comentários no início de cada arquivo deve descrever a finalidade dele.

Com os arquivos de instruções, você garantirá que o Copilot tenha as informações necessárias para executar tarefas de acordo com as práticas destacadas.

### Instruções personalizadas

As instruções personalizadas permitem fornecer contexto e preferências ao Copilot para que ele entenda melhor seu estilo de codificação e seus requisitos. Esse recurso ajuda a orientar o Copilot para que ele sugira código mais relevante. Você pode especificar as convenções de codificação e bibliotecas preferidas, além dos tipos de comentários que deseja incluir no código. É possível criar instruções para todo o repositório ou para tipos específicos de arquivos e tarefas.

Há dois tipos de arquivos de instruções:

- `.github/copilot-instructions.md` é um único arquivo enviado ao Copilot em **todas** as solicitações feitas no repositório. Ele deve conter informações do projeto relevantes para a maioria das solicitações, como a stack tecnológica, uma visão geral do que está sendo desenvolvido, práticas recomendadas e orientações globais.
- Os arquivos `.github/instructions/*.instructions.md` podem ser criados para tarefas ou tipos de arquivo específicos. Você pode usá-los para fornecer diretrizes para linguagens específicas, como TypeScript ou Astro, ou tarefas como criar um componente de interface ou um conjunto de testes unitários.

> [!NOTE]
> Ao trabalhar no IDE, os arquivos de instruções são usados para gerar código no Copilot Chat, mas não para conclusões de código ou sugestões de próxima edição.
>
> O Copilot Chat, o Copilot CLI e o agente de nuvem do Copilot usam tanto as instruções do repositório quanto os arquivos `*.instructions.md` com frontmatter `applyTo` ao gerar código.
>
> O Copilot também [oferece suporte a arquivos de instruções em outros padrões][custom-instructions-support], incluindo arquivos AGENTS.md e CLAUDE.md.

### Práticas recomendadas para gerenciar arquivos de instruções

Uma conversa completa sobre como criar arquivos de instruções está fora do escopo deste workshop. No entanto, os exemplos do projeto ilustram uma abordagem representativa. Em linhas gerais:

- Mantenha o conteúdo de `copilot-instructions.md` focado em orientações para o projeto, como uma descrição do que está sendo desenvolvido, a estrutura do projeto e os padrões globais de codificação.
- Use arquivos `*.instructions.md` para instruções específicas de tipos de arquivo, como testes unitários, componentes Astro e a camada de dados, ou de tarefas específicas.
- Use linguagem natural. Mantenha as orientações claras e inclua exemplos de como o código deve ou não deve ser.

Não existe uma única maneira correta de criar arquivos de instruções, assim como não existe uma única maneira de usar IA. A experimentação ajudará você a descobrir o que funciona para seu projeto.

> [!TIP]
> Todo projeto que usa o GitHub Copilot deve ter um conjunto robusto de arquivos de instruções. Ao explorar os arquivos deste projeto, você verá instruções para vários tipos de tarefas, incluindo [atualizações da interface do usuário][ui-instructions] e [Astro][astro-instructions].
>
> O Copilot também pode ajudar você a gerar arquivos de instruções. Cada interface oferece esse recurso de uma maneira diferente (por exemplo, **Configure Chat → Generate Agent Instructions** no VS Code ou `/init` no Copilot CLI) — a lição da interface que você está usando indicará quando isso for relevante.
>
> Quer encontrar modelos ou um ponto de partida? Explore o [awesome-copilot][awesome-copilot], um repositório com arquivos de instruções, agentes personalizados e outros recursos.

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## Explore os arquivos de instruções personalizadas deste projeto

Leia os arquivos de instruções fornecidos com este repositório: há um arquivo principal `copilot-instructions.md` e vários arquivos `*.instructions.md` para diferentes tarefas. Abra-os no editor ou na interface Web do GitHub.

1. Abra `.github/copilot-instructions.md`.
2. Explore o arquivo e observe a breve descrição do projeto e seções como **Agent notes**, **Code standards**, **Scripts** e **Repository Structure**. Em **Code standards**, observe as orientações aninhadas de **GitHub Actions Workflows**. Essas orientações se aplicam a todas as interações com o Copilot neste repositório.
3. Abra a pasta `.github/instructions` e explore os arquivos. Há instruções para arquivos Astro, a camada de dados Drizzle, testes e outros tópicos.
4. Abra `.github/instructions/unit-tests.instructions.md`. Observe o campo `applyTo` no início do arquivo — ele define um glob, relativo à raiz do repositório, que determina a quais arquivos as instruções se aplicam. Neste caso, os arquivos de teste TypeScript correspondentes, por exemplo, ao padrão `**/*.test.ts`, serão incluídos.
5. Observe as instruções específicas para criar testes unitários neste projeto.
6. Por fim, abra `.github/instructions/drizzle.instructions.md` e role até o final. Observe os links para outros arquivos de instruções, como `unit-tests.instructions.md`, e para arquivos existentes no projeto. Isso permite dividir conjuntos maiores de instruções em arquivos menores e reutilizáveis e apontar o Copilot para exemplos a seguir ao gerar código. (Os caminhos são relativos ao arquivo de instruções, não à raiz do repositório.)

> [!NOTE]
> A seção **Code formatting requirements** em `copilot-instructions.md` documenta os padrões de codificação do projeto, mas ainda não exige documentação no código. Nas próximas etapas, você adicionará regras para comentários de documentação TSDoc e cabeçalhos de comentário nos arquivos.

## Crie uma branch para as alterações

Vamos seguir algumas práticas recomendadas e criar uma branch para as alterações.

1. Volte ao Codespace do exercício anterior.
2. Abra um novo terminal pressionando <kbd>Control</kbd>+<kbd>`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
3. Crie uma branch e mude para ela:

   ```bash
   git checkout -b custom-instructions
   ```

## Use o Copilot Chat *antes* de atualizar as instruções

> [!TIP]
> **Abra o Copilot Chat**
>
> Antes de começar os exercícios abaixo, volte ao Codespace, abra o painel Copilot Chat e selecione **New Chat** para iniciar uma conversa limpa. A seleção de modo e modelo varia por exercício — cada etapa indica essas opções quando forem relevantes.

Para observar o efeito das instruções personalizadas, comece enviando um prompt com o arquivo de instruções atual. Depois, você o atualizará e enviará o mesmo prompt novamente para comparar os resultados.

1. Feche as guias do editor abertas nos exercícios anteriores para que o Copilot use somente o contexto necessário.
2. Abra `src/lib/publishers.ts` para indicar ao Copilot onde o helper deve ficar.
3. Selecione **Agent** no menu de agentes da visualização Chat para que o Copilot possa aplicar alterações aos arquivos.

   ![Captura de tela do seletor de agentes na visualização Chat.](../../../_images/shared-chat-mode-selector.png)

4. Envie o seguinte prompt:

   ```plaintext
   Crie ou atualize src/lib/publishers.ts com um helper de acesso a dados que retorne uma lista de todas as editoras, com o nome e a ID de cada uma. Aplique as alterações aos arquivos.
   ```

5. O Copilot explorará o projeto e aplicará atualizações ao código, muitas vezes abrangendo o arquivo do helper e seus testes.
6. Observe que o helper proposto é uma função tipada que recebe um cliente `db` como primeiro argumento e retorna uma matriz tipada de editoras — isso vem das convenções da camada de dados em `.github/instructions/drizzle.instructions.md` (que se aplica a `src/lib/*.ts`).
7. Observe que o código proposto **não inclui** comentários de documentação TSDoc nem um cabeçalho de comentário no arquivo.

> [!CAUTION]
> Como o Copilot é probabilístico, talvez ele inclua comentários de documentação mesmo sem essa orientação. Se isso acontecer, tudo bem — o objetivo continua sendo observar a melhoria de *consistência* depois da atualização das instruções.

## Adicione um novo padrão para o repositório

Como indicado anteriormente, `.github/copilot-instructions.md` fornece informações sobre o projeto ao Copilot. Registre nele os padrões de codificação do repositório para melhorar as sugestões de código.

1. Abra novamente `.github/copilot-instructions.md`.
2. Localize a seção **Code formatting requirements**, que deve estar perto da linha 27. Observe como ela documenta os padrões de codificação do projeto, mas ainda não inclui uma regra para documentação no código — por isso, o helper gerado não tinha comentários de documentação.
3. Adicione as seguintes linhas de Markdown logo abaixo dos padrões existentes para orientar o Copilot a incluir cabeçalhos de comentário nos arquivos e comentários TSDoc:

   ```markdown
   - Toda função exportada deve ter um comentário TSDoc que descreva sua finalidade, seus parâmetros e o valor retornado.
   - Antes das importações ou de qualquer código, adicione ao arquivo um bloco de comentários que explique sua finalidade.
   ```

4. Salve `copilot-instructions.md`.

> [!TIP]
> Como você viu na lição anterior, os arquivos de instruções podem ficar na raiz do repositório (`.github/copilot-instructions.md`) para fornecer orientações globais ou em `*.instructions.md` para linguagens, tipos de arquivo ou tarefas específicas. O arquivo do repositório é o lugar adequado para padrões que se aplicam a todo o projeto, como a regra para comentários de documentação que você acabou de adicionar.

## Envie o prompt novamente e observe a mudança

1. Volte ao Copilot Chat e selecione **New Chat** para limpar o contexto da conversa.
2. Volte a `src/lib/publishers.ts` para que o Copilot se concentre no arquivo correto.
3. Envie o **mesmo prompt** usado anteriormente:

   ```plaintext
   Crie ou atualize src/lib/publishers.ts com um helper de acesso a dados que retorne uma lista de todas as editoras, com o nome e a ID de cada uma. Aplique as alterações aos arquivos.
   ```

4. Observe que o arquivo proposto agora começa com um bloco de comentários semelhante a:

   ```typescript
   /**
    * Helpers de acesso a dados de editoras para a plataforma de financiamento coletivo da Tailspin Toys.
    * Fornece funções para recuperar informações de editoras do banco de dados.
    */
   ```

5. Observe que a função proposta agora inclui um comentário TSDoc semelhante a:

   ```typescript
   /**
    * Retorna uma lista de todas as editoras com suas IDs e seus nomes.
    *
    * @param db - Cliente do banco de dados Drizzle.
    * @returns Uma promessa que é resolvida em uma matriz de objetos de editoras.
    */
   ```

Você orientou o Copilot a seguir um novo padrão do projeto e aplicá-lo ao código real que servirá de base para o próximo exercício.

## Faça commit das instruções e envie a branch

Os arquivos de instruções são recursos do repositório e devem ser gerenciados pelo controle do código-fonte, assim como os outros arquivos. Vamos fazer commit e enviar a branch ao repositório.

1. Abra uma nova janela do terminal pressionando <kbd>Control</kbd>+<kbd>`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
2. No terminal, confirme se as atualizações das instruções e do helper estão presentes executando:

   ```bash
   git status
   ```

3. No terminal, prepare e faça commit da atualização das instruções e de todos os arquivos alterados pelo Copilot para criar a base do helper:

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # If git status shows additional supporting updates (for example tests), add those files too.
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

4. Envie a branch ao repositório:

   ```bash
   git push -u origin custom-instructions
   ```

## Crie e faça merge de um pull request

Com a branch enviada, vamos criar um pull request e vinculá-lo à issue sobre o padrão de documentação do backlog. Em vez de fazer isso manualmente, podemos pedir ao Copilot que localize a issue, crie um PR associado a ela e faça o merge.

> [!NOTE]
> Este é o primeiro exercício em que o Copilot atua no GitHub em seu nome. O modelo do projeto já conecta as ferramentas do GitHub ao ambiente de trabalho, então não é necessário configurar nada. Na primeira vez que o Copilot usar uma dessas ferramentas, o VS Code poderá solicitar que você entre no GitHub. Siga as instruções para autorizá-lo. Você aprenderá como essa conexão funciona (Model Context Protocol) em um exercício posterior.

1. Abra o Copilot Chat no Codespace.
2. Pressione <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd> (Windows/Linux) para abrir a visualização Copilot Chat e confirme que **Agent** está selecionado no seletor de agentes.
3. Peça ao Copilot que localize a issue relacionada à atualização dos arquivos de instruções e crie um PR da branch atual que descreva tanto as atualizações das instruções quanto a nova base do helper de editoras:

   ```plaintext
   Encontre a issue relacionada à atualização do arquivo de instruções. Crie um pull request a partir da branch atual, informe que o PR fecha essa issue e mencione que também adicionamos a base do helper de editoras para o próximo trabalho de filtragem.
   ```

4. O Copilot começará a localizar a issue e criar o PR.
5. Quando o Copilot solicitar permissão para realizar ações no GitHub em seu nome, revise o comando e selecione **Allow** conforme apropriado.
6. Quando o PR for criado, peça ao Copilot que faça o merge na branch `main` e atualize sua branch local usando este prompt:

   ```plaintext
   Faça o merge do PR em main. Em seguida, volte para main localmente e atualize o código mais recente.
   ```

7. Quando o Copilot solicitar permissão para realizar ações no GitHub e executar comandos de shell em seu nome, revise o comando e selecione **Allow** conforme apropriado.

Agora você criou e fez o merge de um pull request com a ajuda do GitHub Copilot.

## Resumo e próximas etapas

Você explorou como o Copilot obtém contexto dos arquivos de instruções deste projeto e usou o Copilot Chat no VS Code para:

- enviar um prompt de geração de código e observar os resultados com as instruções *atuais*;
- adicionar um novo padrão para todo o repositório a `.github/copilot-instructions.md`;
- enviar o mesmo prompt novamente e observar o código proposto seguir o novo padrão;
- fazer commit das instruções e da base do helper em `main` para que o próximo exercício possa se basear nesse trabalho.

Em seguida, você usará essas instruções no [modo agente][next-lesson] enquanto o Copilot adiciona um novo recurso à base de código.

## Recursos

- [Arquivos de instruções para personalizar o GitHub Copilot][instruction-files]
- [Práticas recomendadas para criar instruções personalizadas][instructions-best-practices]
- [5 dicas para escrever instruções melhores para o Copilot][copilot-instructions-five-tips]
- [Instruções pessoais personalizadas para o GitHub Copilot][personal-instructions]
- [Awesome Copilot — coleção de arquivos de instruções e outros recursos][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
