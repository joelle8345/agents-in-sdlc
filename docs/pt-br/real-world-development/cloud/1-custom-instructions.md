---
title: "Exercício 1 - Instruções personalizadas (agente de nuvem)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lição anterior: Pré-requisitos][previous-lesson] · [Próxima lição: Agente de nuvem do GitHub Copilot →][next-lesson]

O contexto é essencial ao trabalhar com IA generativa. Se uma tarefa precisa ser feita de uma maneira específica — ou se o Copilot deve conhecer informações de contexto — você precisa garantir que esse contexto esteja acessível. Os [arquivos de instruções][instruction-files] fornecem essa orientação para que o Copilot entenda não só *o que* você quer, mas também *como* quer que o trabalho seja feito.

Neste exercício, você vai:

- explorar como o contexto específico do projeto, as diretrizes de codificação e os padrões de documentação chegam ao Copilot por meio das instruções personalizadas do repositório e de arquivos de instruções com escopo por caminho;
- adicionar um novo padrão para todo o repositório a `.github/copilot-instructions.md`.

> [!NOTE]
> Diferentemente dos ambientes do VS Code e do CLI, você não executará aqui um prompt *antes e depois*. O agente de nuvem do Copilot trabalha de forma assíncrona em issues do GitHub, então é mais difícil demonstrar o impacto em tempo real. Você verá a influência do arquivo de instruções mais adiante neste ambiente, ao revisar os pull requests produzidos pelo agente de nuvem.

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

- `.github/copilot-instructions.md` é um único arquivo enviado ao Copilot em **todas** as solicitações feitas no repositório. Ele deve conter informações do projeto relevantes para a maioria das solicitações feitas ao Copilot, como contexto, descrição da tecnologia usada, visão geral do que está sendo desenvolvido, práticas recomendadas e orientações globais.
- Os arquivos `.github/instructions/*.instructions.md` podem ser criados para tarefas ou tipos de arquivo específicos. Você pode usá-los para fornecer diretrizes para linguagens específicas, como TypeScript ou Astro, ou tarefas como criar um componente de interface ou um conjunto de testes unitários.

> [!NOTE]
> Ao trabalhar no ambiente de desenvolvimento integrado (IDE), os arquivos de instruções são usados para gerar código no Copilot Chat, mas não para conclusões de código ou sugestões de próxima edição.
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
6. Por fim, abra `.github/instructions/drizzle.instructions.md` e vá até o final. Observe os links para outros arquivos de instruções, como `unit-tests.instructions.md`, e para arquivos existentes no projeto. Isso permite dividir conjuntos maiores de instruções em arquivos menores e reutilizáveis e apontar o Copilot para exemplos a seguir ao gerar código. (Os caminhos são relativos ao arquivo de instruções, não à raiz do repositório.)

> [!NOTE]
> A seção **Code formatting requirements** em `copilot-instructions.md` documenta os padrões de codificação do projeto, mas ainda não exige documentação no código. Nas próximas etapas, você adicionará regras para comentários de documentação TSDoc e cabeçalhos de comentário nos arquivos.

## Adicione um novo padrão para o repositório

Agora você fará a única edição deste exercício: adicionar uma regra para todo o projeto que exija documentação no código por meio de comentários TSDoc e um cabeçalho de comentário em cada arquivo. O agente de nuvem aplicará essa orientação quando trabalhar nas issues atribuídas a ele mais adiante.

Antes de editar, crie uma branch (o agente de nuvem lerá as instruções da branch de destino da issue, mas você também fará o merge das alterações de forma organizada):

1. No terminal do Codespace, crie uma branch e mude para ela:

   ```bash
   git checkout -b custom-instructions-cloud
   ```

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

## Faça commit, push e merge da atualização de instruções

O agente de nuvem lê os arquivos de instruções da branch de destino da issue. Ao atribuir uma issue ao Copilot no próximo exercício, o Copilot criará uma branch a partir de `main`. Portanto, as alterações nas instruções precisam chegar a `main` para que o agente de nuvem possa usá-las.

1. Prepare e faça commit:

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. Envie a branch:

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. No github.com, abra um pull request da branch `custom-instructions-cloud` para `main` e faça o merge. Assim, o agente de nuvem lerá essas instruções ao trabalhar nas issues que você atribuir no próximo exercício.

> [!TIP]
> Se preferir trabalhar diretamente em `main` neste workshop, você pode pular as etapas da branch e fazer commit diretamente em `main`. A etapa da branch está incluída para que o workshop represente como você faria esse trabalho em um projeto real.

## Resumo e próximas etapas

Você explorou como o Copilot obtém contexto dos arquivos de instruções deste projeto e adicionou um novo padrão para todo o repositório a `.github/copilot-instructions.md`. Você verá esse padrão aplicado nos pull requests gerados pelo agente de nuvem ao longo do restante deste ambiente.

Em seguida, [atribua sua primeira issue ao agente de nuvem do Copilot][next-lesson].

## Recursos

- [Arquivos de instruções para personalizar o GitHub Copilot][instruction-files]
- [Práticas recomendadas para criar instruções personalizadas][instructions-best-practices]
- [5 dicas para escrever instruções melhores para o Copilot][copilot-instructions-five-tips]
- [Awesome Copilot — coleção de arquivos de instruções e outros recursos][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
