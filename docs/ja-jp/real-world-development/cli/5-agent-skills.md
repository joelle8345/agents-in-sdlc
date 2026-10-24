---
title: "Lesson 5 - quality-checks スキルをカスタマイズして使う"
description: "既存の quality-checks スキルを確認し、レポート形式をカスタマイズして、フィルタリングを検証します。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

コードを書くことは、開発作業の一部にすぎません。これまではコードを手動で検証し、instruction file を使って規約に従わせました。では、テストや lint、継続的インテグレーション (CI) のほかの作業はどうでしょうか。

このようなタスクには、**エージェントスキル**が適しています。スキルは、テストなどの操作を適切に実行する方法を Copilot に伝えます。

このレッスンでは、次の内容を学びます。

- 既存の `quality-checks` スキルを確認する。
- 結果のレポート形式をカスタマイズする。
- スキルを再読み込みして実行する。

## シナリオ

Tailspin Toys では、単体テスト、lint、型チェックに `quality-checks` スキルを使っています。チームは、結果を読みやすくするためレポートの改善を希望しています。

## Instruction、スクリプト、リソース

エージェントスキルは、再利用可能なタスクの instruction、実行可能なスクリプト、補助リソースをまとめたもので、エージェントが必要に応じて読み込みます。基本的には、スキル名のフォルダーと、その中の `SKILL.md` で構成されます。Markdown ファイルにはスキルの名前と説明を定義する frontmatter、機能の概要、呼び出すタイミングのガイダンスが含まれます。スキルのフォルダーには、必要に応じてスクリプトやほかのリソース用のサブフォルダーも含められます。

> [!NOTE]
> スキルに追加のフォルダーやファイルは必須ではありません。Tailspin Toys の `quality-checks` スキルはプロジェクトの既存コマンドを使用するため、`SKILL.md` のみで構成されています。

スキルは、チームで共有・再利用できるようプロジェクトの `.github/skills` フォルダーに置くか、ユーザーの `~/.copilot/skills` フォルダーに置けます。

## スキルを確認する

Tailspin Toys チームが単体テスト、lint、型チェック用に作成した `quality-checks` スキルを確認します。

1. Codespace に戻り、Codespaces エディターで `.github/skills/quality-checks/SKILL.md` を開きます。
2. ファイルの先頭にある `name` と `description` を読みます。説明は、Copilot がスキルを呼び出すタイミングを判断するのに役立ちます。
3. instruction を読み、テストと lint の進め方を確認します。
4. まだ **Results output formatting** セクションがないことを確認します。

## 変更前にスキルを実行する

Copilot にスキルの 3 つのチェックを実行してもらいます。

1. Interactive モードでフィルタリングの会話に戻ります。
2. 次のプロンプトを使います。

   ```plaintext
   Run the quality-checks skill for unit tests, lint, and type checks.
   ```

3. 最後に表示されるレポートを確認します。

## レポートをカスタマイズする

何を実行したか、成功したか、ツールがどのような結果を報告したかがわかるレポートに改善します。

1. `.github/skills/quality-checks/SKILL.md` に戻ります。
2. ファイルの末尾に次のセクションを追加します。

   ```markdown
   ## Results output formatting

   Upon completion, report each command that ran and whether it passed, failed, or was blocked. Include test counts, durations, errors, warnings, and other metrics only when the tool reports them. Identify the next action for any failure or blocker, and never describe a skipped or incomplete check as passed.
   ```

3. ファイルが自動的に保存されたことを確認します。

## 更新したスキルを実行する

変更を加えたスキルを実行して、結果を確認します。Copilot CLI は会話を再起動せずに、編集済みのスキルを再読み込みできます。

1. 次を入力します。

   ```plaintext
   /skills reload
   ```

2. 先ほどと同じプロンプトを送信します。

   ```plaintext
   Run the quality-checks skill for unit tests, lint, and type checks.
   ```

3. 最後に表示されるレポートを確認し、最初のレポートと比較します。

## まとめと次のステップ

既存のエージェントスキルをカスタマイズして実行しました。このレッスンでは、次の作業を行いました。

- 単体テスト、lint、型チェック用の `quality-checks` スキルを確認した。
- 結果のレポート形式をカスタマイズした。
- スキルを再読み込みして実行した。

この変更は、フィルタリングの機能 PR に含めます。次は、[Playwright MCP サーバーを使って][next-lesson] Copilot がサイトを直接操作できるようにします。

## スキルの例

以下のコミュニティの例は参考情報であり、追加の作業ではありません。

- [Agent Skills 仕様][skill-spec]
- [コントリビューション ワークフロー: `make-repo-contribution`][contribution-example]
- [要件ドキュメント: `prd`][prd-example]
- [図とエクスポートスクリプト: `drawio`][drawio-example]
- [ブラウザーテスト: `webapp-testing`][browser-example]

[previous-lesson]: ../4-custom-instructions/
[next-lesson]: ../6-mcp-playwright/
[skill-spec]: https://agentskills.io/specification
[contribution-example]: https://github.com/github/awesome-copilot/tree/main/skills/make-repo-contribution
[prd-example]: https://github.com/github/awesome-copilot/tree/main/skills/prd
[drawio-example]: https://github.com/github/awesome-copilot/tree/main/skills/drawio
[browser-example]: https://github.com/github/awesome-copilot/tree/main/skills/webapp-testing
