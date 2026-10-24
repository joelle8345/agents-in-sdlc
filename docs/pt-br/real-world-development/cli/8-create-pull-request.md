---
title: "Lição 8 - Crie e faça merge do pull request do recurso"
description: "Revise a filtragem, as instruções, a atualização da skill, o perfil de garantia de qualidade (QA) e os testes; depois, crie um pull request e use o Agent Merge."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

A implementação da filtragem, as atualizações das instruções, a atualização da skill, o perfil de garantia de qualidade (QA) e os testes estão salvos em uma única branch. Agora, revise tudo em conjunto e abra um pull request. Você mesmo fez o merge do pull request (PR) das avaliações por estrelas; desta vez, permitirá que o **Agent Merge** gerencie o processo.

> [!NOTE]
> Em geral, separaríamos o recurso, as atualizações das instruções, a atualização da skill e o agente de QA em alguns PRs. Para simplificar o workshop, mantivemos todo o fluxo de filtragem e qualidade em uma conversa e uma branch, e enviaremos esse trabalho em um único PR.

Nesta lição, você vai:

- aprender o que é Agent Merge e como ele automatiza o ciclo de vida de um merge;
- inspecionar a alteração completa do recurso e as evidências de verificação;
- criar o PR da filtragem;
- habilitar o Agent Merge somente após a revisão e confirmar que o PR foi mesclado.

## Cenário

Ao longo do fluxo de trabalho de filtragem, você usou o Copilot para planejar, implementar e verificar um recurso. Agora, a Tailspin Toys quer automatizar o trabalho restante do PR, mantendo a autorização de merge sob o controle da pessoa desenvolvedora.

## Apresentação do Agent Merge

O **Agent Merge** automatiza as tarefas restantes para concluir um pull request. Quando habilitado, o Copilot resolve os impedimentos do PR — corrige falhas de integração contínua (CI), responde a comentários de revisão e faz rebase quando necessário — e habilita o merge automático do GitHub quando as configurações do repositório permitem.

Até agora, você mesmo selecionou **Merge pull request**. O Agent Merge pode assumir essa responsabilidade. Revise o trabalho e confirme que está pronto antes de habilitar o Agent Merge.

## Use o Agent Merge para gerenciar o PR

Agora que o código está pronto, vamos revisá-lo em conjunto, criar o PR e deixar que o Agent Merge gerencie o restante do processo.

1. Volte ao Codespace.
2. Abra a caixa de diálogo do agente digitando `/agent`.
3. Selecione **Default** na lista de opções e pressione <kbd>Enter</kbd>.
4. Crie um novo PR usando o comando `/pr create`.
5. Ative o Agent Merge com o comando `/pr agentmerge`.
6. O Copilot acompanhará o processo de integração contínua do PR. Quando todas as verificações forem aprovadas, ele fará o merge.
7. Confirme que o Copilot exibiu uma mensagem semelhante a "PR #14 was squash-merged successfully."

> [!IMPORTANT]
> O Agent Merge não ignora aprovações obrigatórias, proteção de branch, filas de merge, configurações do repositório nem permissões ausentes. Se o processo for bloqueado, leia o motivo informado e faça manualmente o merge revisado quando o repositório permitir.

## Resumo e próximas etapas

Você automatizou várias partes do desenvolvimento, incluindo geração de código, testes, validação e gerenciamento do pull request. Nesta lição, você:

- aprendeu o que é Agent Merge e como ele automatiza o ciclo de vida de um merge;
- inspecionou a alteração completa do recurso e as evidências de verificação;
- criou o PR da filtragem;
- habilitou o Agent Merge somente após a revisão e confirmou que o PR foi mesclado.

Em seguida, você [explorará outros comandos slash úteis do Copilot CLI][next-lesson] para contexto, modelos, compartilhamento e delegação opcional para a nuvem.

## Recursos

- [Gerenciamento de pull requests com o Copilot CLI][manage-prs]
- [Referência de comandos do Copilot CLI][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
