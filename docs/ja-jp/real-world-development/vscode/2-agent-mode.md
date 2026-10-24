---
title: "Exercise 2 - Copilot Agent Mode で新しい機能を追加する"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

アプリケーションの簡単な更新でも、通常は複数のファイルを変更し、テストなどを実行する必要があります。開発者は必要なファイルを探して変更し、テストを実行し、問題をデバッグし、見落としたファイルを見つけてさらに変更する、といった作業を繰り返します。

このような作業には Copilot エージェントモードが役立ちます。

Copilot エージェントモードは統合開発環境 (IDE) 内でより自律的に動作します。開発者と同じように、既存のプロジェクト構造を調査し、必要な更新を行い、テストなどのタスクを実行し、見つかった問題を自動で修正します。エージェントモードを使って、サイトに新しい機能を追加する方法を確認しましょう。

> [!NOTE]
> 名前は似ていますが、エージェントモードと cloud agent は異なる操作を目的としています。エージェントモードは IDE 内でタスクを実行するため、すばやいフィードバックと対話が可能です。cloud agent はチームメンバーのように非同期で作業し、issue とプルリクエストを通じて開発者とやり取りします。

この演習では、次の方法を学びます。

- Copilot エージェントモードでプロジェクトを調査し、関連ファイルを特定して、連携した変更を行う。
- ユーザーインターフェイス (UI) とデータレイヤーにわたる新機能を実装する。
- コードベースにマージする前に、Copilot が生成した変更とテストをレビューする。

## シナリオ

ゲームの一覧が増えてきたため、カテゴリとパブリッシャーで絞り込めるようにします。前の演習で publishers helper を追加しました。残りのデータレイヤー、UI、テストを Copilot エージェントモードで仕上げます。

## Tailspin Toys の Web サイトを実行する

変更を始める前に、Tailspin Toys の Web サイトを確認して、現在の機能を把握します。

この Web サイトは、開発者向けテーマのボードゲーム用クラウドファンディングプラットフォームです。ゲーム一覧と詳細情報を表示します。単一の Astro アプリであり、ビルド時にページを静的 HTML としてレンダリングします。ページは frontmatter 内で Drizzle ORM を使ってローカルの SQLite データベースを直接参照します。別のバックエンド API やクライアント側 UI フレームワークはありません。再利用可能なデータアクセス helper は `src/lib/` にあり、操作性は標準 Document Object Model (DOM) API を使った小さな Astro `<script>` で追加します。

### Web サイトを起動する

`npm run dev` タスクを使って、単一の Astro 開発サーバーを起動します。GitHub Codespace では次の手順を実行します。

1. Codespace に戻ります。前の演習を終えて `main` にいることを確認します。
2. <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux) を押して、Codespace 内に新しいターミナルを開きます。
3. `main` を更新し、フィルタリング作業用のブランチを作成します。

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. 次のコマンドで Web サイトを起動します。

   ```bash
   npm run dev
   ```

   Astro 開発サーバーの準備ができると、次のような URL を示すバナーが表示されます。

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> `http://localhost:4321` のブラウザーウィンドウを開くダイアログが表示された場合は、**x** を選択して閉じます。

5. ターミナルで <kbd>Command</kbd> (Mac) または <kbd>Ctrl</kbd> (Windows/Linux) を押しながら、Astro サーバーのアドレス `http://localhost:4321` を選択して Web サイトを開きます。

> [!NOTE]
> Codespace のターミナルで localhost の URL を選択すると、`https://<your-codespace-name>-4321.app.github.dev/` に自動的に転送されます。Codespace へのプライベートトンネルを通じて Web サーバーに接続しています。

### Web サイトを確認する

Web サイトが起動したら、機能を確認します。主な機能は次のとおりです。

- **ホームページ**: ボードゲームの一覧とタイトル、画像、説明を表示します。
- **ゲーム詳細ページ**: ゲームを選択すると、タイトル、説明、パブリッシャー、カテゴリなどの詳しい情報が表示されます。

## Copilot でバックログを確認する

> [!TIP]
> **Copilot Chat を開く**
>
> 以下の演習を始める前に Codespace に戻り、Copilot Chat パネルを開き、**New Chat** を選択して新しい会話を開始します。モードとモデルの選択は演習によって異なるため、必要な場面で手順を示します。

Web サイトの初期実装は動作しますが、機能を追加して改善します。テンプレートからプロジェクトを作成したときに、issue のバックログが自動的に用意されています。GitHub Copilot にバックログを表示してもらいます。

1. Chat ビューのエージェントドロップダウンで **Agent** を選択します。**Agent** は複数ファイルにわたる変更を自律的に計画・実装し、ターミナルコマンドやツールを実行できます。

   ![Chat ビューのエージェント選択を示すスクリーンショット](../../../_images/shared-chat-mode-selector.png)

2. 利用可能なモデルの一覧から **Claude Sonnet 4.5** を選択します。

> [!CAUTION]
> このワークショップの作成者が特定のモデルを推奨しているわけではありません。作成時に Claude Sonnet 4.5 を使用したため、説明にも含めています。出力の一貫性を高める意図がありますが、大規模言語モデル (LLM) は確率的に動作するため、提案が説明と異なる場合があります。これは正常な動作です。

