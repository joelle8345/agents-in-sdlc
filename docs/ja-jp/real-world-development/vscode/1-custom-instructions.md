---
title: "Exercise 1 - カスタム instruction (VS Code)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: 前提条件][previous-lesson] · [次のレッスン: エージェントモード →][next-lesson]

生成 AI を使うときはコンテキストが重要です。タスクを特定の方法で進めたい場合や、Copilot に知っておいてほしい背景情報がある場合は、そのコンテキストを参照できるようにします。Copilot に特定のコンテキストを渡す方法はいくつかあります。重要な方法の 1 つは、コード生成のガイダンスを提供する [instruction file][instruction-files] です。

この演習では、次の内容を行います。

- リポジトリのカスタム instruction とパス単位の instruction file を通じて、プロジェクト固有のコンテキスト、コーディングガイドライン、ドキュメント標準が Copilot にどのように渡るかを確認する。
- *現在の* instruction を使い、フィルタリングの最初のデータスライス (publishers helper) を生成する。
- `.github/copilot-instructions.md` にリポジトリ全体に適用される標準を追加する。
- 同じプロンプトを再実行し、新しい標準が生成コードに反映されることを確認する。
- instruction の更新とフィルタリングのスライスを `main` にコミットし、次の演習で Copilot が更新したガイダンスを使えるようにする。

> [!CAUTION]
> 生成されたコードが、設定した標準から外れる場合があります。Copilot は非決定的です。この演習の目的は、instruction の更新後に動作の傾向がどう変わるかを確認することであり、出力を一字一句一致させることではありません。

## Instruction file

### シナリオ

Tailspin Toys には、開発プラクティスに関するガイドラインと要件があります。

- データレイヤーには常に単体テストが必要です。
- ユーザーインターフェイス (UI) はダークモードにし、モダンな印象にします。
- コードのドキュメントは TSDoc の doc comment として追加します。
- 各ファイルの先頭に、ファイルの役割を説明するコメントブロックを追加します。

instruction file を使い、これらのプラクティスに沿って作業するための情報を Copilot に渡します。

### カスタム instruction

カスタム instruction は、コーディングスタイルや要件を Copilot に伝えるコンテキストと設定です。好みのコーディング規約、ライブラリ、コードに含めるコメントの種類などを指定できます。リポジトリ全体に適用する instruction と、特定のファイル種別に適用する instruction を作成できます。

instruction file は 2 種類あります。

- `.github/copilot-instructions.md` は、リポジトリへの**すべての**リクエストで Copilot に送られる単一の instruction file です。技術スタック、構築中のものの概要、ベストプラクティスなど、ほとんどの会話や CLI リクエストに関係するプロジェクトレベルの情報を記述します。
- `.github/instructions/*.instructions.md` は、特定のタスクやファイル種別に関するガイドラインです。TypeScript や Astro などの言語、UI コンポーネントや単体テストの作成などのタスクに利用できます。

> [!NOTE]
> 統合開発環境 (IDE) では、instruction file は Copilot Chat のコード生成にのみ使われ、コード補完や次の編集候補には使われません。
>
> Copilot Chat、Copilot CLI、Copilot cloud agent は、コード生成時にリポジトリレベルの instruction file と `applyTo` frontmatter を含む `*.instructions.md` ファイルの両方を使用します。
>
> Copilot は [ほかの標準形式の instruction file][custom-instructions-support] もサポートしており、AGENTS.md と CLAUDE.md も利用できます。

### Instruction file を管理するためのベストプラクティス

instruction file の作成について詳しく扱うことは、このワークショップの範囲外です。サンプルプロジェクトの例は、一般的なアプローチを示しています。

- `copilot-instructions.md` には、構築するものの説明、プロジェクト構造、コーディング標準など、プロジェクトレベルのガイダンスを記述します。
- `*.instructions.md` ファイルは、単体テスト、Astro コンポーネント、データレイヤーなどのファイル種別や、特定のタスク向けの instruction に使用します。
- 自然言語で明確に記述し、望ましいコードと望ましくないコードの例を示します。

instruction file の作成方法にも、AI の使い方にも唯一の正解はありません。試しながらプロジェクトに合う方法を見つけてください。

> [!TIP]
> GitHub Copilot を使うプロジェクトには、十分な instruction file を用意することをお勧めします。このプロジェクトには [UI 更新][ui-instructions]や [Astro][astro-instructions]など、多くの種類のタスク向けのファイルがあります。
>
> Copilot は instruction file の生成も支援できます。VS Code の **Configure Chat → Generate Agent Instructions** や Copilot CLI の `/init` など、surface によって方法が異なります。該当する場面では、各 surface のレッスンで説明します。
>
> テンプレートや出発点が必要な場合は、instruction file、カスタムエージェントなどを集めた [awesome-copilot][awesome-copilot] を確認してください。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## このプロジェクトのカスタム instruction file を確認する

