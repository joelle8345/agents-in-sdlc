---
title: "Exercício 5: Iteração sobre o trabalho do GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lição anterior: Gerenciamento de agentes][previous-lesson] |
|:--|

## Revise o trabalho

Ao longo deste laboratório, você trabalhou com o GitHub Copilot em várias tarefas para melhorar a experiência do usuário e adicionar funcionalidades. Você pediu ao Copilot que documentasse o código, criasse um recurso de jogos relacionados para a equipe de design explorar e implementasse recursos de acessibilidade, incluindo opções para alternar entre os modos de alto contraste e claro. Vamos examinar as mudanças no código e, se necessário, enviar comentários ao Copilot para aprimorar o trabalho.

### Cenário

Como já destacamos várias vezes, os fundamentos de design de software e DevOps não mudam com a chegada da IA generativa. Sempre precisamos revisar o código gerado e seguir nosso processo habitual de DevOps. Com isso em mente, vamos revisar as sugestões do GitHub Copilot para a documentação, o recurso de jogos relacionados e os recursos de acessibilidade antes de habilitar a revisão para o restante da equipe.

## Segurança e agente de nuvem do GitHub Copilot

Como o agente de nuvem do Copilot executa tarefas de forma assíncrona e sem supervisão, há restrições de segurança para manter tudo protegido. Entre elas:

- O Copilot tem acesso de leitura ao repositório e acesso de gravação **somente** à branch usada para o código.
- O agente de nuvem é executado no GitHub Actions, que cria um ambiente separado e efêmero para o trabalho.
- Os fluxos de trabalho do GitHub Actions precisam da aprovação de uma pessoa antes de serem executados.
- [O acesso a recursos externos é limitado por padrão](https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall), inclusive para servidores MCP.

## Revise a documentação gerada

Vamos começar examinando o primeiro pull request (PR) criado pelo agente de nuvem do GitHub Copilot: o que adiciona documentação ao código. Você fará isso usando a interface padrão de PRs do GitHub.com.

> [!NOTE]
> Ao abrir o PR, você poderá ver um aviso de que o GitHub Copilot está bloqueado por um firewall. Isso é **esperado**, pois o acesso do Copilot a recursos externos é limitado por padrão, inclusive chamadas a servidores MCP externos. Se quiser, você pode [personalizar ou desabilitar o firewall do agente de nuvem do Copilot][agent-firewall].

1. Volte ao repositório no github.com.
2. Selecione **Pull Requests** para abrir a lista de pull requests.
3. Abra o pull request com um título semelhante a **Add missing documentation** ou outro título mais detalhado.

> [!NOTE]
> Se o Copilot ainda estiver trabalhando, o pull request terá o sinalizador **[WIP]**. Nesse caso, aguarde até que o Copilot conclua o trabalho. Isso pode levar alguns minutos; aproveite para fazer uma pausa ou refletir sobre o que aprendeu até agora.

4. Quando o pull request estiver pronto, selecione a guia **Files changed** e revise as alterações.

    ![Guia Files changed](../../../_images/shared-pr-files-changed.png)

5. Explore o código atualizado, que inclui os novos comentários de documentação TSDoc e outros documentos. As alterações exatas podem variar.

    Ao examinar as mudanças, procure comentários TSDoc, convenções de TypeScript e cabeçalhos de comentário. Eles vêm dos arquivos de instruções personalizadas que você consultou no início do Exercício 2.

6. Depois de revisar as atualizações e confirmar que parecem corretas, volte à guia **Conversation** e role para baixo.
7. Você deverá ver um indicador informando que alguns fluxos de trabalho aguardam aprovação.
8. Se houver fluxos de trabalho aguardando aprovação, selecione **Approve and run workflows**.

   ![Aprovação e execução dos fluxos de trabalho](../../../_images/shared-approve-workflows.png)

9. Os fluxos de trabalho deverão entrar na fila da seção de verificações do pull request. Se tudo correr bem, as verificações do projeto para o aplicativo Astro deverão ser aprovadas. Isso pode levar alguns minutos.

## Solicite mudanças ao GitHub Copilot

