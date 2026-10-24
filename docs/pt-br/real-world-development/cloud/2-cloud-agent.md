---
title: "Exercício 2 - Agente de nuvem do GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lição anterior: Instruções personalizadas][previous-lesson] |
|:--|

É provável que poucas organizações — se é que alguma — não tenham dificuldades com dívida técnica. Ela pode incluir problemas de segurança não resolvidos, código legado que precisa de atualizações ou solicitações de recursos que ficaram no backlog por falta de tempo para implementá-las. O agente de nuvem do GitHub Copilot foi criado para tarefas como atualizar código e adicionar funcionalidades de forma autônoma. Quando termina o trabalho, ele gera um pull request (PR) de rascunho para que uma pessoa desenvolvedora o revise. Assim, você pode delegar tarefas repetitivas, acelerar o desenvolvimento e se concentrar em questões mais importantes.

Neste exercício, você vai explorar:

- como personalizar o ambiente de geração de código;
- como garantir que as operações sejam realizadas com segurança;
- a importância de definir issues com escopo claro;
- como atribuir issues ao Copilot.

## Cenários

A Tailspin Toys tem dívida técnica que gostaria de resolver. Os profissionais contratados inicialmente para criar a primeira versão do site deixaram a documentação em um estado inadequado — na verdade, você verá que ela está completamente ausente. Como primeiro passo, a equipe quer adicionar comentários de documentação TSDoc a todas as funções exportadas no aplicativo.

Além disso, a equipe de design quer melhorar a descoberta de jogos. Ela gostaria que a página de detalhes de cada jogo mostrasse jogos relacionados — outros títulos da mesma categoria — para que as pessoas continuem navegando. Ainda não é necessária uma implementação refinada; a equipe quer algo que possa usar para testes de aceitação da experiência. Isso é um bloqueio, mas outras issues têm prioridade maior no momento.

Esses são exemplos de tarefas que podem ser facilmente adiadas e que são boas candidatas para o agente de nuvem do Copilot. Ele pode trabalhar nelas de forma assíncrona enquanto você se concentra em outras tarefas. Depois, você pode voltar para revisar o trabalho do Copilot e confirmar se tudo está correto.

## Apresentação do agente de nuvem do GitHub Copilot

O [agente de nuvem do GitHub Copilot](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) executa tarefas em segundo plano de maneira semelhante a uma pessoa desenvolvedora. Assim como acontece ao trabalhar com outra pessoa, há várias maneiras de atribuir o trabalho, incluindo [atribuir uma issue do GitHub ao Copilot](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions). Depois de receber a atribuição, o Copilot cria um pull request de rascunho para acompanhar o progresso, configura um ambiente e começa a trabalhar na tarefa. Você pode examinar a sessão enquanto ela estiver em andamento ou depois que terminar. Quando a solução proposta estiver pronta para revisão, o Copilot marcará você no pull request.

## A importância de instruções com escopo adequado

Não há mágica no GitHub Copilot: você não pode pular a etapa de pensar. Até operações aparentemente simples podem envolver complexidade, por isso [defina com cuidado o escopo das tarefas para o agente de nuvem do Copilot][cloud-agent-best-practices]. Trate-o como uma pessoa parceira de programação com IA: trabalhe em etapas, aprenda, experimente e ajuste conforme necessário. Os fundamentos do desenvolvimento de software não mudam com a chegada da IA generativa.

## Instruções personalizadas neste repositório

Os exercícios anteriores apresentaram as instruções personalizadas e como elas orientam o Copilot. Se você já concluiu uma atividade prática sobre instruções personalizadas, viu `.github/copilot-instructions.md` em ação; caso contrário, este é um bom momento para dar uma olhada. Antes de atribuir trabalho ao agente de nuvem do Copilot, consulte os arquivos de instruções incluídos no repositório, sem alterá-los, para que depois você possa identificar o efeito deles.

Abra os seguintes arquivos na interface Web do GitHub ou em um Codespace que já esteja em execução:

- `.github/copilot-instructions.md` — revise a seção **Code standards**, especialmente as expectativas para convenções de TypeScript e comentários de documentação TSDoc.
- `.github/instructions/unit-tests.instructions.md` — observe o frontmatter `applyTo`, que limita o escopo destas instruções aos arquivos `**/*.test.ts`.