このリポジトリに含まれる instruction file を確認します。中心となる `copilot-instructions.md` が 1 つあり、タスク別の `*.instructions.md` ファイルが複数あります。エディターまたは GitHub の Web UI で開きます。

1. `.github/copilot-instructions.md` を開きます。
2. プロジェクトの簡単な説明と **Agent notes**、**Code standards**、**Scripts**、**Repository Structure** などのセクションを確認します。**Code standards** 内の **GitHub Actions Workflows** のガイダンスも確認してください。これらは Copilot とのすべてのやり取りに適用されます。
3. `.github/instructions` フォルダーを開き、Astro ファイル、Drizzle データレイヤー、テストなどの instruction を確認します。
4. `.github/instructions/unit-tests.instructions.md` を開きます。先頭の `applyTo` フィールドは、リポジトリルートからの相対 glob で適用対象を指定します。この例では `**/*.test.ts` などに一致する TypeScript テストファイルが対象です。
5. このプロジェクトの単体テスト作成に特化した instruction を確認します。
6. `.github/instructions/drizzle.instructions.md` を開いて末尾までスクロールし、`unit-tests.instructions.md` などの別の instruction file や既存ファイルへのリンクを確認します。大きな instruction を再利用しやすい小さなファイルに分け、コード生成時に Copilot が参考にできる例を示せます。ここに記載されたパスはリポジトリルートではなく、instruction file からの相対パスです。

> [!NOTE]
> `copilot-instructions.md` の **Code formatting requirements** セクションにはコーディング標準が記載されていますが、コード内ドキュメントはまだ必須ではありません。次の手順で TSDoc の doc comment とファイルコメントヘッダーのルールを追加します。

## 変更用のブランチを作成する

変更作業用にブランチを作成します。

1. 前の演習で使った Codespace に戻ります。
2. <kbd>Control</kbd>+<kbd>`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux) を押して、新しいターミナルを開きます。
3. 新しいブランチを作成して切り替えます。

   ```bash
   git checkout -b custom-instructions
   ```

## instruction を更新する*前に* Copilot Chat を使う

> [!TIP]
> **Copilot Chat を開く**
>
> 以下の演習を始める前に Codespace に戻り、Copilot Chat パネルを開き、**New Chat** を選択して新しい会話を開始します。モードとモデルの選択は演習によって異なるため、必要な場面で手順を示します。

カスタム instruction の影響を確認するため、まず現在の instruction を使ってプロンプトを送ります。その後、instruction を更新して同じプロンプトを再送します。

1. 前の演習で開いたエディタータブを閉じ、Copilot が必要なコンテキストだけを参照できるようにします。
2. `src/lib/publishers.ts` を開き、helper の配置場所を Copilot に示します。
3. Chat ビューのエージェントドロップダウンで **Agent** を選び、Copilot がファイルを変更できるようにします。

   ![Chat ビューのエージェント選択を示すスクリーンショット](../../../_images/shared-chat-mode-selector.png)

4. 次のプロンプトを送信します。

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

5. Copilot がプロジェクトを調査し、コードを更新します。helper ファイルとテストに変更が及ぶ場合もあります。
6. 提案された helper が、最初の引数として `db` クライアントを受け取り、型付きの publisher 配列を返す関数であることを確認します。これは `src/lib/*.ts` に適用される `.github/instructions/drizzle.instructions.md` のデータレイヤー規約によるものです。
7. 提案されたコードに TSDoc doc comment とファイルレベルのコメントヘッダーが**ない**ことを確認します。

> [!CAUTION]
> Copilot は確率的に動作するため、指示がなくても doc comment を追加することがあります。その場合も問題ありません。instruction 更新後に一貫性が向上することが重要です。

## リポジトリ全体の標準を追加する

`.github/copilot-instructions.md` は Copilot にプロジェクトレベルの情報を提供します。コーディング標準を文書化して、コード提案の質を高めます。

1. `.github/copilot-instructions.md` をもう一度開きます。
2. **Code formatting requirements** セクションを探します。27 行目付近にあります。既存のコーディング標準は記載されていますが、コード内ドキュメントのルールがないことを確認します。これが、先ほど生成された helper に doc comment がなかった理由です。
3. 既存の標準の直後に、次の Markdown 行を追加します。

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. `copilot-instructions.md` を保存します。

> [!TIP]
> 前のレッスンで確認したとおり、instruction file は全体向けのガイダンスを指定するリポジトリレベルの `.github/copilot-instructions.md` と、特定の言語、ファイル種別、タスク向けの `*.instructions.md` に分けられます。今回追加した doc comment ルールのようなプロジェクト全体の標準は、リポジトリレベルのファイルに記述します。

## プロンプトを再実行して変化を確認する

1. Copilot Chat に戻り、**New Chat** を選択してコンテキストをクリアします。
2. `src/lib/publishers.ts` を選択し、Copilot が対象ファイルに注目するようにします。
3. 先ほどと**同じプロンプト**を送信します。

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

4. 提案されたファイルの先頭に、次のようなコメントブロックがあることを確認します。

   ```typescript
   /**
    * Publisher data-access helpers for the Tailspin Toys Crowd Funding platform.
    * Provides functions to retrieve publisher information from the database.
    */
   ```

5. 提案された関数に、次のような TSDoc コメントがあることを確認します。

   ```typescript
   /**
    * Returns a list of all publishers with their id and name.
    *
    * @param db - The Drizzle database client.
    * @returns A promise that resolves to an array of publisher objects.
    */
   ```

Copilot に新しいプロジェクト標準を適用し、次の演習の基礎となる実際のコードに反映できました。

## instruction とブランチをコミットして push する

instruction file も、ほかのリポジトリアセットと同様にソース管理します。変更をコミットし、ブランチをリポジトリに push します。

1. <kbd>Control</kbd>+<kbd>`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux) を押して、新しいターミナルを開きます。
2. ターミナルで次のコマンドを実行し、instruction と helper の変更を確認します。

   ```bash
   git status
   ```

