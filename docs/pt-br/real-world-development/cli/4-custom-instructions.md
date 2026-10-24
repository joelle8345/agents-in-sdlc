---
title: "Lição 4 - Oriente o Copilot com instruções personalizadas"
description: "Explore as instruções do repositório, adicione um padrão de documentação e aplique-o ao código de filtragem."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

O contexto é essencial ao trabalhar com IA generativa. Quando uma tarefa precisa ser executada de uma maneira específica, você quer que essa orientação esteja disponível para o Copilot. Os [arquivos de instruções][instruction-files] descrevem não apenas *o que* você quer, mas também *como* o código deve ser estruturado. Agora que você implementou a filtragem, vai explorar as instruções usadas pelo Copilot, adicionar um padrão de documentação e aplicá-lo ao código.

Nesta lição, você vai:

- explorar como as instruções do repositório e os arquivos de instruções com escopo por caminho chegam ao agente;
- atualizar o arquivo de instruções para garantir que os padrões de codificação sejam seguidos;
- observar o efeito dos arquivos de instruções no código.

## Cenário

Como toda boa empresa de desenvolvimento, a Tailspin Toys tem diretrizes e requisitos para as práticas de desenvolvimento. Entre eles:

- Os comentários devem explicar a intenção e decisões não óbvias, não apenas repetir o código.
- As funções exportadas em `db/` e `src/lib/` devem documentar a finalidade, os parâmetros e os valores retornados com TSDoc/JSDoc, incluindo um argumento `db` injetável quando houver.
- Os componentes Astro reutilizáveis devem documentar seus contratos `Props`, e os comentários devem continuar atualizados quando o código relacionado mudar.
- As orientações existentes de formatação e lint devem ser preservadas.

Com os arquivos de instruções, você dará ao Copilot as informações necessárias para executar tarefas de acordo com as práticas destacadas.

## Arquivos de instruções

As instruções personalizadas fornecem contexto e preferências ao Copilot para que ele entenda melhor seu estilo de codificação e seus requisitos. Elas ajudam a orientar o Copilot para que ele sugira código mais relevante. Você pode especificar convenções de codificação, bibliotecas e tipos de comentário preferidos. É possível criar instruções para todo o repositório ou para tipos específicos de arquivo e tarefas.

Há dois tipos de arquivos de instruções:

- `.github/copilot-instructions.md` é um único arquivo enviado ao Copilot em **todas** as solicitações feitas no repositório. Ele deve conter informações sobre o projeto relevantes para a maioria das solicitações.
- Os arquivos `.github/instructions/*.instructions.md` fornecem diretrizes para linguagens, tipos de arquivo ou tarefas específicos.

> [!NOTE]
> Outros formatos de instrução e o suporte a eles variam por ambiente. Consulte a [referência de suporte a instruções personalizadas][custom-instructions-support] antes de depender de um formato específico.

## Explore os arquivos de instruções personalizadas deste projeto

O projeto inicial já contém um conjunto de arquivos de instruções. Vamos explorá-los antes de fazer uma alteração para observar o efeito.

1. Volte ao Codespace.
2. No editor do Codespaces, não no terminal, abra `.github/copilot-instructions.md`.
3. Explore o arquivo e observe a breve descrição do projeto e as orientações de codificação. Essas instruções se aplicam a todas as interações com o Copilot neste repositório.
4. Abra a pasta `.github/instructions` e explore os arquivos. Há instruções para arquivos Astro, a camada de dados Drizzle, testes e outros tópicos.
5. Abra `.github/instructions/unit-tests.instructions.md`. Observe o campo `applyTo` no início do arquivo — ele define o glob que determina a quais arquivos as instruções se aplicam.
6. Abra `.github/instructions/drizzle.instructions.md` e observe os links para outros arquivos de instruções e arquivos existentes do projeto. Assim, você pode dividir conjuntos de instruções maiores em arquivos menores e reutilizáveis e apontar o Copilot para exemplos.

## Atualize as instruções para corresponder às orientações da equipe

Os arquivos atuais são um bom começo, mas ainda falta uma orientação. Vamos modificar o arquivo principal `copilot-instructions.md` para exigir comentários TSDoc no TypeScript recém-gerado.

1. Em `.github/copilot-instructions.md`, localize a seção **Code formatting guidance**, que deve estar perto da linha 35.
2. Adicione o item a seguir como o último item da lista:

   ```markdown
   - Todo TypeScript novo deve incluir comentários TSDoc para documentação.
   ```

O arquivo será salvo automaticamente.

## Aplique as orientações atualizadas

O Copilot CLI carrega as instruções do repositório quando uma conversa é iniciada. Depois de salvar as instruções atualizadas, saia e retome a conversa de filtragem para que o Copilot comece a usar a nova orientação sem perder o contexto do recurso.

1. Se a conversa de filtragem ainda estiver aberta, digite `/exit` para encerrá-la. O Copilot CLI salva as conversas automaticamente.
2. Na raiz do repositório, na branch `game-filters-cli`, retome a conversa salva:

   ```bash
   copilot --resume
   ```

   Se solicitado, selecione a conversa de filtragem e confirme que a branch `game-filters-cli` está selecionada.
3. Peça ao Copilot que aplique a orientação atualizada:

   ```plaintext
   Acabamos de atualizar as instruções e as orientações de código. Atualize o código que você gerou para seguir essas orientações.
   ```

4. Digite `/diff` e leia os arquivos TypeScript alterados. Observe os comentários TSDoc recém-gerados e confirme se descrevem o código corretamente.

## Resumo e próximas etapas

Você explorou como o Copilot CLI obtém contexto dos arquivos de instruções e aplicou um novo padrão ao recurso. Especificamente, você:

- explorou como as instruções do repositório e os arquivos de instruções com escopo por caminho chegam ao agente;
- atualizou o arquivo de instruções para garantir que os padrões de codificação sejam seguidos;
- observou o efeito dos arquivos de instruções no código.

Em seguida, você [personalizará e executará a skill reutilizável `quality-checks`][next-lesson] para executar lint e testes de maneira consistente.

## Recursos

- [Adição de instruções personalizadas para o Copilot CLI][instruction-files]
- [Suporte a instruções personalizadas][custom-instructions-support]
- [Práticas recomendadas para criar instruções personalizadas][instructions-best-practices]
- [Awesome Copilot — coleção de arquivos de instruções e outros recursos][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
