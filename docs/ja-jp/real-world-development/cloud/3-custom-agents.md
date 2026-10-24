---
title: "Exercise 3 - カスタムエージェント"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## カスタムエージェントとは

GitHub Copilot の[カスタムエージェント][custom-agents-concept]を使うと、開発ワークフロー内の特定のタスクや領域に特化した AI アシスタントを作成できます。リポジトリの `.github/agents` フォルダーに Markdown ファイルでエージェントを定義し、目的を絞った instruction、ベストプラクティス、コーディングパターン、専門知識を Copilot に提供します。チームは専門知識を再利用可能なエージェントにまとめられます。たとえば、[Web Content Accessibility Guidelines (WCAG)][wcag] への準拠を確認するアクセシビリティエージェント、安全なコーディングプラクティスに従うセキュリティエージェント、一貫したテストパターンを維持するテストエージェントを作成できます。

カスタムエージェントは、プロジェクトの `.github/agents` フォルダー内の Markdown ファイル、または全体で使う `~/.copilot/agents` に定義します。各ファイルには、最低限 `name` と `description` を含む YAML frontmatter と、エージェントの動作、専門知識、instruction を定義する Markdown プロンプトを記述します。

### カスタムエージェントとエージェントスキルの比較

カスタムエージェントと[エージェントスキル][agent-skills-concept]には共通点があります。どちらも主に Markdown ファイルで定義し、AI に操作方法を伝えます。違いを簡潔に表すと、**カスタムエージェントは作業者、スキルはツール**です。

カスタムエージェントは独自のコンテキストウィンドウを持ち、作業中にスキルや別のエージェントを調整します。このラボでは、アクセシビリティのカスタムエージェントがガイドラインに照らしてサイトをレビュー・更新します。その作業の一環として、プルリクエストのワークフロースキルや、テストの実行・管理スキルなどを呼び出せます。

> [!NOTE]
> カスタムエージェントの作成に唯一の正解はありません。AI のほかの活用方法と同様に、環境やシナリオに合わせて試し、反復してください。

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

カスタムエージェントを使って、次の内容を確認します。

- カスタムエージェントの定義方法。
- カスタムエージェントへのタスクの割り当て方法。

## シナリオ

Tailspin Toys は、視覚能力や好みにかかわらず、すべてのユーザーがクラウドファンディングのプラットフォームを利用できるよう取り組んでいます。現在のダークテーマは、文字色と背景色のコントラストが不十分で読みづらいというフィードバックが寄せられています。このアクセシビリティ上の課題に対応するため、デザインチームはユーザーが切り替えられるハイコントラストモードの実装を依頼しました。

アクセシビリティは重要です。カスタムエージェントを使って、機能を迅速に生成します。

## アクセシビリティのカスタムエージェントを確認する

アクセシビリティ向けのカスタムエージェントはすでに用意されています。内容を確認して、Copilot へのガイダンスを把握します。

次の手順で Codespace に戻り、アクセシビリティ用カスタムエージェントのファイルを確認します。

1. Codespace に戻ります。
2. `.github/agents/accessibility.md` を開きます。
3. `name` と `description` フィールドを含む YAML frontmatter を確認します。

> [!CAUTION]
> `name` と `description` を含む frontmatter は、カスタムエージェントに必須です。

4. 続くセクションを読み、アクセシブルな Web サイトのコード生成に関する次の項目を確認します。
   - 中核となる責務。
   - アクセシビリティのベストプラクティス。
   - HTML、CSS、JavaScript のコード例。
   - よくある問題と間違い。

## issue を作成して割り当てる

Mission control は、環境内のすべてのエージェントを操作する場所です。Copilot cloud agent にタスクを割り当て、進捗を監視し、方向を変えたり追加のガイダンスを与えたりできます。まず、ハイコントラストモードの作成を Copilot に割り当てます。

1. リポジトリを開きます。
2. **Issues** タブを選択します。
3. **New issue** を選択して、新しい issue のダイアログを開きます。
4. **Blank issue** を選択して issue を作成します。
5. **Title** に `Add high contrast mode to website` と入力します。
6. **Description** に次の内容を入力します。

    ```plaintext
    We need a high contrast mode for the site. There should be a toggle for high contrast which the user can set. It should store the setting in local storage on the browser.
    ```

7. **Create** を選択して issue を作成します。
8. 右側の **Assign to Copilot** を選択して、割り当てダイアログを開きます。
9. 一覧から **Accessibility agent** を選択します。

    ![カスタムエージェントと Accessibility が選択されている cloud agent の割り当て画面](../../../_images/ex5-select-custom-agent.png)

10. **Assign** を選択します。
11. Copilot がバックグラウンドで作業を開始します。

## まとめと次のステップ

GitHub Copilot の[カスタムエージェント][custom-agents]を確認しました。特定のタスクや領域に特化した AI アシスタントです。カスタムエージェントを使うと、チームの専門知識や標準を再利用可能なエージェントにまとめ、特定の作業をより効果的に Copilot に実行させることができます。

このレッスンでは、次の内容を確認しました。

- カスタムエージェントの定義方法。
- カスタムエージェントへのタスクの割り当て方法。

Copilot がハイコントラストモードを実装している間に、次は mission control から[エージェントのセッションを監視して方向づけます][next-lesson]。

## リソース

- [カスタムエージェントについて][custom-agents]
- [Organization でカスタムエージェントを使用するための準備][org-custom-agents]
- [Enterprise でカスタムエージェントを使用するための準備][enterprise-custom-agents]

---

| [← 前のレッスン: GitHub Copilot cloud agent][previous-lesson] | [次のレッスン: エージェントの監視と管理 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
