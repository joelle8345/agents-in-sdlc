---
title: "Lição 3 - Modos de agente: Plan e Autopilot"
description: "Explore os modos de agente: use Plan para definir uma abordagem, Autopilot para criar filtros a partir de uma issue e Interactive para revisar e verificar o resultado."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

Começamos adicionando um pequeno recurso ao projeto. Mas mudanças maiores exigem um processo mais robusto. Felizmente, o aplicativo GitHub Copilot foi desenvolvido para se adaptar ao fluxo de trabalho existente da organização e ajudar a criar o que é necessário da maneira correta. Esta é a primeira de várias lições em que você seguirá um processo comum de desenvolvimento agêntico: começará por uma issue para desenvolver um novo recurso, confirmará se o código é válido e se o recurso funciona como esperado e, por fim, fará o merge no projeto.

> [!NOTE]
> Você usará a mesma sessão durante todo o fluxo de trabalho do recurso. Normalmente, tipos diferentes de arquivos seriam trabalhados em sessões ou PRs diferentes, mas vamos simplificar para que você possa se concentrar nos conceitos principais.

Nesta lição, você vai:

- iniciar uma nova sessão de agente a partir de uma issue do GitHub;
- definir os requisitos no modo **Plan**;
- implementar o recurso no modo **Autopilot**;
- revisar o código;
- validar manualmente o recurso em um canvas de navegador.

Ao longo do trabalho no recurso, você atualizará as instruções do repositório, personalizará a skill `quality-checks` existente, adicionará validação com MCP, criará um agente de QA e abrirá o PR do recurso.

## Cenário

O catálogo da Tailspin Toys está crescendo, e as pessoas precisam filtrar os jogos por categoria e editora. A issue do backlog descreve o recurso, mas detalhes como a combinação de categorias precisam ser definidos antes da programação. Você usará o modo Plan para resolver essas decisões e, depois, autorizará uma implementação de escopo definido com o Autopilot.

## Contexto

A introdução de agentes de programação com IA ao fluxo de desenvolvimento não muda os fundamentos. Na verdade, eles ficam ainda mais importantes. O fluxo da maioria das pessoas desenvolvedoras é parecido com este:

1. Abrir uma issue registrada com os detalhes do trabalho necessário.
2. Criar um plano para o que será desenvolvido.
3. Desenvolver e revisar o código.
4. Executar os testes para validar o código.
5. Validar manualmente a nova funcionalidade.
6. Criar um pull request (PR).
7. Depois que o código for revisado e o processo de integração contínua for aprovado, fazer o merge.

> [!NOTE]
> Os detalhes exatos variam de acordo com a equipe e a organização, mas a maioria dos fluxos segue essa abordagem.

Seguir esse processo padrão garante que o código gerado por IA atenda aos requisitos e passe pelo mesmo processo de revisão que o código escrito manualmente.

## Modos de sessão

O **modo da sessão** controla o nível de autonomia do agente. Você pode selecioná-lo no menu abaixo do campo de prompt e alterá-lo quando quiser:

- **Interactive**: você e o agente trabalham juntos. O agente sugere alterações e aguarda sua autorização antes de continuar.
- **Plan**: o agente cria um plano primeiro. Você revisa e aprova o plano antes de o agente executá-lo.
- **Autopilot**: o agente trabalha de forma totalmente autônoma — escreve código, executa testes e itera sem aguardar sua autorização.

Comece no modo Plan, revise o plano e, em seguida, use o Autopilot para implementá-lo.

## Inicie uma sessão a partir da issue

Confirme que o PR das avaliações por estrelas foi mesclado e que sua `main` local está atualizada antes de começar.

1. Em **Sessions** na barra lateral, selecione a pasta do repositório Tailspin Toys e, em seguida, **Issues** na navegação superior do repositório. Abra **Allow users to filter games by category and publisher**. Essa issue já foi criada pelo modelo; não é necessário criar outra.
2. Selecione **New session** e escolha uma **new working tree** baseada na `main` atualizada.

    ![Visualização da issue no aplicativo GitHub Copilot com uma seta apontando para o botão New session](../../../_images/app-new-session-from-issue.png)

3. Confirme que a issue está anexada à sessão e selecione **Plan** no seletor de modos.

> [!NOTE]
> Se o Node.js ou o npm não forem encontrados, peça ao agente que execute `node --version` e `npm --version`. Se os comandos funcionarem no terminal, mas não na sessão, verifique o PATH do aplicativo ou a configuração do gerenciador de versões e encerre completamente o aplicativo antes de reabri-lo. Tente novamente a operação e as verificações que falharam; não reinstale o npm somente porque o agente não consegue encontrá-lo.

## Planeje o recurso de filtragem

