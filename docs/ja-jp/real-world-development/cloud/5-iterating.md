---
title: "Exercise 5: GitHub Copilot の作業を反復して改善する"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 前のレッスン: エージェントの管理][previous-lesson] |
|:--|

## 作業をレビューする

このラボでは、ユーザー体験の改善や機能追加を目的として、GitHub Copilot といくつかのタスクに取り組みました。コードへのドキュメント追加、デザインチームが改善できる関連ゲーム機能の作成、ハイコントラストとライトモードを切り替えるアクセシビリティ機能の実装を依頼しました。コード変更を確認し、必要に応じて Copilot にフィードバックを送って改善しましょう。

### シナリオ

生成 AI を導入しても、ソフトウェア設計と DevOps の基本は変わりません。生成されたコードをレビューし、通常の DevOps プロセスを進めます。チームでのレビューを有効にする前に、ドキュメント、関連ゲーム機能、アクセシビリティ機能について、GitHub Copilot の提案を確認します。

## GitHub Copilot cloud agent とセキュリティ

Copilot cloud agent は監督なしで非同期にタスクを実行するため、安全性を保つセキュリティ制限が設けられています。

- Copilot はリポジトリに対する読み取りアクセス権を持ち、コード作成に使うブランチに限って書き込みアクセス権を持ちます。
- cloud agent は GitHub Actions 内で動作し、作業用に一時的な独立環境を作成します。
- GitHub Actions ワークフローを実行するには、人間による承認が必要です。
- MCP サーバーを含む[外部リソースへのアクセスは、既定で制限されています](https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall)。

## 生成されたドキュメントをレビューする

まず、GitHub Copilot cloud agent が最初に作成した、コードへのドキュメント追加のプルリクエスト (PR) を確認します。github.com の標準的な PR インターフェイスを使います。

> [!NOTE]
> PR に GitHub Copilot がファイアウォールでブロックされたという警告が表示される場合があります。Copilot は外部 MCP サーバーへの呼び出しなど、外部リソースへのアクセスが既定で制限されているため、これは想定された動作です。必要に応じて、[Copilot cloud agent のファイアウォールを構成または無効化][agent-firewall]できます。

1. github.com のリポジトリに戻ります。
2. **Pull Requests** を選択して、プルリクエストの一覧を開きます。
3. **Add missing documentation** または同様のタイトルのプルリクエストを開きます。

> [!NOTE]
> Copilot がまだ作業中の場合、プルリクエストには **[WIP]** が付いています。その場合は完了するまで待ちます。数分かかることがあるため、休憩したり、これまでに学んだ内容を振り返ったりしてください。

4. 準備ができたら **Files changed** タブを選択して変更をレビューします。

    ![Files changed タブ](../../../_images/shared-pr-files-changed.png)

5. 新しく追加された TSDoc doc comment など、更新されたコードを確認します。変更内容は状況によって異なります。

    コードを確認しながら、TSDoc doc comment、TypeScript の規約、コメントヘッダーを探します。これらは演習 2 の最初に確認したカスタム instruction file によるものです。

6. 更新内容をレビューし問題がなければ、**Conversation** タブに戻り、下にスクロールします。
7. ワークフローが承認待ちであることを示す表示を確認します。
8. 承認待ちのワークフローがある場合は、**Approve and run workflows** を選択します。

   ![ワークフローを承認して実行する画面](../../../_images/shared-approve-workflows.png)

9. ワークフローがプルリクエストのチェックとしてキューに追加されたことを確認します。順調に進めば、単一の Astro アプリに対するプロジェクトのチェックが成功します。完了まで数分かかる場合があります。

## GitHub Copilot に変更を依頼する

プルリクエストで Copilot と作業するときは、Copilot の一方向の出力を受け取るだけではありません。チームメンバーと同じように、プルリクエストまたはコードのインラインコメントで Copilot にメンションできます。Copilot はコメントを読み、対応する新しいセッションを開始します。出力は確定的でないため、依頼文を厳密に指定することはできません。たとえば、次のような更新を依頼できます。

- 各コードファイルの先頭に、役割を説明する短いコメントヘッダーを追加する。
- TypeScript と Astro のファイルに TSDoc doc comment を追加する。
- Astro アプリの構造を説明する README を作成する。

1. 上記の例などを使い、コードベースに必要なドキュメント変更を **@copilot** にメンションしてコメントで依頼します。
2. **View Session** を選択し、Copilot が作業する様子を確認します。Copilot は更新用の新しいセッションを開始します。
3. **Back to pull request** を選択すると、プルリクエストに戻れます。

    ![プルリクエストに戻る画面](../../../_images/ex7-back-to-pr.png)

4. Copilot が変更を完了したら、プルリクエストに新しいコミットが追加されたことを確認します。
5. **Files changed** タブを選択して変更をレビューします。

納得できるまで反復して改善できます。問題がなければ、PR をドラフトからレビュー可能な状態に変更して、`main` ブランチにマージします。

![PR をレビュー可能な状態に変更する画面](../../../_images/ex7-ready-for-review.png)

## 関連ゲーム機能をレビューする

ゲーム詳細ページに関連ゲームを表示する issue に対して、Copilot が作成した PR を確認します。

1. GitHub.com のリポジトリに戻ります。
2. **Pull Requests** タブを選択します。
3. **Show related games on the game details page** または同様のタイトルの PR を選択します。
4. **Files changed** タブを選択し、生成されたコードをレビューします。
5. 更新内容を確認し問題がなければ、**Conversation** タブに戻り、下にスクロールします。
6. ワークフローが承認待ちであることを示す表示を確認します。
7. 承認待ちのワークフローがある場合は、**Approve and run workflows** を選択します。

   ![ワークフローを承認して実行する画面](../../../_images/shared-approve-workflows.png)