Quando você atribuir a issue `Code lacks documentation` ao agente de nuvem na próxima seção, observe os comentários TSDoc, as convenções de TypeScript e os cabeçalhos de comentário no pull request resultante. Esses elementos vêm dos arquivos de instruções que você consultou. Voltaremos a esse assunto ao revisar os pull requests em um exercício posterior.

## Configure o ambiente de desenvolvimento do agente de nuvem do Copilot

Criar código normalmente exige um ambiente específico e a execução de scripts de configuração para garantir que tudo esteja pronto. O mesmo vale ao atribuir tarefas ao Copilot, que trabalha de forma semelhante a uma pessoa engenheira de software.

O agente de nuvem usa o [GitHub Actions][github-actions] como ambiente de trabalho. Você pode personalizar esse ambiente criando um [fluxo de trabalho especial de configuração][setup-workflow] no arquivo `.github/workflows/copilot-setup-steps.yml`, que será executado antes de o agente começar. Assim, ele terá acesso às ferramentas e dependências de desenvolvimento necessárias. Esse fluxo de trabalho já foi configurado para facilitar o laboratório e demonstrar esse recurso. Ele garante que o Copilot tenha acesso ao Node.js, às dependências do projeto, aos navegadores para testes de ponta a ponta e ao banco de dados SQLite migrado e preenchido com dados do aplicativo Astro:

```yaml
name: "Copilot Setup Steps"

# Permite testar as etapas de configuração na guia "Actions" do repositório
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # Defina as permissões mínimas necessárias para *suas etapas*. O Copilot receberá um token próprio para as operações dele.
    permissions:
      # Para clonar o repositório como parte das etapas de configuração, por exemplo, para instalar dependências, você precisará da permissão `contents: read`. Se não clonar o repositório nessas etapas, o Copilot fará isso automaticamente quando elas terminarem.
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # Configuração do front-end/aplicativo - Node.js (o aplicativo inteiro agora usa Astro + Drizzle/libSQL)
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # Migra e popula o banco de dados SQLite local para que builds e testes tenham dados.
      - name: Set up the database
        run: npm run db:setup
```

O arquivo se parece com qualquer outro fluxo de trabalho do GitHub, mas tem alguns pontos importantes:

- Ele contém um único job chamado `copilot-setup-steps`. Esse job é executado no GitHub Actions antes de o Copilot começar a trabalhar no pull request.
- Observe o gatilho `workflow_dispatch`, que permite executar o fluxo de trabalho manualmente na guia **Actions** do repositório. Isso é útil para confirmar se o fluxo funciona sem esperar que o Copilot o execute.

## Adicione documentação

Embora todos reconheçam a importância da documentação, muitos projetos têm informações desatualizadas ou não têm documentação alguma. Essa dívida técnica costuma ficar sem solução, reduzindo a produtividade e dificultando a manutenção da base de código ou a integração de novas pessoas à equipe. Felizmente, o Copilot é muito útil para criar documentação, e esta é uma issue adequada para atribuir ao agente de nuvem. Ele trabalhará em segundo plano para gerar a documentação necessária. Você voltará para revisar o resultado em um exercício futuro.

1. Em uma nova guia do navegador, acesse o repositório no github.com.
2. Selecione a guia **Issues**.
3. Selecione **New issue** para abrir a caixa de diálogo de nova issue.
4. Selecione **Blank issue** para criar a nova issue.
5. Defina **Title** como `Code lacks documentation`.
6. Defina **Description** como:

    ```plaintext
    Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
    ```

7. Selecione **Create** para criar a issue.
8. No lado direito, selecione **Assign to Copilot** para abrir a caixa de diálogo de atribuição.

  ![Atribuição do Copilot a uma issue](../../../_images/shared-assign-copilot.png)

9. Selecione **Assign**.

  ![Detalhes da atribuição do Copilot](../../../_images/ex4-assign-copilot-details.png)

10. Selecione a guia **Pull Requests**.
11. Abra o novo pull request, cujo título será semelhante a `[WIP]: Code lacks documentation`. Se o novo pull request ainda não aparecer na lista, aguarde um ou dois minutos e atualize a janela do navegador.
12. Depois de alguns minutos, o Copilot deverá criar uma lista de tarefas.

> [!NOTE]
> A lista de tarefas do Copilot pode levar alguns minutos para aparecer no pull request. O Copilot está criando o ambiente (executando o fluxo de trabalho descrito acima), analisando o projeto e determinando a melhor abordagem para resolver o problema.

