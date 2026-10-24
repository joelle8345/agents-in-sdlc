---
title: "Exercise 3 - Playwright MCP サーバーで機能をテストする"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: エージェントモード][previous-lesson] · [次のレッスン: カスタムエージェント →][next-lesson]

エージェントモードでフィルタリング機能を作成しました。プルリクエストを開く前に、ブラウザーで実際に動作することを確認します。自分でアプリを操作する代わりに **Playwright MCP server** を接続し、Copilot に実際のブラウザーを操作させて機能をテストします。その後、ブランチを公開して PR を作成します。

この演習では、次の内容を学びます。

- Model Context Protocol (MCP) と、MCP サーバーが Copilot にツールを追加する仕組みを学ぶ。
- Playwright MCP サーバーをワークスペースに追加する。
- Copilot にサーバーを使わせ、ブラウザーでフィルタリング機能を手動テストする。
- ブランチを公開し、フィルタリング作業のプルリクエストを開く。

## Model Context Protocol (MCP) とは

エージェントモードは、エディターの外部にアクセスできると、さらに強力になります。Copilot が外部のツールやサービスを利用するための標準的な方法が Model Context Protocol (MCP) です。

![コンテキスト、LLM、MCP サーバーや VS Code 拡張機能が提供するツールとの連携を含む、エージェントモードの仕組みを示す図](../../../_images/ex1-mcp-diagram.png)

[Model Context Protocol (MCP)](https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/) は、AI エージェントが外部のツールやサービスと通信する方法を提供します。MCP を使うと、エージェントはリソースを使って最新情報を取得し、ツールを使って開発者に代わって操作を実行できます。

ツールとリソースには、AI エージェントと外部サービスとの橋渡しをする MCP サーバーを介してアクセスします。MCP サーバーは、既存の API や npm パッケージなどのローカルツールとエージェントとの通信を管理します。各サーバーはエージェントが利用できるツールやリソースのセットを提供します。

既存の MCP サーバーの例を紹介します。

