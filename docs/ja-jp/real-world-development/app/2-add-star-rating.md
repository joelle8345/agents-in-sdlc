---
title: "レッスン 2 - 星評価を追加する: 小さな成果"
description: "GitHub Copilot app で最初のエージェントセッションを開始し、ゲームカードに小さな変更を加えて、最初のプルリクエストとしてマージします。"
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

ワークスペースを確認してクイックチャットを試したので、次は**エージェントセッション**を開始し、プロジェクトに最初の変更を加えます。変更は小規模なものにします。ゲームデータには星評価がすでにありますが、ホームページのゲームカードには表示されていません。エージェントに表示を依頼し、変更をレビューして、最初のプルリクエストとしてマージします。

このレッスンでは、次の内容を学びます。

- エージェントセッションを開始し、セッションの構成を学ぶ。
- プロジェクトに小規模で対象を絞った変更を加えるようエージェントに依頼する。
- ワークスペースの差分ビューで変更をレビューする。
- アプリをローカルで実行し、ブラウザーで変更を確認する。
- 最初のプルリクエストを作成してマージする。

## シナリオ

Tailspin Toys の各ゲームには星評価があり、ゲーム詳細ページにはすでに表示されています。一方、ホームページのゲームカードに表示されるのは、タイトル、カテゴリ、パブリッシャー、説明だけです。準備運動として、エージェントに既存の評価を各カードへ表示してもらいます。小規模で完結した、最初のセッションに適した変更です。

## セッションの構成

**セッション**は、独立したワークスペースで実行されるエージェントとの会話です。各セッションには**専用の Git worktree とブランチ**が割り当てられます。そのため、あるセッションで機能を追加しながら、別のセッションでバグを修正しても、変更が競合しません。セッションはリポジトリごとにサイドバーにグループ化されます。選択して切り替えられます。

セッションには、エージェントとの**会話**、ファイルの調査や編集を行うエージェントの**ツール操作**、差分を含む**変更されたファイル**の一覧が表示されます。

## セッションを開始して変更を依頼する

新しいセッションを開始し、プロジェクトを調査して機能を実装します。[アプリのセットアップ][prior-lesson]では、GitHub リポジトリからプロジェクトを追加しました。そのリポジトリのセッションを作成し、変更を依頼します。

1. GitHub Copilot app に戻るか、アプリを開きます。
2. サイドバー上部にある **+** を選択してセッションを開始します。
3. リポジトリに `tailspin-toys` を選択します。
4. プロンプトボックスの下で **new working tree** と **Interactive** モードを選択します。次のプロンプトを使って変更を依頼します。

    ```plaintext
    Show each game's starRating out of 5 in the game cards on the list page. If the rating is null, show "No rating yet". Keep the card layout as it is, add tests, and run the relevant checks.
    ```

5. <kbd>Enter</kbd> を押して、Copilot にプロンプトを送信します。

Copilot app は最初にプロジェクトの分離されたコピーである worktree を作成します。次にプロジェクトを調査し、新機能に必要なファイルを見つけ、コードを作成します。これで Copilot app による機能追加ができました。

## 差分をレビューする

AI が生成した変更は、どれほど小さくてもマージ前にレビューしてください。Copilot app 内で変更を確認します。

1. アプリの右上にある **Toggle review panel** を選択します。開いたパネルで **Changes** を選択し、変更されたファイルと差分を確認します。

    ![Create PR の右側にある Toggle review panel ボタンを矢印で示した GitHub Copilot app の上部ツールバー](../../../_images/app-2-review-panel.png)

2. ゲーム詳細の表示に使う中心的なファイル `GameCard.astro` にコードが追加されていることを確認します。評価がある場合はその値を表示し、`starRating` が `null` の場合は "No rating yet" を表示する、次のような小さなブロックです。

   ```astro
   {game.starRating !== null ? (
       <span class="text-xs font-medium px-2.5 py-0.5 rounded bg-amber-900/60 text-amber-300" data-testid="game-rating">
           ★ {game.starRating} / 5
       </span>
   ) : (
       <span class="text-xs font-medium text-slate-500" data-testid="game-rating-empty">
           No rating yet
       </span>
   )}
   ```

> [!NOTE]
> Copilot はすべての生成 AI ツールと同様に確率的に動作するため、実際のコードは上記と異なる場合があります。ただし、比較的似た実装になります。

## 変更を確認する

ブラウザーを開く前に、エージェントの自動チェック結果を確認します。数値の `starRating` と `null` の場合の代替表示をテストしていることを確認してください。前提条件が不足していたり、チェックがスキップされていたりする場合は成功ではありません。インストールの要求は内容を確認してから承認してください。

コードを読むだけで動作すると判断せず、Copilot に Web サイトを起動してもらい、更新されたユーザーインターフェイス (UI) を確認します。サイトを起動し、ブラウザーキャンバスで開くよう依頼します。

> [!TIP]
> キャンバスは Copilot app 内で利用できるインタラクティブなウィジェットです。後のレッスンでカスタムキャンバスを確認して作成しますが、ここでは組み込みのブラウザーキャンバスを使います。

1. 次のプロンプトを使って、アプリを起動しブラウザーキャンバスでページを開くよう Copilot に依頼します。

    ```plaintext
    Start the app and open it in the browser canvas.
    ```

2. しばらくするとアプリが起動し、Copilot app 内にブラウザーウィンドウが開きます。
3. 評価済みのゲームカードに 5 点満点の評価が表示されることを確認します。
4. 終了したら、次のプロンプトを使って、このセッションで起動した開発サーバーを停止するよう Copilot に依頼します。

    ```plaintext
    Stop the dev server and close the browser canvas.
    ```

## 最初のプルリクエストを作成してマージする

機能を作成できました。新しいコードを既存のコードベースにマージするためのプルリクエスト (PR) を作成します。

1. 右上隅にある **Create PR** を選択します。
2. 求められた場合は **Sign in with your browser** を選択し、画面の指示に従って認証します。
3. リポジトリのポリシーで PR 作成前に対応する issue が必要だと Copilot が説明した場合は、そのプロセスに従うよう確認します。
4. Copilot が PR を作成するまで待ちます。
5. チャットのすぐ上にある **PR** バブルを選択し、レビューペインで PR を開きます。必要に応じてここでレビューします。
6. 準備ができたら **Ready to merge** を選択します。
7. 新しいダイアログで **Merge pull request** を選択し、PR をマージします。

## まとめと次のステップ

GitHub Copilot app で最初の変更をリリースしました。具体的には、次の作業を行いました。

- エージェントセッションを開始し、セッションの構成を学んだ。
- ゲームカードに小規模で対象を絞った変更を加えるようエージェントに指示した。
- ワークスペースの差分ビューで変更をレビューした。
- アプリをローカルで実行し、ブラウザーで星評価を確認した。
- PR 1 を開き、チェックをレビューして、明示的にマージした。

次は、[フィルタリングの issue を起点に Plan モードと Autopilot モードを使い][next-lesson]、より大きな機能を構築します。

## リソース

- [GitHub Copilot app でエージェントセッションを使う][agent-sessions]
- [GitHub Copilot app について][about-copilot-app]
- [GitHub Copilot app で issue とプルリクエストを管理する][managing-issues-prs]

[prior-lesson]: ../1-install-copilot-app/#github-copilot-app-をインストールして構成する
[next-lesson]: ../3-agent-modes/
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
[managing-issues-prs]: https://docs.github.com/copilot/how-tos/github-copilot-app/managing-issues-and-pull-requests