Trabalhar com o Copilot em um pull request não é uma via de mão única. Você também pode mencionar o Copilot em comentários no pull request ou em comentários de linha do código, como faria com outras pessoas da equipe. O Copilot verá esses comentários e iniciará outra sessão para atendê-los. Como os resultados não são determinísticos, não há um texto prescritivo para solicitar mudanças. Você pode pedir ao Copilot, por exemplo:

- adicionar cabeçalhos de comentário no início de cada arquivo de código, com uma breve descrição da finalidade;
- adicionar comentários de documentação TSDoc a arquivos TypeScript e Astro;
- criar um README que descreva a estrutura do aplicativo Astro.

1. Adicione um comentário solicitando uma mudança na documentação gerada e mencione **@copilot**, como faria com qualquer pessoa. Use uma das ideias acima ou sugira outra alteração de documentação que gostaria de ver na base de código.
2. Selecione **View Session** para acompanhar o trabalho do Copilot. Observe como ele inicia uma nova sessão para fazer as atualizações.
3. Selecione **Back to pull request** para voltar ao pull request.

    ![Voltar ao pull request](../../../_images/ex7-back-to-pr.png)

4. Quando o Copilot terminar as alterações, deverá aparecer um novo commit no pull request.
5. Selecione a guia **Files changed** para revisar as alterações.

Continue iterando até ficar satisfeito. Quando estiver pronto, você poderá marcar o PR como pronto para revisão e fazer o merge na branch principal.

![Marcar o PR como pronto para revisão](../../../_images/ex7-ready-for-review.png)

## Revise o recurso de jogos relacionados

Agora, volte ao PR criado pelo Copilot para resolver a issue sobre exibir jogos relacionados na página de detalhes do jogo.

1. Volte ao repositório no GitHub.com.
2. Selecione a guia **Pull Requests**.
3. Selecione o PR com um título semelhante a **Show related games on the game details page** ou outro título mais detalhado.
4. Selecione a guia **Files changed** para revisar o código gerado.
5. Depois de revisar as atualizações e confirmar que parecem corretas, volte à guia **Conversation** e role para baixo.
6. Você deverá ver um indicador informando que alguns fluxos de trabalho aguardam aprovação.
7. Se houver fluxos de trabalho aguardando aprovação, selecione **Approve and run workflows**.

   ![Aprovação e execução dos fluxos de trabalho](../../../_images/shared-approve-workflows.png)

8. Os fluxos de trabalho deverão entrar na fila da seção de verificações do pull request. Se tudo correr bem, as verificações do projeto para o aplicativo Astro deverão ser aprovadas. Isso pode levar alguns minutos.
9. **Opcional:** você pode mudar para essa branch no Codespace e testar manualmente o recurso de jogos relacionados. Acesse o Codespace, abra o terminal e execute estes comandos (substitua `<branch-name>` pelo nome da branch criada pelo Copilot, por exemplo, **copilot/fix-8**):

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

O Copilot criou o recurso de jogos relacionados. Como antes, você pode iterar com o agente de nuvem para solicitar atualizações. Por exemplo, peça ao Copilot que ajuste o número de jogos relacionados ou que adicione cabeçalhos de comentário e comentários de documentação TSDoc (lembre-se: a issue foi atribuída **antes** da atualização das instruções personalizadas). Como nos outros casos, faça essas solicitações em um novo comentário na guia **Conversation**; o Copilot o verá e iniciará uma nova sessão.

## Revise os recursos de acessibilidade

Por fim, vamos revisar os recursos de acessibilidade implementados pelo agente personalizado de acessibilidade. Este PR deve incluir o modo de alto contraste atribuído no Exercício 3 e o modo claro solicitado no centro de controle no Exercício 4.

1. Volte ao repositório no GitHub.com.
2. Selecione a guia **Pull Requests**.
3. Selecione o PR com um título semelhante a **Add high contrast mode to website** ou outro título mais detalhado.

> [!NOTE]
> Se o Copilot ainda estiver trabalhando, o pull request terá o sinalizador **[WIP]**. Nesse caso, aguarde até que ele conclua o trabalho. Isso pode levar alguns minutos.

