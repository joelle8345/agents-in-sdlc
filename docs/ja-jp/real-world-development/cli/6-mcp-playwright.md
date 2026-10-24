---
title: "Lesson 6 - Playwright MCP で機能を検証する"
description: "Copilot CLI で Playwright MCP を確認または構成し、ブラウザーでフィルタリング機能を調べます。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

すでに説明したとおり、コードを書くことは開発作業の一部にすぎません。データや外部サービスを扱い、Copilot で追加の自動化を利用できるようにする必要があります。ここで MCP サーバーが役立ちます。MCP サーバーを使うと、Copilot は CLI に組み込まれた機能を超えて、さらに多くのツールやサービスを利用できます。

このレッスンでは、次の内容を学びます。

- Model Context Protocol (MCP) と Copilot CLI での使われ方を理解する。
- まだ利用できない場合は Playwright MCP サーバーを追加する。
- エージェントにブラウザーを操作させて、フィルタリング機能を確認する。

## シナリオ

単体テストと E2E テストは重要ですが、UI の更新を検証するには、実際に UI を操作する必要があります。Copilot がユーザーと同じように作業中の Web サイトを利用できれば、変更が期待どおりに動作するという確信を高め、変更作業をさらに自動化できます。

## Model Context Protocol (MCP) とは

[Model Context Protocol (MCP)][mcp-blog-post] は、AI エージェントが外部のツールやサービスと通信するための方法を提供します。MCP を使うと、エージェントは外部のツールやサービスとリアルタイムに通信し、最新情報にアクセスして、開発者に代わって操作を実行できます。

ツールやリソースには、AI エージェントと外部サービスとの橋渡しをする MCP サーバーを介してアクセスします。各 MCP サーバーは、エージェントが利用できるツールやリソースのセットを提供します。

既存の MCP サーバーの例を紹介します。

- **[GitHub MCP Server][github-mcp]**: GitHub リポジトリ、issue、プルリクエストを管理する API を利用できます。
- **[Playwright MCP Server][playwright-mcp-server]**: Playwright を使ったブラウザー自動化機能を提供します。

ほかにも多数の MCP サーバーがあります。GitHub はエコシステムの発見と貢献を促進するため、[MCP レジストリ][mcp-registry]を提供しています。

> [!CAUTION]
> MCP サーバーは、プロジェクトのほかの依存関係と同じように扱ってください。利用前にソースコードを確認し、発行元を検証して、セキュリティへの影響を検討してください。

## Playwright MCP サーバーを追加する

Playwright MCP サーバーがまだ利用できない場合は追加し、Copilot がユーザーと同じように Web サイトを操作できるようにします。

> [!NOTE]
> Copilot CLI ですでに Playwright MCP が構成されている場合は、セットアップ手順を省略して次のセクションに進みます。

1. Codespace に戻ります。
2. Copilot CLI で次のコマンドを入力して、MCP サーバーの追加ダイアログを開きます。

   ```plaintext
   /mcp add
   ```

3. 名前に `playwright` と入力して、<kbd>Tab</kbd> を押します。
4. <kbd>Enter</kbd> を押してサーバーの種類が **STDIO** であることを確認し、<kbd>Tab</kbd> を押します。
5. **Command** ダイアログに次の内容を貼り付けます。

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

6. <kbd>Control</kbd>+<kbd>S</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>S</kbd> (Windows/Linux) を押して、新しい MCP サーバーを保存します。
7. <kbd>Esc</kbd> を押して MCP ダイアログを閉じます。

## Playwright を使って機能を調べるよう Copilot に依頼する

これまでは機能が期待どおりに動作することを手動で確認しました。次は、Copilot で利用できる Playwright MCP サーバーを使って同じ確認を行います。

1. 次のプロンプトを使い、Playwright MCP サーバーで機能を検証するよう Copilot に伝えます。

   ```plaintext
   Start the app and use Playwright MCP to check filtering against the issue and our plan. Tell me what works and what doesn't, without making changes. Stop the server you started when you're done.
   ```

> [!NOTE]
> 通常は Copilot が MCP サーバーを自動的に判断するため、使用を明示する必要はありません。ただし、使用するサーバーがわかっている場合は伝えておくと、結果の一貫性を高め、トークンを節約できます。

2. Copilot がブラウザーで機能を確認するために実行する手順を見ます。
3. レポートを読み、すべてが想定どおりに動作することを確認します。

Copilot はサーバーを起動し、Playwright で Web サイトを操作して、サーバーを停止した後に結果を報告します。

## まとめと次のステップ

Copilot CLI から Playwright MCP サーバーを使い、実際のブラウザーで機能を確認しました。ここでは次の作業を行いました。

- Model Context Protocol (MCP) と Copilot CLI での使われ方を学んだ。
- まだ利用できない場合に Playwright MCP サーバーを追加した。
- エージェントにブラウザーを操作させて、フィルタリング機能を確認した。

次は、[QA カスタムエージェントを作成し][next-lesson]、スキルとブラウザーツールを専門的な役割にまとめます。

## リソース

- [MCP とは何か、なぜ話題になっているのか][mcp-blog-post]
- [Microsoft Playwright MCP Server][playwright-mcp-server]
- [Copilot CLI に MCP サーバーを追加する][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
