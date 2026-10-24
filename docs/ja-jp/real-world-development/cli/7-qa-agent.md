---
title: "Lesson 7 - QA エージェントを作成して使う"
description: "issue の要件、quality-checks スキル、Playwright MCP を組み合わせた QA カスタムエージェントを作成します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

これまでに `quality-checks` スキルで自動チェックを実行し、Playwright MCP でブラウザー上のフィルタリングを確認しました。次は、それらの機能を明確に定義した QA プロセスを持つカスタムエージェントにまとめます。

このレッスンでは、次の内容を学びます。

- カスタムエージェントが instruction、スキル、MCP ツールとどのように連携するかを確認する。
- 再利用可能な品質保証プロファイルを作成して確認する。
- QA エージェントを選択し、フィルタリングの issue に照らして指摘事項をレビューする。

## シナリオ

Tailspin Toys では、プルリクエスト (PR) を作成する前に、要件、コード品質、自動チェック、テスト範囲、ブラウザー上の動作を一貫して確認したいと考えています。カスタムエージェントに QA プロセスを調整させると、再利用可能なレポートを作成できます。

## カスタムエージェントとは

カスタムエージェントは、Markdown プロファイルで定義する Copilot の専門的な役割です。プロファイルには、エージェントの目的、instruction、利用できるツールを記述します。このワークショップでは `.github/agents/qa.agent.md` に QA の役割を定義し、Copilot CLI で選択します。

これまでに使ったカスタマイズには、それぞれ異なる役割があります。リポジトリの instruction はチームの標準を示します。`quality-checks` スキルは繰り返し可能なチェックをまとめます。Playwright MCP はブラウザーツールを提供します。QA プロファイルは、これらの機能を使って要件を評価し、結果を報告する方法を Copilot に伝えます。これらの機能を置き換えたり、別の会話を開始したりするものではありません。

## QA プロファイルを作成する

機能 PR を開く前に、再利用可能な QA プロファイルを Copilot に作成してもらいます。プロファイルには、QA で行う確認と守るべき境界の両方を定義します。

1. Codespace に戻り、フィルタリングの会話が Interactive モードであることを確認します。
2. 既定のエージェントに、次のカスタムエージェントを作成するよう依頼します。

   ```plaintext
   Create a custom agent named QA in .github/agents/qa.agent.md. It should check features against their issues and agreed requirements, follow the repository instructions, run the quality-checks skill, use Playwright MCP to verify behavior, and add tests when coverage is missing.

   Have it report each requirement as pass, fail, or blocked with supporting evidence. It must ask before changing implementation code, and it must not commit changes or open pull requests.

   Just create the profile for now so I can review it.
   ```

## プロファイルを確認する

新しいエージェントを使う前に、Copilot が意図した QA ワークフローと境界をプロファイルに反映したことを確認します。これにより、検証だけを行いたいときに、不完全または範囲が広すぎるエージェントが機能を変更するのを防げます。

1. `/diff` を入力し、`.github/agents/qa.agent.md` を開きます。
2. frontmatter を読みます。`description` は必須です。`name` は省略できますが、指定するとエージェントの表示名が明確になります。
3. プロファイルの instruction を読み、QA が要件から確認を始め、リポジトリの instruction に従い、`quality-checks` スキルを実行して、Playwright MCP を使うことを確認します。
4. QA が根拠を示して報告すること、実装コードを変更する前に確認を求めること、変更をコミットしたりプルリクエストを開いたりしないことを確認します。
5. 責務や境界が不足している場合は、続行する前に既定のエージェントへプロファイルの修正を依頼します。

## issue に対して QA を実行する

Copilot CLI は会話の開始時にプロジェクトのエージェントを読み込みます。プロファイルを作成したら同じフィルタリングの会話を再開し、QA を選択します。issue と計画時の決定事項をコンテキストとして使用できます。

1. 次のプロンプトでエージェントを有効にします。

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> 作成したばかりのエージェントは、利用可能なエージェントの一覧に表示されないことがあります。エージェントは利用できるため、上記のコマンドで有効にしてください。

2. 次のプロンプトで QA エージェントに機能をレビューするよう依頼します。

   ```plaintext
   Review the filtering feature against the issue and the decisions in our plan. Is it ready for a PR?
   ```

3. QA エージェントの作業が完了するまで待ちます。
4. 完了したら、提示されたレポートを読みます。

## まとめと次のステップ

再利用可能な専門的役割をワークフローに追加し、その作業を確認しました。このレッスンでは、次の内容を学びました。

- カスタムエージェントが instruction、スキル、MCP ツールとどのように連携するかを確認した。
- 再利用可能な品質保証プロファイルを作成して確認した。
- QA エージェントを選択し、フィルタリングの issue に照らして指摘事項をレビューした。

実装、スキルの更新、QA プロファイル、テスト、検証レポートの準備ができました。次は、[機能 PR にまとめて Agent Merge を使います][next-lesson]。

## リソース

- [Copilot CLI 用のカスタムエージェントを作成する][create-agents]
- [カスタムエージェントの構成][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
