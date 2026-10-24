---
title: "Lesson 1 - GitHub Copilot CLI をインストールする"
description: "Codespace に Copilot CLI をインストールして認証し、基本操作を確認して、用意されたフィルタリングの issue を見つけます。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

[GitHub Copilot CLI][about-copilot-cli] は、ターミナルで動作する強力なエージェント型コーディングアシスタントです。コードベースの調査、コード生成、コマンド実行、外部ツールとの連携をすべてコマンドラインから行えます。タスクを任せたり、変更を依頼したりしながら、集中を保って作業できます。最初のステップとして、使い慣れたツールを使って Copilot CLI をインストールします。

このレッスンでは、次の内容を行います。

- npm を使って GitHub Copilot CLI をインストールする。
- GitHub アカウントで認証する。
- ワークショップのリポジトリを信頼し、簡単な会話を試す。
- 組み込みの GitHub Model Context Protocol (MCP) サーバーでフィルタリングの issue を見つける。

## シナリオ

チームでは、増え続けるバックログに対応するために AI エージェントを使い始めています。Copilot CLI はその機能を、多くの開発者が使い慣れているターミナルに提供します。このレッスンでは、インストールと認証を済ませ、残りのワークショップで使えるようにします。

## Copilot CLI をインストールする

Copilot CLI は [npm][install-cli]、WinGet、Homebrew でインストールできます。GitHub Codespaces には Node.js があらかじめインストールされているため、ここでは npm を使います。

1. Codespace に戻り、ターミナルを開きます。
2. Node.js がインストールされ、必要なバージョンを満たしていることを確認します。

   ```bash
   node --version
   ```

   バージョン 24 以上が表示されます。

3. Copilot CLI をグローバルにインストールします。

   ```bash
   npm install -g @github/copilot
   ```

4. インストールを確認します。

   ```bash
   copilot --version
   ```

   バージョン番号が表示されます。

## GitHub で認証する

初回起動時に、Copilot CLI は GitHub アカウントでの認証を求めます。

1. Copilot CLI を起動します。

   ```bash
   copilot
   ```

2. 認証を求められたら、device code の手順に従って Copilot CLI を認証し、許可します。
3. Copilot CLI に次のプロンプトが表示されます。

   ```plaintext
   Copilot can read files in this folder and, with your permission, edit them or run code and shell commands. It will remember your permissions for the rest of this session.

   Do you trust the files in this folder?
   ```

4. パスが Tailspin Toys リポジトリであることを確認し、**Yes, and remember this folder for future sessions** を選択して信頼します。

> [!NOTE]
> Codespace では、GitHub セッションを通じてすでに認証されている場合があります。Copilot CLI が認証を求めずに起動した場合は、そのまま進めて問題ありません。

## 基本操作を確認する

通常のシェルプロンプトで実行するコマンドは、Codespace 上で直接実行されます。Copilot CLI の起動後は、自然言語がエージェントに送られ、スラッシュコマンドで会話を操作します。

1. `/model` を入力し、矢印キーで **Auto** を選択して <kbd>Enter</kbd> を押します。確認のため、もう一度 <kbd>Enter</kbd> を押します。
2. `/help` を入力してインストール済みのバージョンで利用できるコマンドを確認し、<kbd>Esc</kbd> を押してヘルプ画面を閉じます。
3. Copilot に簡単な質問をして、動作を確認します。

   ```plaintext
   What are the key files in this project?
   ```

4. 回答を読み、Copilot がリポジトリを調査してから答えることを確認します。
5. `/mcp list` を入力し、組み込みの GitHub MCP サーバーを利用できることを確認します。
6. 次のプロンプトでフィルタリングの issue を探します。

   ```plaintext
   Using GitHub MCP, find the issue in this repository titled "Allow users to filter games by category and publisher." Give me its URL and a short summary. Don't change anything.
   ```

7. URL を開いて issue を読みます。簡単な最初の変更を終えた後に使用します。

> [!TIP]
> 通常の Copilot CLI セッションは、ターミナルで現在チェックアウトしているブランチを使います。自動的に worktree を作成するわけではありません。変更の前に機能ブランチを作成します。

## ワークショップ用のショートカットを使う

Copilot CLI は通常、設定済みの権限を超えるツールの使用前に確認を求めます。このワークショップでは、Codespace 内で `--yolo` を使って再起動し、承認プロンプトを省略します。

> [!CAUTION]
> `--yolo` は完全な自動権限 (`--allow-all-tools`、`--allow-all-paths`、`--allow-all-urls`) を有効にします。Codespace や VM などの分離された環境でのみ使用し、日常の開発で使う既定の alias にしないでください。詳細は[ツール使用の許可と拒否][allow-all-warning]を参照してください。

このワークショップでは `--enable-all-github-mcp-tools` を使って、後のレッスンで issue やプルリクエストを操作するための GitHub MCP 読み取り / 書き込みツールを有効にします。Codespace によってローカルコンピューターへのアクセスは制限されますが、認証済みの GitHub リソースは実際のものです。公開やマージの前に変更をレビューしてください。

1. `/exit` を入力して Copilot CLI を終了します。
2. リポジトリルートから再起動します。

   ```bash
   copilot --yolo --enable-all-github-mcp-tools
   ```

3. もう一度プロジェクトについて簡単な質問をして会話の動作を確認し、`/exit` で終了します。

Copilot は会話を自動的に保存します。後のレッスンで instruction を変更したりエージェントを追加したりした後、`copilot --resume` を使って同じ機能の会話とブランチに戻ります。

## まとめと次のステップ

このレッスンでは、次の作業を行いました。

- npm を使って GitHub Copilot CLI をインストールした。
- GitHub アカウントで認証した。
- ワークショップのリポジトリを信頼し、簡単な会話を試した。
- 組み込みの GitHub MCP サーバーでフィルタリングの issue を見つけた。

次は、[最初の小さな変更を開始し][next-lesson]、Copilot CLI でゲームカードに星評価を表示します。

## リソース

- [GitHub Copilot CLI のインストール][install-cli]
- [GitHub Copilot CLI について][about-copilot-cli]
- [Copilot CLI のコマンド リファレンス][cli-reference]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-add-star-rating/
[install-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/set-up-copilot-cli/install-copilot-cli
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[allow-all-warning]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli#allowing-and-denying-tool-use
