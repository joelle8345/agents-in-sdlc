---
title: "レッスン 8 - 機能 PR の作成とマージ"
description: "フィルタリング、instruction、スキルの更新、QA プロファイル、テストをまとめてレビューし、PR を作成して Agent Merge を使います。"
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

フィルタリングの実装、instruction の更新、スキルの更新、品質保証 (QA) プロファイル、テストは、1 つのブランチに保存されています。まとめてレビューし、プルリクエストを開きます。星評価のプルリクエスト (PR) は自分でマージしましたが、今回は **Agent Merge** にプロセスを管理させます。

> [!NOTE]
> 通常は、機能、instruction の更新、スキルの更新、QA エージェントを複数の PR に分けます。ワークショップを簡潔にするため、フィルタリングと品質ワークフロー全体を 1 つのセッションとブランチで進め、すべての作業をこの PR に含めます。

このレッスンでは、次の内容を行います。

- Agent Merge とは何か、マージのライフサイクルをどのように自動化するかを学ぶ。
- 機能 PR 全体と検証の根拠を確認する。
- レビュー後にのみ Agent Merge を承認し、PR がマージされたことを確認する。

## シナリオ

フィルタリング機能の作業を通じて、Copilot を使って機能を計画、実装、検証しました。Tailspin Toys では、マージの承認を開発者が管理しながら、残りの PR 作業を自動化します。

## Agent Merge の概要

**Agent Merge** を使うと、GitHub Copilot app でプルリクエストをマージするまでの作業を自動化できます。有効にすると、アプリのセッションが PR を読み取り、失敗した継続的インテグレーション (CI) チェックの修正、レビューコメントへの対応、必要に応じたリベースなど、マージを妨げる問題に取り組みます。その後、GitHub で許可され次第マージします。バックグラウンドで動作し、アプリの再起動後も継続して、PR がマージされると自動的に停止します。

これまでは自分で **Merge pull request** を選択しました。Agent Merge に任せることもできますが、コードの編集とマージには明示的な承認が必要です。マージを許可する前に、許可する操作と作業内容をレビューしてください。

## Agent Merge で PR を管理する

コードの作成とレビューが完了したので、Agent Merge に PR プロセスを管理させます。

1. エージェントピッカーで **Default agent** を選択します。
2. **Create PR** の横にあるドロップダウンを選択します。
3. **Agent Merge** を選択します。ボタンのラベルが **Agent Merge** に変わります。
4. **Agent Merge** ボタンを選択してプロセスを開始します。ドロップダウン項目を選ぶだけでは開始されません。

Agent Merge が開始されると、次の作業を行います。

- タイトルと説明を付けてプルリクエストを作成する。
- issue からセッションを開始した場合、説明の本文で関連 issue に言及する。
- ターゲットブランチにリベースするか、マージ競合に対処する。
- 継続的インテグレーションを監視し、すべてのチェックが成功することを確認する。
- ほかの開発者や Copilot のコードレビューからのフィードバックを監視し、コメントを解決する変更を加える。
- すべて成功した後、必要に応じて PR を自動的にマージする。

すべてのチェックが成功した後、Agent Merge に PR のマージも許可します。

5. マージ権限を与える前に、PR の差分と検証の根拠をレビューします。
6. **Agent Merge** の横にあるドロップダウンを選択します。
7. **Merge pull request** の横にチェックマークがあることを確認します。
8. 次のプロンプトで、エージェントに明示的にマージを依頼します。

    ```plaintext
    Merge the PR once all required checks and approvals pass. Do not bypass repository protections.
    ```

9. 進捗を確認し、報告された問題を解決します。続行する前に PR の状態が **Merged** になったことを確認してください。マージ権限を有効にした状態やエージェントが実行中であることだけでは、マージ完了の確認になりません。

> [!IMPORTANT]
> Agent Merge は、リポジトリの保護や権限不足を回避しません。続行前に問題を解決してください。

## まとめと次のステップ

コードの生成、テストと検証、プルリクエストの処理など、開発プロセスの複数の部分を自動化しました。具体的には、次の作業を行いました。

- Agent Merge とは何か、マージのライフサイクルをどのように自動化するかを学んだ。
- 機能 PR 全体と検証の根拠を確認した。
- レビュー後にのみ Agent Merge を承認し、PR がマージされたことを確認した。

次は、[既存のキャンバスを使ってトリアージキャンバスを作成し][next-lesson]、エージェントと一緒に作業を確認、計画、視覚化する方法を学びます。

## リソース

- [GitHub Copilot app で issue とプルリクエストを管理する][managing-issues-prs]
- [GitHub Copilot app について][about-copilot-app]

[next-lesson]: ../9-canvases/
[managing-issues-prs]: https://docs.github.com/copilot/how-tos/github-copilot-app/managing-issues-and-pull-requests
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
