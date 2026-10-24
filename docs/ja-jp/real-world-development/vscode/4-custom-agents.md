---
title: "Exercise 4 - カスタムエージェント"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## カスタムエージェントとは

GitHub Copilot の[カスタムエージェント][custom-agents-concept]を使うと、開発ワークフロー内の特定のタスクや領域に特化した AI アシスタントを作成できます。リポジトリの `.github/agents` フォルダーに Markdown ファイルでエージェントを定義し、目的を絞った instruction、ベストプラクティス、コーディングパターン、専門知識を Copilot に提供します。チームは専門知識を再利用可能なエージェントにまとめられます。たとえば、[WCAG][wcag] への準拠を確認するアクセシビリティエージェント、安全なコーディングプラクティスに従うセキュリティエージェント、一貫したテストパターンを維持するテストエージェントを作成できます。

カスタムエージェントは、プロジェクトの `.github/agents` フォルダー内の Markdown ファイル、または全体で使う `~/.copilot/agents` に定義します。各ファイルには、最低限 `name` と `description` を含む YAML frontmatter と、エージェントの動作、専門知識、instruction を定義する Markdown プロンプトを記述します。

### カスタムエージェントとエージェントスキルの比較

カスタムエージェントと[エージェントスキル][agent-skills-concept]には共通点があります。どちらも主に Markdown ファイルで定義し、AI に操作方法を伝えます。違いを簡潔に表すと、**カスタムエージェントは作業者、スキルはツール**です。

カスタムエージェントは独自のコンテキストウィンドウを持ち、作業中にスキルや別のエージェントを調整します。このラボでは、アクセシビリティのカスタムエージェントがガイドラインに照らしてサイトをレビュー・更新します。その作業の一環として、プルリクエストのワークフロースキルや、テストの実行・管理スキルなどを呼び出せます。

> [!NOTE]
> カスタムエージェントの作成に唯一の正解はありません。AI のほかの活用方法と同様に、環境やシナリオに合わせて試し、反復してください。

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

## シナリオ

Tailspin Toys は、視覚能力や好みにかかわらず、すべてのユーザーがクラウドファンディングのプラットフォームを利用できるよう取り組んでいます。現在のダークテーマは、文字色と背景色のコントラストが不十分で読みづらいというフィードバックが寄せられています。このアクセシビリティ上の課題に対応するため、デザインチームはユーザーが切り替えられるハイコントラストモードの実装を依頼しました。

アクセシビリティは重要です。カスタムエージェントを使って、機能を迅速に生成します。

この演習では、次の内容を学びます。

- 既存のアクセシビリティ用カスタムエージェントを確認する。
- Copilot Chat でアクセシビリティエージェントを使い、ハイコントラストモードを実装する。

## アクセシビリティのカスタムエージェントを確認する

アクセシビリティ向けのカスタムエージェントはすでに用意されています。Copilot へのガイダンスを確認します。

Codespace に戻り、ターミナルを開いて `main` からアクセシビリティ作業用の新しいブランチを作成します (演習 3 のフィルタリング PR とは分けて作業します)。

```bash
git checkout main
git pull
git checkout -b accessibility-vscode
```

1. `.github/agents/accessibility.md` を開きます。
2. `name` と `description` フィールドを含む YAML frontmatter を確認します。

> [!CAUTION]
> `name` と `description` を含む frontmatter は、カスタムエージェントに必須です。

3. 続くセクションを確認し、次の内容を把握します。
   - アクセシブルな Web サイトのコード生成に関する中核的な責務。
   - アクセシビリティのベストプラクティス。
   - HTML、CSS、JavaScript のコード例。
   - よくある問題と間違い。

## Copilot Chat でカスタムエージェントを使う

VS Code では、`.github/agents` に定義されたすべてのカスタムエージェントが Copilot Chat ビュー下部のエージェントドロップダウンに表示されます。カスタムエージェントを選択すると、その instruction とツールに合わせてチャットセッションが設定されます。

> [!TIP]
> **Copilot Chat を開く**
>
> 以下の演習を始める前に Codespace に戻り、Copilot Chat パネルを開き、**New Chat** を選択して新しい会話を開始します。モードとモデルの選択は演習によって異なるため、必要な場面で手順を示します。

1. Chat ビューのエージェントドロップダウンで **Agent** が選択されていない場合は選択します。

   ![Chat ビューのエージェント選択を示すスクリーンショット](../../../_images/shared-chat-mode-selector.png)

2. Chat ビュー下部のエージェントドロップダウンを選択します。現在のエージェントが表示されています。既定では **default** です。
3. 利用可能なエージェントの一覧から **Accessibility agent** を選択します。
4. 次のプロンプトをアクセシビリティエージェントに送信します。

    ```plaintext
    Add a high-contrast mode to the site. There should be a toggle for high contrast which the user can set, and the setting should persist across page reloads using local storage on the browser.
    ```

5. Copilot Chat がコードベースを調査し、変更を提案してプロジェクトファイルを編集する様子を確認します。各編集はファイルパスとレビュー用の差分とともにチャットに表示されます。
6. エージェントが変更したファイルに応じて、**Files changed** の表示が更新されることを確認します。

> [!NOTE]
> 実際のリポジトリを変更するため、処理には数分かかる場合があります。作業中に Astro コンポーネント、CSS、関連テストなどの既存ファイルが編集されます。

進行中の作業の確認と方向づけは、次の演習で行います。

## まとめと次のステップ

GitHub Copilot の[カスタムエージェント][custom-agents]を確認しました。特定のタスクや領域に特化した AI アシスタントです。カスタムエージェントを使うと、チームの専門知識や標準を再利用可能なエージェントにまとめ、特定の作業をより効果的に Copilot に実行させることができます。

このレッスンでは、次の内容を確認しました。

- カスタムエージェントの定義方法。
- Copilot Chat のエージェントモードでカスタムエージェントを使う方法。

次は、[エージェントの作業を監視して方向づけます][next-lesson]。変更を確認しながら、同じセッションにライトモードの切り替えを追加します。

## リソース

- [カスタムエージェントについて][custom-agents]
- [IDE でカスタムエージェントを作成する][creating-custom-agents-ide]
- [VS Code のカスタムエージェント][custom-agents-vscode]
- [カスタムエージェントの構成][custom-agents-config]
- [awesome-copilot のカスタムエージェント][awesome-copilot-agents]

---

| [← 前のレッスン: Playwright MCP サーバーで機能をテストする][previous-lesson] | [次のレッスン: エージェントの監視と管理 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-mcp/
[next-lesson]: ../5-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[creating-custom-agents-ide]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/create-custom-agents-in-your-ide
[custom-agents-vscode]: https://code.visualstudio.com/docs/copilot/customization/custom-agents
[custom-agents-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
[awesome-copilot-agents]: https://github.com/github/awesome-copilot/tree/main/agents
