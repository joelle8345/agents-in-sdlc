---
title: "Lesson 12 - GitHub Pages でサイトをデプロイする"
description: "GitHub Copilot app を使って Pages ワークフローを構成し、プルリクエストをレビューして、公開された Space Quiz を確認します。"
authors:
  - jamesmontemagno
lastUpdated: 2026-10-12
---

GitHub Pages にデプロイして、Space Quiz を公開しましょう。Copilot はワークフローの準備とデプロイを支援しますが、変更をレビューし、サイトが公開されたことを確認するのは開発者の役割です。

このレッスンでは、次の内容を学びます。

- Copilot に GitHub Pages のデプロイを構成するよう依頼する。
- マージする前に、ワークフローとプルリクエストをレビューする。
- デプロイを追跡し、公開されたサイトを確認する。

## シナリオ

Space Quiz はすでに GitHub リポジトリにありますが、試してもらうには簡単な方法が必要です。単一ファイルのサイトを GitHub Pages で公開すると、サーバーやランタイム依存関係を追加せずに、公開先のアドレスからアクセスできるようになります。

## Copilot にサイトのデプロイを依頼する

`space-quiz` の Copilot app セッションで、次のプロンプトを送信します。

```plaintext
Enable GitHub Pages for this repository. Create a GitHub Actions workflow that builds the website if needed and deploys it to GitHub Pages. Add a README describing the app and how to run it locally if one does not already exist. Create a pull request with these changes and merge it after required checks pass. Monitor the deployment until it succeeds, then report the final URL of the live website. If you lack permission to enable Pages or merge, tell me exactly what I need to approve or do; do not report success until the site is live.
```

![マージ済みの space-quiz プルリクエスト、Build website・Upload artifact・Deploy to Pages の各ステップが成功した GitHub Actions の Deploy website 実行、yourname.github.io/space-quiz/ に公開された Space Quiz の3段階を示す図。](../../../_images/first-steps-app-pages-deploy.svg)

> [!WARNING]
> このプロンプトは、エージェントにプルリクエストの作成とマージ、およびリポジトリの Pages 設定の変更を依頼します。続行する前に、差分、デプロイ権限、GitHub の承認要求を確認してください。

## ワークフローをレビューしてデプロイを確認する

ワークフローの変更を確認し、サイトが利用可能になるまでデプロイを追跡します。

1. README は、リポジトリにまだ存在しない場合にのみ追加されていることを確認します。
2. ワークフローのビルド手順とデプロイ手順を含め、プルリクエストの変更をレビューします。
3. 必須のプルリクエストチェックが成功してからマージします。
4. GitHub Actions のデプロイ実行が成功するまで追跡します。
5. 報告された URL を開き、Space Quiz が表示されることを確認します。

エージェントが Pages を有効化できない場合やプルリクエストをマージできない場合は、提示された具体的な手順に従ってください。デプロイが成功し、公開サイトが表示されるまでは完了とみなさないでください。

## まとめと次のステップ

Space Quiz が公開され、エージェントの報告だけに頼らずデプロイを確認できました。次は、[レッスン 13「振り返りと次のステップ」][next-lesson]に進みます。

[next-lesson]: ../13-review/
