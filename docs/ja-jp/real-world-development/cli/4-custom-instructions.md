---
title: "Lesson 4 - カスタム instruction で Copilot を案内する"
description: "リポジトリの instruction を確認し、ドキュメント標準を追加して、フィルタリングのコードに適用します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

生成 AI を使うときはコンテキストが重要です。特定の方法で実行する必要があるタスクでは、そのガイダンスを Copilot が参照できるようにします。[instruction file][instruction-files] を使うと、必要なコードだけでなく、その構成方法も伝えられます。フィルタリング機能を作成したので、Copilot が使用した instruction を確認し、ドキュメント標準を追加して、コードに適用します。

このレッスンでは、次の内容を学びます。

- リポジトリの instruction とパス単位の instruction file がエージェントにどのように渡るかを確認する。
- コーディング標準を守るため、instruction file を更新する。
- instruction file がコードに与える影響を確認する。

## シナリオ

Tailspin Toys には、開発プラクティスに関するガイドラインと要件があります。

- コメントには、コードの言い換えではなく、意図や自明でない判断を記述します。
- `db/` と `src/lib/` の export 関数には、存在する場合は注入可能な `db` 引数を含め、目的、パラメーター、戻り値を TSDoc/JSDoc で記述します。
- 再利用可能な Astro コンポーネントには `Props` の契約を記述し、関連コードの変更時にはコメントを最新に保ちます。
- 既存のフォーマットと lint のガイダンスを維持します。

instruction file を使うことで、Copilot に必要な情報を渡し、これらのプラクティスに沿って作業できるようにします。

## Instruction file

カスタム instruction を使うと、コンテキストや設定を Copilot に伝え、コーディングスタイルや要件を理解させることができます。好みのコーディング規約、ライブラリ、コードに含めるコメントの種類などを指定できます。リポジトリ全体に適用する instruction と、特定のファイル種別に適用する instruction を作成できます。

instruction file は 2 種類あります。

- `.github/copilot-instructions.md` は、リポジトリに対する**すべての**リクエストで Copilot に送られる単一の instruction file です。ほとんどのリクエストに関係するプロジェクトレベルの情報を記載します。
- `.github/instructions/*.instructions.md` は、特定の言語、ファイル種別、タスクに関するガイドラインを提供します。

> [!NOTE]
> その他の instruction 形式とサポート状況は環境によって異なります。特定の形式を前提にする前に、[カスタム instruction のサポート リファレンス][custom-instructions-support]を確認してください。

## このプロジェクトのカスタム instruction file を確認する

スタータープロジェクトには instruction file が用意されています。変更を加える前に確認し、すでに含まれている内容を把握します。

1. Codespace に戻ります。
2. Codespaces エディターで (ターミナルではなく) `.github/copilot-instructions.md` を開きます。
3. プロジェクトの簡単な説明とコーディングガイダンスを確認します。この instruction は、このリポジトリで Copilot を使うすべてのやり取りに適用されます。
4. `.github/instructions` フォルダーを開き、Astro ファイル、Drizzle データレイヤー、テストなどの instruction を確認します。
5. `.github/instructions/unit-tests.instructions.md` を開きます。先頭の `applyTo` フィールドは、instruction を適用するファイルを決める glob を設定します。
6. `.github/instructions/drizzle.instructions.md` を開き、ほかの instruction file や既存のプロジェクトファイルへのリンクを確認します。大きな instruction を再利用可能な小さなファイルに分け、Copilot が参考にできる例を示せます。

## チームのガイダンスに合わせて instruction file を更新する

既存の instruction は出発点になりますが、生成された TypeScript に TSDoc コメントが付くよう、中心となる `copilot-instructions.md` を更新します。

1. `.github/copilot-instructions.md` の **Code formatting guidance** セクションを探します。35 行目付近にあります。
2. セクションの最後に、次の項目を追加します。

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

ファイルは自動的に保存されます。

## 更新したガイダンスを使う

Copilot CLI は会話の開始時にリポジトリの instruction を読み込みます。機能のコンテキストを保ちながら新しいガイダンスを読み込むため、更新後に会話を終了して再開します。

1. フィルタリングの会話が開いている場合は `/exit` を入力して終了します。Copilot CLI は会話を自動的に保存します。
2. `game-filters-cli` ブランチのリポジトリルートから、保存した会話を再開します。

   ```bash
   copilot --resume
   ```

   選択を求められたらフィルタリングの会話を選び、`game-filters-cli` ブランチがチェックアウトされていることを確認します。
3. Copilot に更新したガイダンスを適用するよう依頼します。

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

4. `/diff` を入力し、変更された TypeScript ファイルを確認します。新しい TSDoc コメントがコードを正確に説明していることを確認します。

## まとめと次のステップ

Copilot CLI が instruction file からコンテキストを取得する方法を確認し、新しい標準を機能に適用しました。具体的には、次の作業を行いました。

- リポジトリの instruction とパス単位の instruction file がエージェントにどのように渡るかを確認した。
- コーディング標準を守るため、instruction file を更新した。
- instruction file がコードに与える影響を確認した。

次は、[再利用可能な quality-checks スキルをカスタマイズして実行し][next-lesson]、lint とテストを一貫して実行できるようにします。

## リソース

- [Copilot CLI にカスタム instruction を追加する][instruction-files]
- [カスタム instruction 作成のベスト プラクティス][instructions-best-practices]
- [Copilot 向けのカスタム instruction をより良く書くための 5 つのヒント][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