8. ワークフローがプルリクエストのチェックとしてキューに追加されたことを確認します。順調に進めば、単一の Astro アプリに対するプロジェクトのチェックが成功します。完了まで数分かかる場合があります。
9. **任意:** Codespace でこのブランチに切り替え、関連ゲーム機能を手動でテストできます。Codespace のターミナルを開き、Copilot が作成したブランチ名 (例: **copilot/fix-8**) に置き換えて次のコマンドを実行します。

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

Copilot は関連ゲーム機能を作成しました。これまでと同じように、更新をコメントで依頼して反復できます。たとえば、表示する関連ゲームの件数を変えたり、コメントヘッダーや TSDoc doc comment を追加したりできます (この issue はカスタム instruction を更新する**前**に割り当てたことを思い出してください)。**Conversation** タブにコメントを追加すると、Copilot が確認して新しいセッションを開始します。

## アクセシビリティ機能をレビューする

最後に、アクセシビリティ用カスタムエージェントが実装した機能を確認します。この PR には、演習 3 で依頼したハイコントラストモードと、演習 4 で mission control から追加を依頼したライトモードの両方が含まれます。

1. GitHub.com のリポジトリに戻ります。
2. **Pull Requests** タブを選択します。
3. **Add high contrast mode to website** または同様のタイトルの PR を選択します。

> [!NOTE]
> Copilot がまだ作業中の場合、プルリクエストには **[WIP]** が付いています。その場合は完了まで待ちます。数分かかる場合があります。

4. **Files changed** タブを選択して、生成されたコードをレビューします。
5. 実装を確認し、特に次の項目に注意します。
   - モード切り替え用の UI コンポーネント。
   - ユーザー設定の保存に使うローカルストレージ。
   - ハイコントラストモードとライトモードの CSS またはスタイル変更。
   - アクセシビリティ属性 (ARIA ラベル、キーボード操作など)。
   - モード切り替えを管理する JavaScript/TypeScript コード。

6. 更新内容を確認し問題がなければ、**Conversation** タブに戻り、下にスクロールします。
7. ワークフローが承認待ちであることを示す表示を確認します。
8. 承認待ちのワークフローがある場合は、**Approve and run workflows** を選択します。

   ![ワークフローを承認して実行する画面](../../../_images/shared-approve-workflows.png)

9. ワークフローがプルリクエストのチェックとしてキューに追加されたことを確認します。順調に進めば、単一の Astro アプリに対するプロジェクトのチェックが成功します。完了まで数分かかる場合があります。
10. **任意:** Codespace でこのブランチに切り替えて、アクセシビリティ機能を手動でテストできます。Codespace のターミナルを開き、Copilot が作成したブランチ名に置き換えて次のコマンドを実行します。

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    アプリケーションを起動し、ブラウザーでハイコントラストとライトモードの切り替えをテストします。ページを再読み込みしても設定が保持されることを確認します。

アクセシビリティ用カスタムエージェントが、アクセシビリティのベストプラクティスに沿って機能を実装するよう Copilot を案内したことを確認してください。アクセシビリティ上の懸念や改善点がある場合は、前の PR と同じようにコメントで **@copilot** に更新を依頼できます。

## オプションの演習 — 追加の作業を委任する

実際のバックログ項目を cloud agent に割り当てて別の作業に移ることで、cloud agent を効果的に活用できます。練習として、リポジトリに issue を追加し、Copilot に割り当ててみましょう。たとえば、次のような作業があります。

- ゲーム詳細ページに支援者の関心フォームを作成する。
- ゲーム一覧ページにページネーションを実装する。
- データアクセスヘルパーに入力検証とエラー処理を追加する。

## まとめ

Cloud agent のハーネスを完了しました。これらのレッスンを通じて、次の作業を行いました。

- **このリポジトリにあるカスタム instruction file を確認し、後で cloud agent の出力への影響を確認できるようにした。**
- **issue を Copilot cloud agent に割り当て、環境の準備、計画、非同期の実行を確認した。**
- **アクセシビリティ用のカスタムエージェントを作成して使い、ハイコントラストとライトモードの切り替えを追加した。**
- **Copilot agents ページを mission control として使い、アクセシビリティセッションを監視して途中で指示を追加した。**
- **cloud agent のプルリクエストをレビューして反復し、`@copilot` に変更を依頼してワークフローを承認した。**

## レビューと次のステップ

Cloud agent のハーネスを完了しました。引き続き確認する場合は、ほかのハーネスで異なる環境を使ったシナリオに取り組めます。

- 🖥️ **[VS Code ハーネス](../../vscode/)** — IDE から Copilot Chat のエージェントモードと MCP 統合を確認します。
- 💻 **[CLI ハーネス](../../cli/)** — Plan と Autopilot モード、エージェントスキル、QA カスタムエージェント、Playwright MCP、Agent Merge、cloud agent への任意の `/delegate` を使い、ターミナルから 2 つの変更をレビューしてリリースします。

自分のリポジトリでは、次のアイデアを試せます。

- リファクタリングまたはテスト範囲の issue を cloud agent に割り当てる。
- 別の領域向けのカスタムエージェントを作成する。
- 別の技術スタック用に `copilot-setup-steps.yml` を設定する。

## リソース

- [GitHub Copilot][github-copilot]
- [Copilot エージェントについて][copilot-agents]
- [GitHub issue を Copilot に割り当てる][assign-issue]
- [Copilot cloud agent のセットアップ ワークフローのベストプラクティス][cloud-agent-best-practices]
- [Copilot cloud agent のファイアウォールを構成する][agent-firewall]

---

| [← 前のレッスン: エージェントの管理][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
