---
title: "Lesson 8 - 機能の PR を作成してマージする"
description: "フィルタリング、instruction、スキルの更新、QA プロファイル、テストをまとめてレビューし、PR を作成して Agent Merge を使います。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

フィルタリングの実装、instruction の更新、スキルの更新、品質保証 (QA) プロファイル、テストは、1 つのブランチに保存されています。まとめてレビューしてプルリクエストを作成しましょう。星評価のプルリクエスト (PR) は手動でマージしましたが、今回は **Agent Merge** にプロセスを管理させます。

> [!NOTE]
> 通常は、機能、instruction の更新、スキルの更新、QA エージェントをいくつかの PR に分けます。ワークショップを簡潔にするため、フィルタリングと品質確認の作業全体を 1 つの会話とブランチで進め、この PR にまとめます。

このレッスンでは、次の内容を学びます。

- Agent Merge とは何か、マージのライフサイクルをどのように自動化するかを学ぶ。
- 機能変更全体と検証の根拠を確認する。
- フィルタリングの PR を作成する。
- レビュー後にのみ Agent Merge を有効にして、PR がマージされたことを確認する。

## シナリオ

フィルタリング機能の作業を通じて、Copilot を使って機能を計画、実装、検証しました。Tailspin Toys では、マージの承認を開発者が管理しながら、PR に関する残りの作業を自動化します。

## Agent Merge の概要

**Agent Merge** は、プルリクエストをマージするために必要な残りの作業を自動化します。有効にすると、Copilot は PR を妨げている問題 (失敗した継続的インテグレーション (CI) チェックの修正、レビューコメントへの対応、必要に応じたリベースなど) に取り組み、リポジトリで許可されていれば GitHub の自動マージを有効にします。

これまでは開発者自身が **Merge pull request** を選択しました。Agent Merge にその作業を任せることもできますが、有効にする前に変更をレビューし、マージの準備が整っていることを確認してください。

## Agent Merge で PR を管理する

コードを作成したので、まとめてレビューして PR を作成し、残りのプロセスを Agent Merge に任せます。

1. Codespace に戻ります。
2. `/agent` を入力してエージェントダイアログを開きます。
3. 選択肢から **Default** を選び、<kbd>Enter</kbd> を押します。
4. `/pr create` を入力して PR を作成します。
5. `/pr agentmerge` を入力して Agent Merge を有効にします。
6. Copilot が PR の継続的インテグレーションを監視します。すべてのチェックが成功すると、マージが実行されます。
7. Copilot が「PR #14 was squash-merged successfully.」のようなメッセージを表示することを確認します。

> [!IMPORTANT]
> Agent Merge は、必須の承認、ブランチ保護、マージキュー、リポジトリの設定、権限不足を回避しません。処理がブロックされた場合は、報告された理由を確認し、リポジトリで許可されている方法でレビュー済みの変更を手動でマージしてください。

## まとめと次のステップ

コードの生成、テストと検証、プルリクエストの処理など、開発プロセスのいくつかの部分を自動化しました。具体的には、次の作業を行いました。

- Agent Merge とは何か、マージのライフサイクルをどのように自動化するかを学んだ。
- 機能変更全体と検証の根拠を確認した。
- フィルタリングの PR を作成した。
- レビュー後に Agent Merge を有効にし、PR がマージされたことを確認した。

次は、[コンテキスト、モデル、共有、任意のクラウド委任に役立つ Copilot CLI のスラッシュコマンド][next-lesson]を確認します。

## リソース

- [Copilot CLI でプルリクエストを管理する][manage-prs]
- [Copilot CLI のコマンド リファレンス][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
