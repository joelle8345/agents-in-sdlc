---
title: "Lição 3 - Modos de agente: Plan e Autopilot"
description: "Use o modo Plan para definir uma abordagem, o Autopilot para desenvolver filtros a partir de uma issue e o modo Interactive para revisar o resultado."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Começamos adicionando um pequeno recurso ao projeto. Mas mudanças maiores exigem um processo mais robusto. Felizmente, o GitHub Copilot CLI foi desenvolvido para se adaptar ao fluxo de trabalho existente da organização e ajudar a criar o que é necessário da maneira correta. Esta é a primeira de várias lições em que você seguirá um processo comum de desenvolvimento agêntico: começará por uma issue para desenvolver um novo recurso, confirmará se o código é válido e se o recurso funciona como esperado e, por fim, fará o merge no projeto.

> [!NOTE]
> Você usará a mesma conversa e branch durante todo o fluxo de trabalho do recurso. Normalmente, tipos diferentes de arquivos seriam trabalhados em branches ou PRs diferentes, mas vamos simplificar para que você possa se concentrar nos conceitos principais.

Nesta lição, você vai:

- iniciar uma nova conversa do Copilot a partir de uma issue do GitHub;
- definir os requisitos no modo Plan;
- implementar o recurso com o modo Autopilot;
- revisar o código;
- validar manualmente o recurso em um navegador encaminhado.

Ao longo do trabalho no recurso, você atualizará as instruções do repositório, personalizará a skill `quality-checks` existente, adicionará validação com MCP, criará um agente de QA e abrirá o PR do recurso.

## Cenário

O catálogo da Tailspin Toys está crescendo, e as pessoas precisam filtrar os jogos por categoria e editora. A issue do backlog descreve o recurso, mas detalhes como a combinação de categorias precisam ser definidos antes da programação. Você usará o modo Plan para resolver essas decisões e, depois, autorizará uma implementação de escopo definido com o Autopilot.

## Contexto

A introdução de agentes de programação com IA ao fluxo de desenvolvimento não muda os fundamentos. Na verdade, eles ficam ainda mais importantes. O fluxo da maioria das pessoas desenvolvedoras é parecido com este:

1. Começar por uma issue registrada que descreve o trabalho necessário.
2. Criar um plano para o que será desenvolvido.
3. Desenvolver e revisar o código.
4. Executar os testes para validar o código.
5. Validar manualmente a nova funcionalidade.
6. Criar um pull request (PR).
7. Depois que o código for revisado e a integração contínua for aprovada, fazer o merge.

> [!NOTE]
> Os detalhes exatos variam de acordo com a equipe e a organização, mas a maioria dos fluxos segue essa abordagem.

Seguir esse processo padrão garante que o código gerado por IA atenda aos requisitos e passe pelo mesmo processo de revisão que o código escrito manualmente.

## Modos de conversa

O **modo de conversa** controla o nível de autonomia do agente. Pressione <kbd>Shift</kbd>+<kbd>Tab</kbd> para alternar entre os modos:

- **Interactive**: você e o agente trabalham juntos. O agente sugere alterações e aguarda sua autorização antes de continuar.
- **Plan**: o agente cria um plano e não pode editar os arquivos do projeto.
- **Autopilot**: o agente trabalha de forma autônoma — escreve código, executa testes e itera até concluir a tarefa.

Comece no modo Plan, revise o plano e, em seguida, use o Autopilot para implementá-lo.

## Comece pela issue

Antes de iniciar o trabalho de filtragem, volte ao Codespace e confirme que o repositório e o terminal estão prontos.

1. Volte ao Codespace. Se estiver parado, reinicie-o antes de continuar.
2. Confirme que o PR de avaliação por estrelas foi mesclado.
3. Se o terminal não estiver aberto, pressione <kbd>Control</kbd>+<kbd>`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
4. Atualize `main` e crie uma branch para o trabalho de filtragem:

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. Inicie o Copilot CLI:

   ```bash
   copilot --yolo
   ```

6. Pressione <kbd>Tab</kbd> duas vezes para abrir a guia **Issues**.
7. Pressione <kbd>A</kbd> para exibir todas as issues.
8. Use as teclas de seta para destacar a issue intitulada **Allow users to filter games by category and publisher**.
9. Pressione <kbd>C</kbd> para adicionar a issue ao prompt e voltar à guia **Session**.

Observe que o prompt agora começa com `#7` ou um número semelhante. O caractere `#` permite adicionar ao contexto uma issue ou um pull request (PR) do GitHub.

