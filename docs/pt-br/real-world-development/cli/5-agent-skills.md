---
title: "Lição 5 - Personalize e use uma skill quality-checks"
description: "Explore a skill quality-checks existente, personalize o formato do relatório e use-a para validar os filtros."
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

Escrever código envolve mais do que simplesmente programar. Já validamos manualmente se o código funciona e usamos arquivos de instruções para garantir que ele siga os padrões da equipe. Mas e os testes? E o lint? E as outras partes da integração contínua (CI)?

Para esse tipo de tarefa, as **skills de agente** são a melhor opção. Elas ajudam o Copilot a entender como executar operações reutilizáveis.

Nesta lição, você vai:

- explorar a skill `quality-checks` existente;
- personalizar o formato dos resultados;
- recarregar e executar a skill.

## Cenário

A Tailspin Toys usa a skill `quality-checks` para executar testes unitários, lint e verificações de tipos. A equipe quer aprimorar o relatório para facilitar a leitura dos resultados.

## Instruções, scripts e recursos

As skills de agente agrupam instruções reutilizáveis para tarefas, scripts executáveis e recursos de apoio que um agente carrega sob demanda. Em sua forma básica, uma skill é uma pasta com o nome correspondente e um arquivo Markdown chamado `SKILL.md`. Esse arquivo inclui frontmatter com um nome e uma descrição para definir a skill, uma visão geral do que ela faz e orientações sobre quando usá-la. A pasta também pode conter subpastas com scripts e outros recursos a serem usados pela skill.

> [!NOTE]
> Pastas e arquivos adicionais não são necessários para uma skill. A skill `quality-checks` da Tailspin Toys contém apenas `SKILL.md` porque usa os comandos existentes do projeto.

As skills podem ficar na pasta `.github/skills` do projeto para se tornarem recursos compartilhados e reutilizados pela equipe, ou na pasta de skills do usuário `~/.copilot/skills`.

## Explore a skill

Vamos explorar a skill que a equipe da Tailspin Toys criou para executar testes unitários, lint e verificações de tipos: `quality-checks`.

1. Volte ao Codespace. No editor do Codespaces, abra `.github/skills/quality-checks/SKILL.md`.
2. Leia `name` e `description` na parte superior. A descrição ajuda o Copilot a decidir quando chamar a skill.
3. Leia as instruções e observe como orientam o Copilot durante os testes e a execução do lint.
4. Observe que a skill ainda não tem uma seção **Results output formatting**.

## Execute a skill antes de fazer uma alteração

As skills podem ser chamadas diretamente pelo Copilot CLI ou usando linguagem natural. Vamos pedir ao Copilot que execute as três verificações da skill.

1. Volte à conversa de filtragem no modo Interactive.
2. Envie o seguinte prompt:

   ```plaintext
   Execute a skill quality-checks para os testes unitários, o lint e as verificações de tipos.
   ```

3. Observe o relatório final.

## Personalize o relatório

Queremos um relatório melhor, que informe o que foi executado, se houve aprovação e o que as ferramentas relataram. Vamos atualizar a skill para gerar esse relatório.

1. Volte a `.github/skills/quality-checks/SKILL.md`.
2. Adicione esta seção ao final do arquivo:

   ```markdown
   ## Formatação dos resultados

   Ao terminar, informe cada comando executado e se foi aprovado, reprovado ou bloqueado. Inclua contagens e durações de testes, erros, avisos e outras métricas somente quando a ferramenta as informar. Indique a próxima ação para cada falha ou impedimento e nunca descreva uma verificação ignorada ou incompleta como aprovada.
   ```

3. O arquivo é salvo automaticamente.

## Execute a skill atualizada

Agora que você fez a alteração, veja-a em ação. O Copilot CLI pode recarregar skills editadas sem reiniciar a conversa.

1. Digite:

   ```plaintext
   /skills reload
   ```

2. Use exatamente o mesmo prompt de antes:

   ```plaintext
   Execute a skill quality-checks para os testes unitários, o lint e as verificações de tipos.
   ```

3. Observe o relatório final e compare-o com o primeiro.

## Resumo e próximas etapas

Você personalizou e usou uma skill de agente existente. Nesta lição, você:

- explorou a skill `quality-checks` para executar testes unitários, lint e verificações de tipos;
- personalizou o formato dos resultados;
- recarregou e executou a skill.

Essa alteração acompanhará a filtragem no PR do recurso. Em seguida, você permitirá que o Copilot interaja diretamente com o site [por meio do servidor Playwright MCP][next-lesson].

## Mais exemplos de skills

Estes exemplos da comunidade são referências, não tarefas adicionais:

- [Especificação de Agent Skills][skill-spec]
- [Fluxo de contribuição: `make-repo-contribution`][contribution-example]
- [Documentos de requisitos: `prd`][prd-example]
- [Diagramas e script de exportação incluído: `drawio`][drawio-example]
- [Teste de navegador: `webapp-testing`][browser-example]

[previous-lesson]: ../4-custom-instructions/
[next-lesson]: ../6-mcp-playwright/
[skill-spec]: https://agentskills.io/specification
[contribution-example]: https://github.com/github/awesome-copilot/tree/main/skills/make-repo-contribution
[prd-example]: https://github.com/github/awesome-copilot/tree/main/skills/prd
[drawio-example]: https://github.com/github/awesome-copilot/tree/main/skills/drawio
[browser-example]: https://github.com/github/awesome-copilot/tree/main/skills/webapp-testing
