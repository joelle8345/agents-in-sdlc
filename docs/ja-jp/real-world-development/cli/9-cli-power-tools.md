---
title: "Lesson 9 - GitHub Copilot CLI のスラッシュコマンド"
description: "コンテキストの管理、モデルの選択、セッションの共有、クラウドへの任意の委任に使うスラッシュコマンドを確認します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

多くの CLI ツールと同様に、GitHub Copilot CLI には操作用のスラッシュコマンドが用意されています。高度な機能、内部情報、追加の構成オプションを利用できます。これまでに `/diff`、`/mcp`、`/skills`、`/agent`、`/pr` などのコマンドを使いました。ここでは、ほかの便利なコマンドをいくつか確認します。

このレッスンでは、次の内容を学びます。

- `/context` と `/compact` を使って、Copilot が会話のコンテキストを管理する方法を確認する。
- `/model` で利用可能なモデルを確認する。
- `/share` でセッションをエクスポートまたは共有する方法を学ぶ。
- 並列作業、worktree、cloud agent への委任に使う任意のコマンドを確認する。

## シナリオ

CLI の中心的なワークフローが完了しました。ここでは、コンテキスト管理、モデルの切り替え、セッションの共有、[Copilot cloud agent][about-cloud-agent] への任意の委任など、追加機能を確認します。

## Copilot CLI のコンテキストを確認する

大規模または複雑なタスクでは、モデルのコンテキストウィンドウの上限に達することがあります。Copilot CLI は必要に応じて会話を自動的に圧縮します。スラッシュコマンドを使えば、状態を確認したり、手動で圧縮したりできます。

1. Codespace に戻り、まだ開いていない場合はリポジトリルートから Copilot CLI を起動します。
2. 次を入力します。

   ```plaintext
   /context
   ```

3. モデル、現在のトークン使用量、システム instruction、ツール、メッセージ、空き領域ごとのコンテキストの内訳を確認します。
4. 会話を圧縮します。

   ```plaintext
   /compact
   ```

5. もう一度 `/context` を入力して結果を比較します。会話が短い場合は、大きな違いがないこともあります。

> [!NOTE]
> Copilot CLI はコンテキストウィンドウがいっぱいになると自動的に圧縮します。タイミングを指定したい場合は `/compact` を使います。関係のないタスクに切り替えて会話を新しくしたい場合は、`/clear` または `/new` を使います。

## モデルを選ぶ

モデルにはそれぞれ異なる強みがあり、開発者によって好みも異なります。Copilot CLI では、利用可能なモデルを一覧表示して選択できます。

1. 次を入力します。

   ```plaintext
   /model
   ```

2. 利用可能なモデルと使用状況を確認します。
3. 現在のモデルを維持するか、別のモデルを選ぶか、<kbd>Esc</kbd> を押して一覧を閉じます。

## セッションを共有する

チームで作業して知見を共有すると、AI ツールの活用方法を互いに改善できます。`/share` コマンドでは、セッションを Markdown または HTML ファイルにエクスポートしたり、共有リンクを作成したり、GitHub gist として公開したりできます。

1. `/help` を入力し、インストール済みのバージョンで利用できる `/share` オプションを確認します。
2. セッションを共有する場合は、ローカルの Markdown にエクスポートする `/share file` など、目的に合った方法を選びます。
3. エクスポートした内容を送信または公開する前に確認します。セッションのエクスポートには、プロンプト、回答、プロジェクトの詳細が含まれる場合があります。

リンクや gist の公開は任意です。チームが共有する予定のないリポジトリや会話の内容は公開しないでください。

## オプション: 作業を拡張または委任する

ワークショップの中心的な内容は完了しました。Copilot CLI には、大きなタスク向けのコマンドもあります。

- `/fleet` は、独立したサブタスクをサブエージェントに分割して並列実行できます。
- `/worktree` は、別のタスク用に分離された Git worktree を作成できます。
- `/delegate` は、非同期に作業し、プルリクエストを作成する場合もある Copilot cloud agent にタスクを送信できます。

これらのコマンドは worktree やリモート作業を追加で作成する可能性があるため、任意です。試す場合は、新しく開始した範囲の明確なタスクを使い、通常のワークフローで結果をレビューしてください。非同期エージェントをさらに詳しく知りたい場合は、[cloud agent ワークショップ][cloud-workshop]に進んでください。

## まとめと次のステップ

Copilot CLI のスラッシュコマンドを使って構成し、セッションを共有し、内部の状態を確認しました。このレッスンでは、次の内容を学びました。

- `/context` と `/compact` を使って、Copilot が会話のコンテキストを管理する方法を確認した。
- `/model` を使って、利用可能なモデルを確認した。
- `/share` でセッションをエクスポートまたは共有する方法を学んだ。
- 並列作業、worktree、cloud agent への委任に使う任意のコマンドを確認した。

Copilot CLI にはほかにも多くのスラッシュコマンドがあります。次は、[これまでの内容と次の手順を振り返り][next-lesson]、このワークショップを締めくくります。

## リソース

- [Copilot CLI のコマンド リファレンス][cli-reference]
- [Copilot CLI のコンテキスト管理][context-management]
- [Copilot cloud agent について][about-cloud-agent]

[previous-lesson]: ../8-create-pull-request/
[next-lesson]: ../10-review/
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[context-management]: https://docs.github.com/copilot/concepts/agents/copilot-cli/context-management
[about-cloud-agent]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-workshop]: ../../cloud/
