---
title: "Exercise 2 - GitHub Copilot cloud agent"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 前のレッスン: カスタム instruction][previous-lesson] |
|:--|

技術的負債に悩む組織は少なくありません。未解決のセキュリティ問題、更新が必要なレガシーコード、実装する時間がなくバックログに残り続ける機能リクエストなどがあります。GitHub Copilot cloud agent は、コードの更新や機能追加などを自律的に行います。作業が完了すると、人間の開発者がレビューできるドラフトのプルリクエスト (PR) を作成します。手間のかかるタスクを委任して開発を加速し、開発者がより大きな課題に集中できるようにします。

Copilot cloud agent では、次の内容を確認します。

- コード生成用の環境をカスタマイズする。
- 操作を安全に実行する。
- 範囲を明確に定めた issue の重要性を理解する。
- issue を Copilot に割り当てる。

## シナリオ

Tailspin Toys には、解決したい技術的負債があります。サイトの初期開発を担当した委託先がドキュメントを十分に整備しておらず、アプリケーションにはドキュメントがほとんどありません。まず、アプリケーション内のすべての export 関数に TypeScript documentation (TSDoc) の doc comment を追加します。

また、デザインチームはゲームを見つけやすくしたいと考えています。各ゲームの詳細ページに同じカテゴリの別のゲームを表示し、閲覧者が引き続きゲームを探せるようにします。まだ洗練された実装は必要なく、ユーザー体験 (UX) の受け入れテストに使えるものを希望しています。現在はブロックされていますが、より優先度の高い issue もあります。

どちらも優先順位が下がりやすいタスクです。Copilot cloud agent に割り当てれば、非同期で作業している間、開発者は別の作業に集中できます。その後、Copilot の作業をレビューして期待どおりか確認できます。

## GitHub Copilot cloud agent の概要

[GitHub Copilot cloud agent](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) は、人間の開発者と同じようにバックグラウンドでタスクを実行します。たとえば、[GitHub issue を Copilot に割り当て][assign-issue]る方法があります。割り当てると Copilot は進捗を追跡するドラフトのプルリクエストを作成し、環境を準備して作業を開始します。作業中でも完了後でも、Copilot のセッションを確認できます。提案された解決策のレビュー準備が整うと、プルリクエストで開発者に通知します。

## 範囲を明確に定めた instruction の重要性

GitHub Copilot に魔法はありません。考える作業を省略できるわけではありません。一見簡単な操作も、詳しく見ると複雑さを含みます。[Copilot cloud agent に依頼するタスクの範囲][cloud-agent-best-practices]を慎重に定めてください。AI ペアプログラマーとして扱い、段階的に作業して、学び、試し、必要に応じて調整します。生成 AI を導入しても、ソフトウェア開発の基本は変わりません。

## このリポジトリのカスタム instruction

これまでの演習で、カスタム instruction と Copilot へのガイダンス方法を確認しました。すでにカスタム instruction の演習を完了していれば `.github/copilot-instructions.md` の動作を見ています。未確認の場合は、ここで簡単に目を通してください。Copilot cloud agent に作業を割り当てる前に、リポジトリに含まれる instruction file を読み取り専用で確認し、後から影響を特定できるようにします。

実行中の Codespace があればそこで、なければリポジトリの GitHub Web UI で次のファイルを開きます。

- `.github/copilot-instructions.md` — **Code standards** セクションを確認し、TypeScript の規約と TSDoc doc comment に関する要件を確認します。
- `.github/instructions/unit-tests.instructions.md` — `applyTo` frontmatter を確認します。この instruction は `**/*.test.ts` に適用されます。

次のセクションで **Code lacks documentation** issue を cloud agent に割り当てると、作成されたプルリクエストに TSDoc doc comment、TypeScript の規約、コメントヘッダーが反映されているか確認できます。後の演習で PR をレビューするときにも、あらためて取り上げます。

## Copilot cloud agent 用の開発環境を設定する

コード作成では、誰が作業する場合でも、適切な環境とセットアップスクリプトが必要です。Copilot にタスクを割り当てる場合も同じで、Copilot はソフトウェアエンジニアと同様の作業を行います。

cloud agent は作業環境に [GitHub Actions][github-actions] を使用します。`.github/workflows/copilot-setup-steps.yml` に設定する[専用のセットアップ ワークフロー][setup-workflow]を作成すると、作業開始前に必要な開発ツールと依存関係を用意できます。ラボの進行を円滑にし、環境を学べるよう、事前に設定されています。Node.js、プロジェクトの依存関係、エンドツーエンド (E2E) テスト用のブラウザーバイナリ、単一の Astro アプリ用にマイグレーションとシードが完了した SQLite データベースを Copilot が利用できます。

```yaml
name: "Copilot Setup Steps"

# リポジトリの Actions タブからセットアップ手順をテストできます。
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # 必要な手順に最低限必要な権限を設定します。Copilot の操作には独自のトークンが使われます。
    permissions:
      # セットアップ手順でリポジトリをクローンする場合 (依存関係のインストールなど) は `contents: read` が必要です。クローンしない場合は、手順完了後に Copilot が自動的にクローンします。
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # フロントエンド / アプリのセットアップ (アプリ全体は Astro + Drizzle/libSQL)
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # ビルドとテスト用のローカル SQLite データベースをマイグレーションしてシードします。
      - name: Set up the database
        run: npm run db:setup
```