## Planeje o recurso de filtragem

O planejamento permite definir a abordagem antes de passar uma funcionalidade ou tarefa ao Copilot. Planejar com antecedência é especialmente útil em tarefas complexas. Vamos mudar para o modo Plan e pedir ao Copilot que crie um plano.

1. Pressione <kbd>Shift</kbd>+<kbd>Tab</kbd> para mudar para o modo Plan. Confirme que o indicador abaixo do prompt mostra **Plan**.
2. Depois da referência à issue adicionada na etapa anterior, digite este prompt:

   ```plaintext
   Crie um plano para implementar esse recurso.
   ```

O Copilot começará a criar o plano: primeiro explorará o projeto e depois determinará a melhor abordagem.

3. Durante o processo, o Copilot poderá fazer perguntas sobre como os filtros devem funcionar. Responda de acordo com suas preferências; não há respostas certas ou erradas.
4. Quando o plano estiver concluído, pressione <kbd>Control</kbd>+<kbd>E</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>E</kbd> (Windows/Linux) para expandi-lo.
5. Percorra o plano para revisá-lo.
6. Peça ao Copilot que altere as partes do plano que não correspondam às suas decisões.

## Autorize o Autopilot

Com o plano escrito e revisado, chegou a hora de implementá-lo. Vamos deixar o Copilot executar o trabalho usando o Autopilot.

O Autopilot permite que o Copilot itere sobre o problema até considerar que a tarefa está concluída.

1. Selecione **Accept plan and build on autopilot (recommended)** ou uma opção semelhante na versão instalada.
2. Confirme que o indicador abaixo do prompt mostra **Autopilot**.
3. Acompanhe o Copilot enquanto ele segue o plano, gera código e executa testes.

> [!NOTE]
> A aprovação pode iniciar a implementação imediatamente, então revise o plano antes. Se o Copilot informar que faltam dependências ou que há conflito de portas, resolva o problema de configuração antes de considerar as verificações concluídas.

## Revise e verifique a implementação

Depois que o código for gerado, revise-o antes do merge, como faria com qualquer outro código. Vamos revisar o código e executar o site para confirmar se tudo está funcionando.

1. Pressione <kbd>Shift</kbd>+<kbd>Tab</kbd> para entrar no modo Interactive. Confirme que o indicador não mostra **Plan** nem **Autopilot**.
2. Digite `/diff` e inspecione a implementação dos filtros e os testes.
3. Compare o resultado com a issue e com as decisões tomadas durante o planejamento.
4. Depois da revisão, pressione <kbd>Esc</kbd> para sair da visualização do diff.
5. Revise os resultados das verificações do projeto e peça ao Copilot que resolva quaisquer falhas.

## Explore a nova funcionalidade

O código parece correto, mas será que funciona? Vamos iniciar o aplicativo como antes e abrir o site pela porta encaminhada do Codespaces.

1. Peça ao Copilot que inicie o aplicativo:

   ```plaintext
   Inicie o aplicativo para que eu possa testar o recurso de filtragem no navegador. Informe a URL e deixe o servidor em execução.
   ```

2. Quando o Codespaces informar que a porta `4321` está disponível, selecione **Open in Browser**.
3. Teste a filtragem por categoria, por editora e as combinações definidas no plano.
4. Confirme se o comportamento de redefinição e de resultados vazios corresponde à issue e às suas decisões.
5. Volte ao Codespace e peça ao Copilot que pare o servidor de desenvolvimento iniciado.

## Resumo e próximas etapas

Você usou diferentes modos de conversa para criar e revisar um recurso. Nesta lição, você:

- iniciou uma conversa do Copilot a partir de uma issue do GitHub;
- definiu os requisitos no modo Plan;
- implementou o recurso com o modo Autopilot;
- revisou o código;
- validou manualmente o recurso em um navegador encaminhado.

Em seguida, vamos analisar como gerar código que siga práticas documentadas usando [instruções personalizadas][next-lesson].

## Recursos

- [Autopilot no GitHub Copilot CLI][autopilot]
- [Referência de comandos do Copilot CLI][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