13. Revise a lista e as tarefas que o Copilot pretende concluir.
14. Role a linha do tempo do pull request para baixo. Você deverá ver uma atualização informando que o Copilot começou a trabalhar na issue.
15. Selecione o botão **View session**.

  ![Visualização da sessão do Copilot](../../../_images/ex4-view-session.png)

> [!CAUTION]
> Talvez seja necessário atualizar a janela para ver o indicador atualizado.

16. Observe que você pode acompanhar a sessão ao vivo e ver como o Copilot está resolvendo o problema: ele explora o código e entende o estado atual, pausa para pensar e decidir sobre o plano adequado e cria código.

Esse processo provavelmente levará alguns minutos. Um dos principais objetivos do agente de nuvem do Copilot é executar tarefas de forma assíncrona, deixando você livre para se concentrar em outras atividades. Vamos aproveitar esse recurso: atribua outra tarefa ao agente de nuvem e, enquanto ele trabalha, volte sua atenção para o desenvolvimento de recursos no aplicativo.

## Adicione uma seção de jogos relacionados à página de detalhes do jogo

Como já destacamos, uma das grandes vantagens do agente de nuvem do GitHub Copilot é dividir o trabalho: você pode se concentrar em um conjunto de tarefas enquanto ele cuida de outro. Mesmo que a seção de jogos relacionados para a equipe de design não leve muito tempo, esse tempo ainda pode ser usado para outras tarefas. Vamos atribuí-la ao agente de nuvem do Copilot.

1. Volte ao repositório no github.com.
2. Selecione a guia **Issues**.
3. Selecione **New issue** para abrir a caixa de diálogo de nova issue.
4. Selecione **Blank issue** para usar o modelo em branco.
5. Defina **Title** como `Show related games on the game details page`.
6. Defina **Description** como:

    ```markdown
    Queremos ajudar as pessoas a descobrir mais jogos exibindo jogos relacionados na página de detalhes de cada jogo. A equipe de design quer explorar a experiência do usuário e realizar alguns testes de aceitação. Estes são os requisitos:

   - Adicione em `src/lib/` um helper de acesso a dados que retorne outros jogos da mesma categoria de um jogo, excluindo o próprio jogo.
   - Mostre na página de detalhes do jogo uma seção "Related games" que use o helper.
   - Trate o caso em que um jogo não tem jogos relacionados.
   - Crie testes unitários para o novo helper.
   - Antes de criar o PR, confirme que todos os testes foram aprovados.
    ```

7. Selecione **Create** para criar a issue.
8. No lado direito, selecione **Assign to Copilot** para abrir a caixa de diálogo de atribuição.

  ![Atribuição do Copilot a uma issue](../../../_images/shared-assign-copilot.png)

9. Selecione **Assign**.

Pouco depois, você deverá ver um conjunto de 👀 no primeiro comentário da issue, indicando que o Copilot está trabalhando nela.

![O emoji de olhos indica que o Copilot está trabalhando na issue](../../../_images/ex4-issue-eyes-emoji.png)

O Copilot já está trabalhando diligentemente na segunda solicitação. O agente de nuvem funciona de forma semelhante a uma pessoa engenheira de software, então você não precisa acompanhá-lo ativamente; basta revisar o resultado quando estiver pronto. Agora, vamos criar e usar agentes personalizados.

## Resumo e próximas etapas

Neste exercício, você explorou o [agente de nuvem do GitHub Copilot][copilot-agents]. Com o agente de nuvem, você pode atribuir issues ao Copilot para que ele trabalhe de forma assíncrona. Use o Copilot para resolver dívida técnica, criar recursos ou ajudar a migrar código de uma estrutura para outra.

Você explorou os seguintes conceitos:

- personalizar o ambiente de geração de código;
- garantir que as operações sejam realizadas com segurança;
- compreender a importância de definir issues com escopo claro;
- atribuir issues ao Copilot.

Enquanto o agente de nuvem trabalha em segundo plano, vamos criar e usar agentes personalizados. O [agente de nuvem do Copilot também pode usar servidores do Model Context Protocol (MCP)][cloud-agent-mcp] e pode acessar instruções personalizadas, que exploramos em módulos anteriores.

## Recursos

- [Sobre o agente de nuvem do Copilot][copilot-agents]
- [Atribuição de issues do GitHub ao Copilot][assign-issue]
- [Práticas recomendadas para o fluxo de trabalho de configuração do agente de nuvem][cloud-agent-best-practices]

| [Próxima lição: Agentes personalizados →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