3. ターミナルで instruction と helper の基礎に関する変更をステージしてコミットします。

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # git status にテストなどの関連変更が表示された場合は、それらのファイルも追加します。
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

4. ブランチをリポジトリに push します。

   ```bash
   git push -u origin custom-instructions
   ```

## プルリクエストを作成してマージする

ブランチを push したら、バックログにあるドキュメント標準の issue に関連付けたプルリクエストを作成します。手動で作成する代わりに、接続済みの GitHub ツールを使って Copilot に issue を探してもらい、issue を解決する PR を作成してマージします。

> [!NOTE]
> この演習では初めて Copilot に GitHub 上の操作を依頼します。プロジェクトテンプレートには GitHub ツールがすでに設定されているため、セットアップは不要です。Copilot がツールを初めて使うときに VS Code から GitHub へのサインインを求められる場合があります。画面の指示に従って許可してください。後の演習で、この接続に使う Model Context Protocol (MCP) の仕組みを確認します。

1. Codespace 内で Copilot Chat を開きます。
2. <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd> (Windows/Linux) を押して Copilot Chat ビューを開き、エージェントピッカーで **Agent** が選択されていることを確認します。
3. instruction file の更新に関連する issue を探し、現在のブランチから PR を作成するよう Copilot に依頼します。PR には instruction の更新と、今後のフィルタリング作業に向けた publishers helper の基礎の両方を記載します。

   ```
   Find the issue related to updating the instructions file. Create a new PR from the current branch, highlight that the PR closes that issue, and include that we also added the publishers helper foundation for the upcoming filtering work.
   ```

4. Copilot が issue を探して PR を作成するまで待ちます。
5. GitHub 操作を許可するよう Copilot に求められたら、コマンドを確認して適切に **Allow** を選択します。
6. PR が作成されたら、次のプロンプトでマージし、ローカルのブランチを `main` に戻すよう Copilot に依頼します。

   ```
   Merge the PR into main. Then return to main locally, and pull the latest code so we are up to date.
   ```

7. GitHub 操作とシェルコマンドを許可するよう求められたら、コマンドを確認して適切に **Allow** を選択します。

GitHub Copilot の支援を使ってプルリクエストを作成し、マージできました。

## まとめと次のステップ

このプロジェクトで Copilot が instruction file からコンテキストを取得する方法を確認し、VS Code の Copilot Chat を使って次の作業を行いました。

- *既存の* instruction を使ってコード生成プロンプトを送り、Copilot の出力を確認した。
- `.github/copilot-instructions.md` にリポジトリ全体に適用される標準を追加した。
- 同じプロンプトを再実行し、提案されたコードに新しい標準が反映されることを確認した。
- instruction の更新と helper の基礎を `main` にコミットし、次の演習で作業を引き継げるようにした。

次は、[エージェントモード][next-lesson]を使い、コードベース全体にわたる新機能の追加に取り組みます。

## リソース

- [GitHub Copilot のカスタマイズ用 instruction file][instruction-files]
- [カスタム instruction 作成のベストプラクティス][instructions-best-practices]
- [Copilot 向けのカスタム instruction をより良く書くための 5 つのヒント][copilot-instructions-five-tips]
- [GitHub Copilot の個人用カスタム instruction][personal-instructions]
- [Awesome Copilot — instruction file などのリソース集][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
