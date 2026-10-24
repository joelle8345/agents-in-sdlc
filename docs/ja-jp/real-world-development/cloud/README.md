---
slug: ja-jp/real-world-development/cloud
title: "GitHub Copilot cloud agent"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

**[GitHub Copilot cloud agent](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent)** を使うと、GitHub Copilot がクラウド上で非同期に作業できます。GitHub で作業を割り当てると、cloud agent がバックグラウンドでリポジトリを調査し、変更を加えてプルリクエストを作成するため、その間に別の作業を進められます。

この一連の演習では、まず cloud agent が従うカスタム instruction を追加し、GitHub issue を割り当てて実装を依頼します。カスタムエージェントを確認して利用し、エージェントの進め方を調整します。エージェントのダッシュボードでセッションを監視して方向づけた後、作成されたプルリクエストをレビューし、結果を反復して改善します。

## 演習

| 演習 | トピック | 説明 |
|----------|-------------|-------------|
| [0. 前提条件][ex0] | セットアップ | リポジトリと Codespace を作成する |
| [1. カスタム instruction][ex1] | コンテキスト | cloud agent が従うカスタム instruction を追加する |
| [2. Cloud Agent][ex2] | 非同期エージェント | GitHub issue を Copilot cloud agent に割り当てる |
| [3. カスタムエージェント][ex3] | 専門エージェント | カスタムエージェントを確認して利用する |
| [4. エージェントの管理][ex4] | 監視 | エージェントのセッションを監視し、方向づける |
| [5. 反復][ex5] | レビュー | プルリクエストをレビューし、Copilot の作業を反復して改善し、次の手順を選ぶ |

## 前提条件

このワークショップに参加する前に、次の条件を満たしていることを確認してください。

- [ ] 有効な **Copilot Student、Pro、Pro+、Business、または Enterprise** プランを利用できる GitHub アカウント
- [ ] アカウントまたは Organization で Copilot cloud agent が有効になっていること

> [!TIP]
> 有料プランを利用していませんか。認証済みの学生は [GitHub Education][callout-student-plan-education] を通じて GitHub Copilot を無料で利用できます。**Copilot Student** プランには、このワークショップで使うエージェント、Model Context Protocol (MCP)、コードレビュー、Copilot CLI の機能が含まれているため、どの開発環境でも演習を完了できます。

[callout-student-plan-education]: https://github.com/education/students

> [!NOTE]
> Cloud agent は **Copilot Free を除く Copilot Student、Pro、Pro+、Business、Enterprise** で利用できます。Copilot Business または Enterprise では、管理者が組織で有効にする必要があります。

> [!NOTE]
> このハーネスでは MCP を扱いません。Copilot で MCP サーバーを使う方法については、[CLI ハーネス](../cli/)または [VS Code ハーネス](../vscode/)を参照してください。

## はじめる

**[演習 0「前提条件」から始める →][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-custom-instructions/
[ex2]: 2-cloud-agent/
[ex3]: 3-custom-agents/
[ex4]: 4-managing-agents/
[ex5]: 5-iterating/
