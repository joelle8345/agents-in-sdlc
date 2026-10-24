---
slug: ja-jp/real-world-development/cli
title: "GitHub Copilot CLI"
description: "Copilot CLI のモード、カスタマイズ、Model Context Protocol (MCP) ツール、プルリクエストの自動化を学びながら、Tailspin Toys の変更を実装、検証、リリースします。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

**[GitHub Copilot CLI][about-copilot-cli]** を使うと、エージェント型コーディングアシスタントとして GitHub Copilot をターミナルで利用できます。コードベースを調査し、コードを生成し、コマンドを実行し、外部ツールに接続できます。すべてコマンドラインから行えるため、グラフィカルエディターに切り替えずに作業の流れを保てます。

このワークショップでは、Tailspin Toys を使った一連のワークフローに取り組みます。

1. GitHub Codespaces でプロジェクトを準備し、Copilot CLI をインストールして、基本操作を確認します。
2. 星評価を追加し、ブラウザーで変更をレビューして、最初のプルリクエスト (PR) を手動でマージします。
3. フィルタリングの issue を起点に、Plan モードでアプローチを決め、Autopilot モードで実装し、Interactive モードでレビューします。
4. リポジトリの instruction を更新し、フィルタリングの作業に適用します。
5. 既存の `quality-checks` スキルをカスタマイズして、プロジェクトのチェックを実行します。
6. Playwright Model Context Protocol (MCP) サーバーを追加し、ブラウザーでフィルタリングを確認します。
7. 品質保証 (QA) 用のカスタムエージェントを作成して使い、要件、テスト範囲、検証の根拠を確認します。
8. フィルタリングの変更全体をレビューし、Agent Merge を使ってフィルタリングの PR をマージします。
9. コンテキスト、モデル、共有、任意のクラウド委任に役立つスラッシュコマンドを確認します。

ワークショップでは、星評価用とフィルタリング用の 2 つの PR を作成します。フィルタリングの PR には、instruction の更新、スキルの更新、QA プロファイル、テストが含まれます。フィルタリングと品質確認の作業は、1 つの会話とブランチで進めるため、各ツールを試しながら作業を積み重ねられます。

## レッスン

| レッスン | トピック | 説明 |
| ------ | ----- | ----------- |
| [0. 前提条件][ex0] | セットアップ | リポジトリと Codespace を作成する |
| [1. Copilot CLI のインストール][ex1] | インストール | Copilot CLI をインストールして認証し、基本操作を確認する |
| [2. 星評価を追加する: 小さな成果][ex2] | 最初の変更 | 既存の評価と null の場合の代替表示を行い、最初の PR をマージする |
| [3. エージェントモード: Plan と Autopilot][ex3] | エージェントモード | issue を基に機能を計画し、Autopilot で実装して、Interactive モードでレビューする |
| [4. カスタム instruction で Copilot を案内する][ex4] | コンテキスト | instruction を確認・更新し、フィルタリングに適用する |
| [5. quality-checks スキルをカスタマイズして使う][ex5] | 繰り返し可能なチェック | 既存のスキルを確認し、レポート形式を変更して実行する |
| [6. Playwright MCP で機能を検証する][ex6] | ブラウザーでの確認 | CLI で MCP を構成し、フィルタリングの動作を調べる |
| [7. QA エージェントを作成して使う][ex7] | 要件とテスト範囲 | 専門エージェントのプロファイルを作成・選択し、最終確認の根拠を集める |
| [8. 機能の PR を作成してマージする][ex8] | レビューとマージ | 変更全体をレビューし、PR を作成して Agent Merge を使う |
| [9. GitHub Copilot CLI のスラッシュコマンド][ex9] | CLI の機能 | コンテキスト、モデル、共有、cloud agent への任意の委任を確認する |
| [10. 振り返りと次のステップ][ex10] | まとめ | ワークフロー、再利用可能なカスタマイズ、参考リソースを振り返る |
| [オプション: Foundry を取り入れる][foundry] | ホスト型エージェント | モデルを準備し、カタログに基づくエージェントをデプロイして、Web サイトに接続する |

## 前提条件

このワークショップに参加する前に、次の条件を満たしていることを確認してください。

- [ ] 有効な **Copilot Student、Pro、Pro+、Business、または Enterprise** プランを利用できる GitHub アカウント
- [ ] リポジトリと Codespace を作成する権限
- [ ] ターミナルまたはコマンドライン操作の基本的な知識

> [!TIP]
> 有料プランを利用していませんか。認証済みの学生は [GitHub Education][student-plan] を通じて GitHub Copilot を無料で利用できます。**Copilot Student** プランには、このワークショップで使うエージェント、MCP、コードレビュー、Copilot CLI の機能が含まれています。

> [!NOTE]
> Copilot Business または Copilot Enterprise を使用している場合は、管理者が Copilot CLI を有効にしていることを確認してください。

## はじめる

**[前提条件から始める →][ex0]**

[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[student-plan]: https://github.com/education/students
[ex0]: 0-prerequisites/
[ex1]: 1-install-copilot-cli/
[ex2]: 2-add-star-rating/
[ex3]: 3-agent-modes/
[ex4]: 4-custom-instructions/
[ex5]: 5-agent-skills/
[ex6]: 6-mcp-playwright/
[ex7]: 7-qa-agent/
[ex8]: 8-create-pull-request/
[ex9]: 9-cli-power-tools/
[ex10]: 10-review/
[foundry]: 8-foundry-agent/
