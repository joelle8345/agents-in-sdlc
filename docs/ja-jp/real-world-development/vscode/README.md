---
slug: ja-jp/real-world-development/vscode
title: "Visual Studio Code"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

VS Code の **[GitHub Copilot Chat](https://code.visualstudio.com/docs/copilot/chat/copilot-chat)** を使うと、普段使っているコードエディターで GitHub Copilot を利用できます。Visual Studio Code (および GitHub Codespaces) で、Copilot Chat のエージェントモードを操作し、Model Context Protocol (MCP) を通じて外部ツールを接続し、カスタムエージェントを活用します。すべて IDE を離れずに進められ、Copilot はファイル、ターミナル、問題の全体を把握できます。

まずカスタム instruction を追加し、Copilot が従うことを確認します。次に、エージェントモードを使って UI、データレイヤー、テストにまたがるフィルタリング機能を構築します。Playwright MCP サーバーを接続し、プルリクエストを開く前に Copilot にブラウザーを操作させて機能をテストします。最後に、アクセシビリティ用カスタムエージェントをレビューして使い、エディターを離れずに Copilot の変更を監視し、方向づけて反復します。

## 演習

| 演習 | トピック | 説明 |
|----------|-------|-------------|
| [0. 前提条件][ex0] | セットアップ | リポジトリと Codespace を作成する |
| [1. カスタム instruction][ex1] | コンテキスト | VS Code でカスタム instruction を追加して検証する |
| [2. エージェントモード][ex2] | コード生成 | エージェントモードでフィルタリング機能を構築する |
| [3. Playwright による MCP][ex3] | 外部ツール | Playwright MCP サーバーを使ってブラウザーで機能をテストする |
| [4. カスタムエージェント][ex4] | 専門エージェント | カスタムエージェントをレビューして使う |
| [5. エージェントの管理][ex5] | 監視 | エージェントのセッションを監視して方向づける |
| [6. 反復][ex6] | レビュー | Copilot の作業をローカルでレビューし、次のステップを選ぶ |
| [オプション: Foundry を取り入れる][foundry-toolkit] | AI エージェント | VS Code と Foundry Toolkit を使う 3 つのモジュールで、モデルを準備し、エージェントをデプロイしてサイトに接続する |

## 前提条件

このワークショップに参加する前に、次の条件を満たしていることを確認してください。

- [ ] 有効な **Copilot Student、Pro、Pro+、Business、または Enterprise** プランを利用できる GitHub アカウント
- [ ] GitHub Codespaces へのアクセス

> [!TIP]
> 有料プランを利用していませんか。認証済みの学生は [GitHub Education][callout-student-plan-education] を通じて GitHub Copilot を無料で利用できます。**Copilot Student** プランには、このワークショップで使うエージェント、MCP、コードレビュー、Copilot CLI の機能が含まれているため、どのハーネスでも演習を完了できます。

[callout-student-plan-education]: https://github.com/education/students

## はじめる

**[演習 0「前提条件」から始める →][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-custom-instructions/
[ex2]: 2-agent-mode/
[ex3]: 3-mcp/
[ex4]: 4-custom-agents/
[ex5]: 5-managing-agents/
[ex6]: 6-iterating/
[foundry-toolkit]: 7-foundry-toolkit/
