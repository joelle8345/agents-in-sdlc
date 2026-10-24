---
title: "Exercise 1 - カスタム instruction (Cloud agent)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: 前提条件][previous-lesson] · [次のレッスン: Copilot cloud agent →][next-lesson]

生成 AI を使うときはコンテキストが重要です。タスクを特定の方法で進めたい場合や、Copilot に知っておいてほしい背景情報がある場合は、そのコンテキストを参照できるようにします。[instruction file][instruction-files] を使うと、何をするかだけでなく、どのように実行するかも Copilot に伝えられます。

この演習では、次の内容を学びます。

- リポジトリのカスタム instruction とパス単位の instruction file を通じて、プロジェクト固有のコンテキスト、コーディングガイドライン、ドキュメント標準が Copilot にどのように渡るかを確認する。
- `.github/copilot-instructions.md` にリポジトリ全体に適用される標準を追加する。

> [!NOTE]
> VS Code や CLI のハーネスとは異なり、この演習では変更前後のプロンプトを実行しません。Copilot cloud agent は GitHub issue に対して非同期に動作するため、影響をリアルタイムで比較しにくいためです。このハーネスの後半で cloud agent が作成したプルリクエストをレビューするときに、instruction file の影響を確認します。

## Instruction file

### シナリオ

Tailspin Toys には、開発プラクティスに関するガイドラインと要件があります。

- データレイヤーには常に単体テストが必要です。
- UI はダークモードにし、モダンな印象にします。
- コードのドキュメントは TSDoc の doc comment として追加します。
- 各ファイルの先頭に、ファイルの役割を説明するコメントブロックを追加します。

instruction file を使い、これらのプラクティスに沿って作業するための情報を Copilot に渡します。

### カスタム instruction

カスタム instruction は、コーディングスタイルや要件を Copilot に伝えるコンテキストと設定です。好みのコーディング規約、ライブラリ、コードに含めるコメントの種類などを指定できます。リポジトリ全体に適用する instruction と、特定のファイル種別に適用する instruction を作成できます。

instruction file は 2 種類あります。

- `.github/copilot-instructions.md` は、リポジトリへの**すべての**リクエストで Copilot に送られる単一の instruction file です。技術スタック、構築中のものの概要、ベストプラクティスなど、ほとんどの会話や CLI リクエストに関係するプロジェクトレベルの情報を記述します。
- `.github/instructions/*.instructions.md` は、特定のタスクやファイル種別に関するガイドラインです。TypeScript や Astro などの言語、UI コンポーネントや単体テストの作成などのタスクに利用できます。

> [!NOTE]
> IDE では、instruction file は Copilot Chat のコード生成にのみ使われ、コード補完や次の編集候補には使われません。
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
> GitHub Copilot を使うプロジェクトには、十分な instruction file を用意することをお勧めします。このプロジェクトには [UI 更新][ui-instructions]や [Astro][astro-instructions]など、さまざまなタスク向けのファイルがあります。
>
> Copilot は instruction file の生成も支援できます。VS Code の **Configure Chat → Generate Agent Instructions** や Copilot CLI の `/init` など、surface によって方法が異なります。該当する場面では、各 surface のレッスンで説明します。
>
> テンプレートや出発点が必要な場合は、instruction file、カスタムエージェントなどを集めた [awesome-copilot][awesome-copilot] を確認してください。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## このプロジェクトのカスタム instruction file を確認する

リポジトリには中核となる `copilot-instructions.md` と、タスクごとの `*.instructions.md` ファイルがあります。エディターまたは GitHub の Web UI で開いて確認します。