- **[GitHub MCP Server](https://github.com/github/github-mcp-server)**: GitHub リポジトリを管理する API を利用できます。AI エージェントは、リポジトリの新規作成や更新、issue とプルリクエストの管理などを実行できます。
- **[Playwright MCP Server](https://github.com/microsoft/playwright-mcp)**: Playwright を使ったブラウザー自動化機能を提供します。AI エージェントは、Web ページへの移動、フォーム入力、ボタンの選択などを実行できます。

ほかにもさまざまなツールやリソースを提供する MCP サーバーがあります。GitHub はエコシステムの発見と貢献を促進するため、[MCP レジストリ](https://github.com/mcp)を提供しています。

> [!CAUTION]
> セキュリティの観点から、MCP サーバーはプロジェクトのほかの依存関係と同じように扱ってください。使用前にソースコードを慎重に確認し、発行元を検証して、セキュリティへの影響を検討してください。信頼できる MCP サーバーのみを使用し、機密リソースや操作へのアクセス許可には注意してください。

## MCP の構成を確認する

`.vscode/mcp.json` ファイルで、この VS Code ワークスペースで利用できる MCP サーバーを設定します。

1. Codespace で `.vscode/mcp.json` を開きます。
2. 次の `github` サーバーがすでに設定されていることを確認します。

    ```json
    {
      "servers": {
        "github": {
          "type": "http",
          "url": "https://api.githubcopilot.com/mcp/"
        }
      }
    }
    ```

この `github` の設定はプロジェクトテンプレートに含まれているため、前の演習で Copilot が issue のバックログを読み取ることができました。[リモート GitHub MCP サーバー][remote-github-mcp-server]を使うので、ローカルにインストールする必要はありません。VS Code は HTTP で接続し、Copilot が初めてツールを使うときに GitHub で認証します。

## Playwright MCP サーバーを追加する

次に 2 つ目のサーバーを追加します。[Playwright MCP サーバー][playwright-mcp-server]を使うと、Copilot がブラウザーを操作できます。今回の機能をテストするのに適しています。

1. `.vscode/mcp.json` で `github` の隣に `playwright` のエントリを追加し、次の内容にします。

    ```json
    {
      "servers": {
        "github": {
          "type": "http",
          "url": "https://api.githubcopilot.com/mcp/"
        },
        "playwright": {
          "command": "npx",
          "args": ["@playwright/mcp@latest", "--headless"]
        }
      }
    }
    ```

2. ファイルを保存します。

リモートの `github` サーバーと異なり、`playwright` は**ローカル**サーバーです。VS Code は `npx @playwright/mcp@latest` を実行して起動します。`--headless` フラグを指定すると、画面に表示せずにブラウザーを実行します。デスクトップ環境がない Codespace では、この設定が必要です。

> [!NOTE]
> Tailspin Toys プロジェクトは E2E テストで Playwright をすでに使っているため、通常はブラウザーもインストール済みです。Copilot がブラウザーの不足を報告した場合は、`npx playwright install chromium` を実行して再試行するよう依頼します。

## サーバーを起動して信頼する

VS Code は MCP サーバーを**必要に応じて**起動します。Copilot がサーバーのツールを初めて必要としたとき、VS Code はサーバーを起動し、信頼するか確認します。

1. `.vscode/mcp.json` の `playwright` エントリの上に **Start** が表示されます。選択してサーバーを起動し、構成が正しいことを確認します。
2. VS Code からサーバーを信頼するか確認されたら、構成を確認して信頼を選び、サーバーを起動します。

手動で起動する手順は任意です。省略した場合は、次の手順で Copilot がツールを初めて必要としたときに VS Code がサーバーを起動し、信頼を確認します。

## フィルタリング機能をテストする

[Playwright MCP サーバー][playwright-mcp-server]を使うと、Copilot が実際のブラウザーを操作できます。開発者がアプリを操作する代わりに、エージェントがページを開き、移動し、フィルターを適用して、結果を読み取って要約できます。会話を続けたまま機能の動作を確認できます。

Playwright MCP サーバーは、スクリーンショットではなくページの[アクセシビリティ ツリー][playwright-mcp-server]を使って操作します。そのため、エージェントは支援技術と同じように、ボタン、リンク、リスト項目など、ラベル付きの構造化要素を使って判断します。簡単な機能確認が、基本的なアクセシビリティ確認にもなります。

サーバーを接続してアプリを起動した状態で、Copilot に次のプロンプトを送信してフィルタリング機能を操作してもらいます。

```text
Using the Playwright MCP server, open a browser to the running app at http://localhost:4321 and verify the new game filtering feature:

1. Go to the games page and note how many games are listed.
2. Apply a category filter and confirm the list updates to only show games in that category.
3. Clear it, then apply a publisher filter and confirm the list updates to that publisher.
4. Combine a category and a publisher filter and confirm the results respect both.

Report what you observe at each step, and call out anything that does not behave as expected.
```

Copilot は Playwright MCP サーバーを介してブラウザーを起動し、各手順を実行して結果を報告します。issue の受け入れ条件と照らし合わせて内容を確認してください。期待と異なる場合は、追加で質問するか、プルリクエストを開く前にコードの修正を依頼します。

> [!NOTE]
> テスト中はアプリを `http://localhost:4321` で実行しておく必要があります。開発サーバーを停止していた場合は、プロンプトを送る前に再起動してください。Copilot が Playwright MCP サーバーを初めて使用するときにブラウザーのダウンロードが必要になる場合があります。不足を報告したら `npx playwright install chromium` を実行して再試行するよう依頼します。

[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp

## ブランチを公開してプルリクエストを作成する

機能が動作することを確認したので、チームでレビューできるようプルリクエスト (PR) を開きます。最初に `filtering-vscode` ブランチを公開します。

1. Codespace の **Source Control** パネルを開き、Copilot が行った変更を確認します。
2. **+** アイコンを選択して変更をステージします。
3. **Sparkle** ボタンを選択してコミットメッセージを生成します。

   ![Copilot が行った変更を示す Source Control パネル](../../../_images/ex3-source-control-changes.png)

4. **Publish** を選択してブランチをリポジトリに push します。

## プルリクエストを作成する

github.com や GitHub コマンドライン インターフェイス (CLI) など、プルリクエストの作成方法はいくつかあります。GitHub Copilot を使っているので、関連 issue を見つけて関連付けた PR を作成してもらいます。

1. Copilot Chat パネルを開き、**New Chat** を選択して新しいセッションを開始します。
2. Copilot が GitHub ツールを使えるよう、エージェントドロップダウンで **Agent** が選択されていることを確認します。
3. 次のプロンプトで PR を作成するよう Copilot に依頼します。

   ```plaintext
   Find the issue in the repo related to filtering by category and publisher. Create a new pull request for the current branch, and associate it with the correct issue.
   ```

4. Copilot が情報を取得して操作を行うため **Continue** を求めた場合は選択します。GitHub ツールを初めて使うときに GitHub 認証を求められる場合があります。指示に従って許可します。
5. Copilot が issue を検索し、適切なものを見つけて PR を作成したことを確認します。
6. Copilot が生成したリンクを選択して PR をレビューします。ただし、まだマージ**しないでください**。

## まとめと次のステップ

この演習では、次の作業を行いました。

- Model Context Protocol (MCP) と、MCP サーバーが Copilot にツールを追加する仕組みを学んだ。
- Playwright MCP サーバーをワークスペースに追加した。
- リリース前にブラウザーでフィルタリング機能を手動テストするためにサーバーを使った。
- ブランチを公開し、フィルタリング作業のプルリクエストを作成した。

機能の**テスト**に MCP サーバーを使いましたが、MCP は Copilot を拡張する方法の 1 つにすぎません。次は、アクセシビリティレビューなどの作業を効率化する[カスタムエージェントを作成します][next-lesson]。

## リソース

- [MCP とは何か、なぜ話題になっているのか][mcp-blog-post]
- [Microsoft Playwright MCP Server][playwright-mcp-server]
- [GitHub MCP Server][github-mcp-server]
- [GitHub MCP Registry][mcp-registry]
- [VS Code の MCP サーバー][vscode-mcp-config]

[previous-lesson]: ../2-agent-mode/
[next-lesson]: ../4-custom-agents/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[github-mcp-server]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[remote-github-mcp-server]: https://github.blog/changelog/2025-06-12-remote-github-mcp-server-is-now-available-in-public-preview/
[vscode-mcp-config]: https://code.visualstudio.com/docs/agents/reference/mcp-configuration
