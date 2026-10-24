---
title: "Lição 8 - Crie e faça merge do PR do recurso"
description: "Revise a filtragem, as instruções, a atualização da skill, o perfil de QA e os testes em conjunto; depois, crie o PR e use o Agent Merge."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

A implementação da filtragem, as atualizações das instruções, a atualização da skill, o perfil de garantia de qualidade (QA) e os testes estão salvos em uma única branch. Agora, revise tudo em conjunto e abra um pull request. Você mesmo fez o merge do pull request (PR) das avaliações por estrelas; desta vez, permitirá que o **Agent Merge** gerencie o processo.

> [!NOTE]
> Em geral, separaríamos o recurso, as atualizações das instruções, a atualização da skill e o agente de QA em alguns PRs. Para simplificar o workshop, mantivemos todo o fluxo de filtragem e qualidade em uma única sessão e branch, e enviaremos esse trabalho em um único PR.

Nesta lição, você vai:

- aprender o que é Agent Merge e como ele automatiza o ciclo de vida de um merge;
- inspecionar todo o PR do recurso e as evidências de verificação;
- autorizar o Agent Merge somente depois da revisão e confirmar que o PR foi mesclado.

## Cenário

Ao longo do fluxo de trabalho de filtragem, você usou o Copilot para planejar, implementar e verificar um recurso. Agora, a Tailspin Toys quer automatizar o trabalho restante do PR, mantendo a autorização de merge sob o controle da pessoa desenvolvedora.

## Apresentação do Agent Merge

O **Agent Merge** automatiza as tarefas restantes para concluir um pull request no aplicativo GitHub Copilot. Quando você o habilita, a sessão do aplicativo lê o pull request e resolve os impedimentos — corrige falhas de integração contínua (CI), responde a comentários de revisão e faz rebase quando necessário — e faz o merge assim que o GitHub permite. Ele trabalha em segundo plano, continua depois que o aplicativo é reiniciado e é desativado quando o pull request é mesclado.

Até agora, você mesmo selecionou **Merge pull request**. O Agent Merge pode assumir essa responsabilidade, mas ainda precisa de autorização explícita para editar o código e fazer merge. Revise as ações permitidas e o trabalho antes de conceder a permissão de merge.

## Use o Agent Merge para gerenciar o PR

Com o código criado e revisado, vamos deixar que o Agent Merge gerencie o processo do PR.

1. Use o seletor de agentes para selecionar **Default agent**.
2. Selecione o menu suspenso ao lado de **Create PR**.
3. Selecione **Agent Merge**. O botão mudará para **Agent Merge**.
4. Selecione o botão **Agent Merge** para iniciar o processo. Escolher a opção no menu, por si só, não inicia o processo.

O processo do Agent Merge começa. Ele:

- cria o pull request com título e descrição;
- se a sessão começou a partir de uma issue, faz referência à issue relacionada no corpo da descrição;
- faz rebase ou resolve possíveis conflitos de merge com a branch de destino;
- acompanha o processo de CI para garantir que todas as verificações sejam aprovadas;
- acompanha o PR em busca de feedback de outras pessoas desenvolvedoras ou da revisão de código do Copilot e faz atualizações para resolver os comentários;
- pode fazer o merge do PR automaticamente depois que tudo for aprovado.

Vamos permitir que o Agent Merge também faça o merge do PR quando todas as verificações forem aprovadas.

5. Revise o diff do PR e as evidências de verificação antes de conceder permissão para fazer merge.
6. Selecione o menu suspenso ao lado de **Agent Merge**.
7. Confirme que **Merge pull request** está marcado.
8. Peça explicitamente ao agente que faça o merge:

    ```plaintext
    Faça o merge do PR quando todas as verificações e aprovações obrigatórias forem concluídas. Não ignore as proteções do repositório.
    ```

9. Acompanhe o progresso e resolva os impedimentos relatados. Confirme que o status do PR é **Merged** antes de continuar; a permissão de merge habilitada ou um agente em execução não confirmam que o merge foi concluído.

> [!IMPORTANT]
> O Agent Merge não ignora as proteções do repositório nem a falta de permissões. Resolva esses impedimentos antes de continuar.

## Resumo e próximas etapas

Você automatizou várias partes do desenvolvimento, incluindo geração de código, testes, validação e gerenciamento do pull request. Nesta lição, você:

- aprendeu o que é Agent Merge e como ele automatiza o ciclo de vida de um merge;
- inspecionou todo o PR do recurso e as evidências de verificação;
- autorizou o Agent Merge somente depois da revisão e confirmou que o PR foi mesclado.

Em seguida, você [usará um canvas existente e criará um canvas de triagem][next-lesson] para explorar uma maneira mais rica de inspecionar, planejar e visualizar o trabalho com o agente.

## Recursos

- [Gerenciamento de issues e pull requests no aplicativo GitHub Copilot][managing-issues-prs]
- [Sobre o aplicativo GitHub Copilot][about-copilot-app]

[next-lesson]: ../9-canvases/
[managing-issues-prs]: https://docs.github.com/copilot/how-tos/github-copilot-app/managing-issues-and-pull-requests
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