O planejamento permite revisar a abordagem antes que o Copilot escreva código. Como você começou pela issue, o Copilot já tem a solicitação do recurso no contexto. Envie:

```plaintext
Implemente este recurso.
```

Responda às perguntas do Copilot e compare o plano com os critérios de aceitação da issue. Confirme que ele cobre filtros por categoria e editora, controles acessíveis, mudanças de acesso a dados e testes. Discuta qualquer comportamento pouco claro, como a combinação de várias categorias ou o que acontece quando nenhum jogo corresponde.

O plano deve incluir lint, testes unitários, testes de ponta a ponta (E2E) e verificação de tipos com as ferramentas existentes no projeto. Mantenha o escopo em implementar e testar a filtragem; você criará o PR depois de concluir o fluxo de qualidade. Peça mudanças no plano antes de aprová-lo e mantenha a URL da issue e quaisquer esclarecimentos acordados à disposição para a validação posterior.

## Aprove explicitamente o Autopilot

Quando estiver satisfeito com o plano, selecione **Approve and implement this plan** ou a opção equivalente da sua versão. Confirme o modo ativo em vez de presumir que a aprovação o altera. Verifique se o indicador de modo mostra **Autopilot**.

O Copilot começará a trabalhar na implementação. Ele seguirá o plano, gerará código e executará testes, iterando ao longo do processo.

> [!NOTE]
> A aprovação pode iniciar a implementação imediatamente, então revise o plano antes. Se o Copilot informar que faltam dependências ou que há conflito de portas, resolva o problema de configuração antes de considerar as verificações concluídas. Pare somente os servidores que você iniciou.

## Revise e verifique a implementação

Depois que o código for gerado, revise-o antes do merge, como faria com qualquer outro código. Vamos revisar o código e executar o site para confirmar se tudo está funcionando.

1. Abra **Changes** e inspecione a implementação dos filtros e os testes.
2. Compare o resultado com a issue e com os esclarecimentos aprovados, incluindo as combinações de categorias e editoras. Confirme que as mudanças seguem as instruções existentes do repositório.
3. Inspecione os resultados do lint, dos testes unitários, dos testes E2E e da verificação de tipos. Uma verificação ignorada não representa aprovação.
4. Resolva as falhas e execute novamente as verificações afetadas antes de aceitar a implementação. A configuração E2E do Playwright compila e disponibiliza uma prévia e pode reutilizar um servidor local; confirme que o servidor testado pertence a esta worktree, não a uma lição anterior.

## Explore a nova funcionalidade

O código parece correto, mas será que funciona? Vamos iniciar o aplicativo como antes e abrir o site em um canvas de navegador.

1. Use este prompt para pedir ao Copilot que inicie o aplicativo e abra a página no canvas de navegador:

    ```plaintext
    Inicie o aplicativo e abra-o no canvas de navegador.
    ```

2. Em alguns instantes, o aplicativo será iniciado e uma janela do navegador será aberta dentro do aplicativo Copilot.
3. Selecione uma categoria e confirme se os resultados correspondem a ela. Limpe o filtro, selecione uma editora e confirme se os resultados correspondem a essa editora.
4. Combine os filtros de categoria e editora e compare os resultados com a issue e o plano aprovado. Se várias categorias forem aceitas, verifique o comportamento combinado acordado.
5. Teste uma combinação sem jogos correspondentes e verifique o estado vazio. Limpe ou redefina os filtros e confirme que a lista completa volta a aparecer.
6. Quando terminar, peça ao Copilot que pare o servidor de desenvolvimento iniciado para esta sessão e feche o canvas:

    ```plaintext
    Pare o servidor de desenvolvimento e feche o canvas de navegador.
    ```

## Mantenha esta sessão para as próximas lições

Ainda não crie nem faça merge do PR da filtragem. Mantenha esta sessão, worktree e branch para as Lições 4 a 8. Em seguida, você aplicará instruções personalizadas ao código de filtragem e adicionará melhorias à skill e ao QA antes de criar e mesclar o PR combinado na Lição 8. Você pode deixar a sessão ociosa depois de parar o servidor de desenvolvimento e voltar a ela na próxima lição.

## Resumo e próximas etapas

Você usou diferentes modos de agente para desenvolver e revisar um recurso. Nesta lição, você:

- iniciou uma nova sessão de agente a partir de uma issue do GitHub;
- definiu os requisitos no modo **Plan**;
- implementou o recurso no modo **Autopilot**;
- revisou o código;
- validou manualmente o recurso em um canvas de navegador.

Em seguida, vamos analisar como gerar código que siga práticas documentadas usando [instruções personalizadas][next-lesson].

## Recursos

- [Trabalho com sessões de agente no aplicativo GitHub Copilot][agent-sessions]

[next-lesson]: ../4-custom-instructions/
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