4. Selecione a guia **Files changed** para revisar o código gerado.
5. Revise a implementação, prestando atenção especial a:
   - componentes de interface para alternar entre os modos;
   - uso do armazenamento local para persistir as preferências do usuário;
   - mudanças de CSS ou estilo para os modos de alto contraste e claro;
   - atributos de acessibilidade, como rótulos ARIA e navegação pelo teclado;
   - qualquer código JavaScript ou TypeScript que gerencie a alternância entre os modos.

6. Depois de revisar as atualizações e confirmar que parecem corretas, volte à guia **Conversation** e role para baixo.
7. Você deverá ver um indicador informando que alguns fluxos de trabalho aguardam aprovação.
8. Se houver fluxos de trabalho aguardando aprovação, selecione **Approve and run workflows**.

   ![Aprovação e execução dos fluxos de trabalho](../../../_images/shared-approve-workflows.png)

9. Os fluxos de trabalho deverão entrar na fila da seção de verificações do pull request. Se tudo correr bem, as verificações do projeto para o aplicativo Astro deverão ser aprovadas. Isso pode levar alguns minutos.
10. **Opcional:** você pode mudar para essa branch no Codespace e testar manualmente os recursos de acessibilidade. Acesse o Codespace, abra o terminal e execute estes comandos (substitua `<branch-name>` pelo nome da branch criada pelo Copilot):

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    Em seguida, inicie o aplicativo e teste as opções de modo de alto contraste e claro no navegador. Confirme se funcionam como esperado e se as configurações persistem após recarregar a página.

Observe como o agente personalizado de acessibilidade orientou o Copilot a implementar os recursos seguindo práticas recomendadas de acessibilidade. Se encontrar problemas ou oportunidades de melhoria, mencione **@copilot** em um comentário para solicitar atualizações, como fez nos PRs anteriores.

## Exercício opcional — continue delegando

O agente de nuvem funciona melhor quando você pode delegar itens reais do backlog e se concentrar em outras tarefas. Para desenvolver esse hábito, crie algumas issues no seu repositório e atribua-as ao Copilot. Algumas ideias:

- criar um formulário de interesse de apoiadores na página de detalhes do jogo;
- implementar paginação na lista de jogos;
- adicionar validação de entrada e tratamento de erros aos helpers de acesso a dados.

## Resumo

Você concluiu o ambiente do agente de nuvem. Ao longo destas lições, você:

- **Inspecionou os arquivos de instruções personalizadas fornecidos com o repositório** para observar mais tarde o efeito deles nos resultados do agente de nuvem.
- **Atribuiu issues ao agente de nuvem do Copilot** e acompanhou a configuração do ambiente, o planejamento e a execução assíncrona.
- **Criou e usou um agente personalizado** para acessibilidade, adicionando opções para alternar entre os modos de alto contraste e claro.
- **Usou a página de agentes do Copilot como centro de controle** para monitorar e orientar a sessão de acessibilidade enquanto ela estava em andamento.
- **Revisou e iterou sobre os pull requests do agente de nuvem**, mencionando `@copilot` para solicitar alterações e aprovando fluxos de trabalho.

## Revisão e próximas etapas

Você concluiu o ambiente do agente de nuvem. Para continuar explorando, os outros ambientes complementam o que você praticou:

- 🖥️ **[Ambiente do VS Code](../../vscode/)** — explore o modo agente do Copilot Chat e a integração com MCP diretamente no IDE.
- 💻 **[Ambiente CLI](../../cli/)** — entregue duas mudanças revisadas pelo terminal usando os modos Plan e Autopilot, skills de agente, um agente personalizado de QA, Playwright MCP, Agent Merge e a integração opcional `/delegate` com o agente de nuvem.

No seu próprio repositório, experimente estas ideias:

- atribua ao agente de nuvem uma issue de refatoração ou cobertura de testes;
- crie um agente personalizado para outro domínio;
- configure `copilot-setup-steps.yml` para outra stack.

## Recursos

- [GitHub Copilot][github-copilot]
- [Sobre os agentes do Copilot][copilot-agents]
- [Atribuição de issues do GitHub ao Copilot][assign-issue]
- [Práticas recomendadas para o fluxo de trabalho de configuração do agente de nuvem][cloud-agent-best-practices]
- [Configuração do firewall do agente de nuvem do Copilot][agent-firewall]

---

| [← Lição anterior: Gerenciamento de agentes][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