> [!NOTE]
> LLM の確率的な性質により、Copilot が別の MCP コマンドを使うことがありますが、タスクは完了できます。

3. 次のプロンプトを Copilot に送信し、issue のバックログについて尋ねます。

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. **Continue** を選択して、すべての issue を一覧表示するコマンドを実行します。
5. 生成された issue の一覧を確認します。

Copilot がユーザーにとって最も役立つと判断した項目を優先順位付けしていることを確認します。

## Instruction file を確認する

コード生成をエージェントに依頼する前に、コンテキストを提供する instruction file を確認します。Web サイトの機能追加に関するガイダンスが記載された [ユーザーインターフェイス (UI) instruction][ui-instructions]を使います。

1. Codespace で `.github/instructions/ui.instructions.md` を開きます。
2. 機能追加の進め方に関するガイダンスを確認します。次の内容が含まれます。
   - アーキテクチャの概要。
   - コンポーネント設計、テスト容易性、アクセシビリティの原則。
   - Astro、Tailwind CSS、Drizzle など、ファイル種別ごとの instruction へのリンク。

> [!TIP]
> instruction file からほかの instruction file やプロジェクト内のファイルを参照できます。パスは instruction file の場所からの相対パスです。これにより、instruction を再利用したり、複雑な内容を管理しやすい単位に分割したり、Copilot に例やテンプレートを提示したりできます。

## フィルタリング機能を実装する

フィルタリング機能を完成させるには、少なくとも次の 3 つの更新が必要です。

- データレイヤー (`src/lib/`) のフィルタリングロジックを追加または調整する。
- フィルタリングの動作に関するテストを追加または更新する。
- ゲーム一覧ページにフィルタリング UI を追加する。

コードベースにマージする前に、テストを実行して成功することも必要です。Copilot エージェントモードに作業を依頼します。

1. Copilot の現在の会話を続けるか、**New Chat** を選択して新しい会話を開始します。
2. **Add Context**、**Instructions**、**ui** の順に選択して、instruction file を指定します。

   ![UI instruction file を選択する例を示すスクリーンショット](../../../_images/ex3-select-instructions-file.png)

3. Chat ビューのエージェントドロップダウンで **Agent** が選択されていることを確認します。

   ![Chat ビューのエージェント選択を示すスクリーンショット](../../../_images/shared-chat-mode-selector.png)

4. モデルとして **Claude Sonnet 4.5** が選択されていることを確認します。
5. バックログの関連 issue に基づいて機能を実装するよう、次のプロンプトを使って Copilot に依頼します。

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. Copilot がプロジェクトを調査し、機能に関連するデータレイヤー helper、UI、テストを探して変更し、テストを実行する様子を確認します。

   ![Copilot がプロジェクトのファイルを調査するスクリーンショット](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot はプロジェクトを調査し、ファイルを変更してテストを実行します。タスクやコードベースの複雑さによって数分かかる場合があります。作業中にコードエディターに **Keep** と **Undo** が表示されることがあります。作業の完了後は、すべての変更に対して **Keep** または **Undo** を選べるため、処理中に選択する必要はありません。

7. Copilot に求められたら、**Continue** を選択してテストを実行します。

   ![Copilot Chat ペインにテストの実行確認ダイアログが表示された画面](../../../_images/ex3-agent-mode-run-tests.png)

8. 作業中に一時停止したり、テストが失敗したりする場合があります。Copilot はタスクが完了し、エラーが検出されなくなるまでコード生成とテストを反復します。

   ![Copilot エージェントモードの完了した Chat セッション](../../../_images/ex3-agent-mode-proposed-changes.png)

9. 生成されたコードに問題がないか確認します。

> [!CAUTION]
> Copilot やほかの AI ツールが生成したコードをレビューすることは常に重要です。

10. Web サイトが起動しているブラウザーに戻り、新機能を確認します。
11. 動作を確認してコードをレビューしたら、Copilot Chat ウィンドウで **Keep** を選択します。

## まとめと次のステップ

GitHub Copilot エージェントモードを使って、Tailspin Toys の Web サイトに機能を追加する方法を確認しました。次のことを学びました。

- GitHub Copilot エージェントモードで UI とデータレイヤーにわたる機能を実装する。
- Copilot エージェントモードでプロジェクトを調査し、関連ファイルを特定して連携した変更を行う。
- コードベースにマージする前に、Copilot が生成した変更とテストをレビューする。

次は、[Playwright MCP サーバーで機能をテストし][next-lesson]、プルリクエストを作成します。

### ボーナスの演習 — ページネーションを実装する

ゲーム一覧が増えると、ページネーションが必要になります。この演習で学んだスキルを使って、Copilot にページネーションを実装してもらいます。次の点を検討してください。

- 既存の instruction file を使うなど、既存のベストプラクティスに従う。
- ページサイズをユーザーが選択できるようにするか、固定値にするかを決める。
- 希望する実装に必要なガイダンスをプロンプトで Copilot に伝える。
- Copilot に変更を依頼してコンテキストを追加するなど、反復が必要になる場合があります。これは Copilot を使った通常の作業方法です。

## リソース

- [Copilot の Ask、Edit、Agent モード: 機能と使い分け][choose-mode]
- [VS Code のエージェントモード][vs-code-agent-mode]

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