ほかの GitHub ワークフローファイルと同様の構造ですが、重要な点が 2 つあります。

- `copilot-setup-steps` というジョブが 1 つあります。このジョブは、Copilot がプルリクエストの作業を始める前に GitHub Actions で実行されます。
- `workflow_dispatch` トリガーを指定しています。これにより、リポジトリの **Actions** タブからワークフローを手動実行できます。Copilot の実行を待たず、ワークフローが正常に動くことを確認するのに役立ちます。

## ドキュメントを追加する

ドキュメントの重要性は広く認識されていますが、古い情報が残っていたり、まったく記載されていないプロジェクトもあります。このような技術的負債は放置されやすく、生産性を低下させ、コードベースの保守や新しい開発者の参加を難しくします。Copilot はドキュメントの作成にも適しているため、cloud agent に割り当てます。後の演習で作業をレビューします。

1. 新しいブラウザータブで github.com のリポジトリを開きます。
2. **Issues** タブを選択します。
3. **New issue** を選択して、新しい issue のダイアログを開きます。
4. **Blank issue** を選択して issue を作成します。
5. **Title** に `Code lacks documentation` と入力します。
6. **Description** に次の内容を入力します。

    ```plaintext
    Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
    ```

7. **Create** を選択して issue を作成します。
8. 右側の **Assign to Copilot** を選択して、割り当てダイアログを開きます。

    ![Copilot を issue に割り当てる画面](../../../_images/shared-assign-copilot.png)

9. **Assign** を選択します。
10. **Pull Requests** タブを選択します。
11. 新しく生成されたプルリクエスト (PR) を開きます。タイトルは `[WIP]: Code lacks documentation` のようなものです。一覧に PR が表示されない場合は、少し待ってからブラウザーを更新します。
12. 数分後、Copilot が TODO リストを作成したことを確認します。

> [!NOTE]
> Copilot の TODO リストが PR に表示されるまで数分かかることがあります。Copilot は環境を準備して (前述のワークフローを実行し)、プロジェクトを分析し、問題への取り組み方を決めています。

13. リストと、Copilot が実行するタスクを確認します。
14. プルリクエストのタイムラインを下にスクロールし、Copilot が issue に取り組み始めたことを示す更新を確認します。
15. **View session** ボタンを選択します。

    ![Copilot セッションを表示する画面](../../../_images/ex4-view-session.png)

> [!CAUTION]
> 表示が更新されるまで、ウィンドウを更新する必要がある場合があります。

16. ライブセッションをスクロールし、Copilot の作業を確認します。コードを調査して状態を把握し、計画を検討して、コードを作成する様子が表示されます。

処理には数分かかる場合があります。Copilot cloud agent の主な目的の 1 つは、タスクを非同期で実行して、開発者が別の作業に集中できるようにすることです。この機能を利用して、もう 1 つのタスクを cloud agent に割り当てた後、アプリケーションの機能を追加するコード作成に取り組みます。

## ゲーム詳細ページに関連ゲームのセクションを追加する

GitHub Copilot cloud agent の大きな利点は、作業を分担できることです。デザインチーム向けに関連ゲームのセクションを追加する作業に時間がかからない場合でも、その間に別の作業を進められます。cloud agent に割り当てましょう。

1. github.com のリポジトリに戻ります。
2. **Issues** タブを選択します。
3. **New issue** を選択して、新しい issue のダイアログを開きます。
4. **Blank issue** を選択します。
5. **Title** に `Show related games on the game details page` と入力します。
6. **Description** に次の内容を入力します。

    ```markdown
    We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
    ```

7. **Create** を選択して issue を作成します。
8. 右側の **Assign to Copilot** を選択して、割り当てダイアログを開きます。

    ![Copilot を issue に割り当てる画面](../../../_images/shared-assign-copilot.png)

9. **Assign** を選択します。

ほどなく、最初の issue コメントに 👀 が表示され、Copilot が作業を開始したことがわかります。

![目の絵文字で issue に取り組んでいることを示す Copilot](../../../_images/ex4-issue-eyes-emoji.png)

Copilot は 2 つ目の依頼にも取り組み始めます。Copilot cloud agent はソフトウェアエンジニアと同様に作業するため、常に監視する必要はありません。完了後に確認します。次は、カスタムエージェントの作成と使用に取り組みます。

## まとめと次のステップ

[GitHub Copilot cloud agent][copilot-agents] を使って、issue を Copilot に割り当てて非同期に作業させる方法を確認しました。cloud agent は技術的負債への対応、新機能の作成、別のフレームワークからのコード移行などに利用できます。

このレッスンでは、次の内容を確認しました。

- コード生成用の環境をカスタマイズする。
- 操作を安全に実行する。
- 範囲を明確に定めた issue の重要性を理解する。
- issue を Copilot に割り当てる。

cloud agent がバックグラウンドで作業している間に、カスタムエージェントを作成して使います。[Copilot cloud agent は Model Context Protocol (MCP) サーバーも利用でき][cloud-agent-mcp]、前のモジュールで確認したカスタム instruction も参照します。

## リソース

- [Copilot cloud agent について][copilot-agents]
- [GitHub issue を Copilot に割り当てる][assign-issue]
- [Copilot cloud agent のセットアップ ワークフローのベストプラクティス][cloud-agent-best-practices]

| [次のレッスン: カスタムエージェント →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