1. `.github/copilot-instructions.md` を開きます。
2. プロジェクトの説明と **Agent notes**、**Code standards**、**Scripts**、**Repository Structure** などのセクションを確認します。**Code standards** 内の **GitHub Actions Workflows** のガイダンスも確認してください。これらは Copilot とのすべてのやり取りに適用されます。
3. `.github/instructions` フォルダーを開き、Astro、Drizzle データレイヤー、テストなどの instruction を確認します。
4. `.github/instructions/unit-tests.instructions.md` を開きます。先頭の `applyTo` フィールドは、リポジトリルートからの相対 glob で適用対象を指定します。この例では `**/*.test.ts` などに一致する TypeScript テストファイルが対象です。
5. このプロジェクトの単体テスト作成に特化した instruction を確認します。
6. `.github/instructions/drizzle.instructions.md` を開いて末尾までスクロールし、`unit-tests.instructions.md` などの別の instruction file や既存ファイルへのリンクを確認します。大きな instruction を再利用しやすい小さなファイルに分け、コード生成の参考例を Copilot に示せます。ここに記載されたパスはリポジトリルートではなく、instruction file からの相対パスです。

> [!NOTE]
> `copilot-instructions.md` の **Code formatting requirements** セクションにはコーディング標準が記載されていますが、コード内ドキュメントはまだ必須ではありません。次の手順で TSDoc の doc comment とファイルコメントヘッダーのルールを追加します。

## リポジトリ全体の標準を追加する

この演習で編集するのは、コード内ドキュメントに関するプロジェクト全体のルールを追加する作業です。後続の演習で issue を割り当てると、cloud agent がこのルールを使用します。

編集の前に作業ブランチを準備します。cloud agent は issue の対象ブランチから instruction を読み込みますが、ここでは変更をきちんとコミットします。

1. Codespace のターミナルで新しいブランチを作成して切り替えます。

   ```bash
   git checkout -b custom-instructions-cloud
   ```

`.github/copilot-instructions.md` は Copilot にプロジェクトレベルの情報を提供します。コーディング標準を文書化して、コード提案の質を高めます。

1. `.github/copilot-instructions.md` をもう一度開きます。
2. **Code formatting requirements** セクションを探します。27 行目付近にあります。コーディング標準は記載されていますが、コード内ドキュメントのルールはありません。
3. 既存の標準の直後に、次の Markdown 行を追加し、ファイルコメントヘッダーと TSDoc doc comment を Copilot に指示します。

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. `copilot-instructions.md` を保存します。

> [!TIP]
> instruction file は、リポジトリレベルの `.github/copilot-instructions.md` で全体向けのガイダンスを指定する方法と、特定の言語、ファイル種別、タスク向けの `*.instructions.md` を使う方法があります。今回の doc comment ルールのようにプロジェクト全体に適用する標準は、リポジトリレベルのファイルに記述します。

## instruction の更新をコミット、push、マージする

cloud agent は issue の対象ブランチから instruction file を読み込みます。次の演習では Copilot が `main` からブランチを作成するため、cloud agent が更新内容を使えるように、instruction を `main` に反映します。

1. 変更をステージしてコミットします。

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. ブランチを push します。

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. github.com で `custom-instructions-cloud` から `main` へのプルリクエストを開いてマージします。次の演習で issue を割り当てる際に、cloud agent がこの instruction を読み込みます。

> [!TIP]
> このワークショップで `main` に直接作業する場合は、ブランチの手順を省略して `main` に直接コミットできます。実際のプロジェクトでの作業方法に近づけるため、ここではブランチを使います。

## まとめと次のステップ

このプロジェクトの instruction file から Copilot がコンテキストを取得する方法を確認し、`.github/copilot-instructions.md` にリポジトリ全体の標準を追加しました。このハーネスの後半で cloud agent が作成するプルリクエストをレビューするときに、この標準が使われていることを確認できます。

次は、[最初の issue を Copilot cloud agent に割り当てます][next-lesson]。

## リソース

- [GitHub Copilot のカスタマイズ用 instruction file][instruction-files]
- [カスタム instruction 作成のベストプラクティス][instructions-best-practices]
- [Copilot 向けのカスタム instruction をより良く書くための 5 つのヒント][copilot-instructions-five-tips]
- [Awesome Copilot — instruction file などのリソース集][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
