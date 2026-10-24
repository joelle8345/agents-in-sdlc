---
title: "Exercise 6 - GitHub Copilot の作業を反復して改善する"
authors:
  - geektrainer
lastUpdated: 2026-06-30
next: false
---

| [← 前のレッスン: エージェントの監視と管理][previous-lesson] |
| :-- |

## 作業をレビューする

このラボでは、ユーザー体験を改善するいくつかのタスクに GitHub Copilot と取り組みました。エージェントモードでクライアントとサーバーにまたがるフィルタリングを追加し、Playwright MCP サーバーでブラウザーから手動テストしました。その後、カスタムエージェントを使って、ハイコントラストとライトモードを切り替えるアクセシビリティ機能を実装し、進行中のセッションに指示を追加して作業を拡張しました。次は、ローカルの作業を公開し、チームと同じ方法でレビューします。

### シナリオ

生成 AI を導入しても、ソフトウェア設計と DevOps の基本は変わりません。Copilot が生成したものも、通常のレビューサイクルに通します。Codespace からアクセシビリティの変更を push し、プルリクエストを作成して、チームをレビューに招待する前に差分を確認します。

## アクセシビリティ機能を公開する

[演習 4][exercise-4] と[演習 5][exercise-5]でアクセシビリティ用カスタムエージェントを使って実装した、ハイコントラストとライトモードの切り替えは、コミット済みの変更として Codespace にあります。チームでレビューできるようにブランチを push し、プルリクエストを作成します。

1. Codespace に戻ります。
2. VS Code で **Source Control** ビューを開きます。
3. アクセシビリティの変更がコミット済みであることを確認します。演習 5 の未コミットの変更がある場合は、ステージして `Add high-contrast and light-mode toggles` などの内容がわかるメッセージでコミットします。
4. **Publish Branch** を選択してブランチを公開します。または **...** メニューから **Push** を選択します。
5. VS Code から github.com で新しいブランチを開くよう求められたら、プロンプトを受け入れます。手動でリポジトリを開く場合は、ブランチのバナーで **Compare & pull request** を選択します。
6. わかりやすいタイトル (例: `Add high-contrast and light-mode toggles`) と、何をなぜ変更したかをまとめた短い説明を入力します。
7. **Create pull request** を選択します。
8. PR が作成されたら **Files changed** タブを選択し、変更全体をレビューします。特に次の項目を確認します。
   - モード切り替え用の UI コンポーネント。
   - ユーザー設定の保持に使うローカルストレージ。
   - ハイコントラストとライトモードの CSS またはスタイル変更。
   - アクセシビリティ属性 (ARIA ラベル、キーボード操作など)。
   - モード切り替えを管理する JavaScript/TypeScript コード。
9. **Conversation** タブに戻ります。
10. ワークフローが承認待ちの場合は、**Approve and run workflows** を選択します。

    ![ワークフローを承認して実行する画面](../../../_images/shared-approve-workflows.png)

11. ワークフローが完了するまで待ちます。すべて成功したことを確認します。

> [!TIP]
> アクセシビリティの変更について別の意見が必要な場合は、PR のコメントで `@copilot` にメンションし、「この PR にほかの Web Content Accessibility Guidelines (WCAG) の問題がないかレビューしてください」や「キーボード操作の改善を提案してください」などと依頼します。Copilot はコメントに対応する新しいセッションを開始します。

## オプションの演習 - ローカルでさらに試す

IDE でエージェントと反復して作業するスキルは、実践を重ねて身に付けます。VS Code で次のような追加セッションを試せます。

- ゲーム詳細ページに支援者の関心フォームを追加する。
- ゲーム一覧ページにページネーションを実装する。
- `src/lib/` のデータアクセス helper に入力検証とエラー処理を追加する。
- アクセシビリティエージェントの対象範囲を広げる。たとえば、サイト全体のキーボードフォーカス順序を監査する。

## まとめ

おめでとうございます。VS Code ハーネスを完了しました。このラボでは、次の作業を行いました。

- **Playwright MCP で機能を手動テストしました。** Playwright MCP サーバーを追加し、プルリクエストを開く前に Copilot にブラウザーを操作させてフィルタリング機能を検証しました。
- **エージェントモードでスタック全体にまたがる変更を連携して進めました。** 1 つのセッションで、クライアント、サーバー、テストにまたがるフィルタリング機能を追加しました。
- **カスタムエージェントを使いました。** エージェントピッカーからアクセシビリティに特化したカスタムエージェントを選び、リポジトリでハイコントラストモードを実装する様子を確認しました。
- **エージェントセッションを管理して方向づけました。** 提案された変更をインラインでレビューして必要なものを承認し、ライトモードの追加プロンプトで作業を拡張しました。
- **プルリクエストで作業を完了しました。** ローカルの変更を公開し、チームと同じ方法で全体をレビューしました。

## レビューと次のステップ

必須の VS Code ハーネスを完了しました。ここでワークショップを終了できます。

Copilot のエージェント機能をさらに知りたい場合は、ほかのハーネスで異なる環境を使ったシナリオに取り組めます。

- 💻 **[CLI ハーネス](../../cli/)** — Plan と Autopilot モード、スキル、QA カスタムエージェント、Playwright MCP、Agent Merge、コンテキストを考慮した引き継ぎを使って、ターミナルからレビュー済みの変更を 2 つリリースします。
- ☁️ **[Cloud agent ハーネス](../../cloud/)** — cloud agent への issue の割り当て、agents ページでのセッションの監視、プルリクエストでの非同期の反復に重点を置きます。

ここで始めた作業をさらに発展させることもできます。[awesome-copilot][awesome-copilot]には、自分のプロジェクトに応用できる instruction file、カスタムエージェント、スキルが豊富にあります。

オプションの拡張である[オプション: Foundry を取り入れる][exercise-7]では、VS Code と Microsoft Foundry Toolkit を使い、モデルを準備して Backer Concierge をデプロイし、サイトに接続します。

## リソース

- [GitHub Copilot][github-copilot]
- [VS Code の Copilot Chat][copilot-chat-vscode]
- [エージェントモードの使用][agent-mode]

---

| [← 前のレッスン: エージェントの管理][previous-lesson] |
|:--|

[previous-lesson]: ../5-managing-agents/
[exercise-4]: ../4-custom-agents/
[exercise-5]: ../5-managing-agents/
[exercise-7]: ../7-foundry-toolkit/
[github-copilot]: https://github.com/features/copilot
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
[awesome-copilot]: https://github.com/github/awesome-copilot
