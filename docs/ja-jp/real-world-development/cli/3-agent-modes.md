---
title: "Lesson 3 - エージェントモード: Plan と Autopilot"
description: "Plan モードでアプローチを決め、Autopilot で issue に基づいてフィルタリングを構築し、Interactive モードで結果をレビューします。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

最初は小さな機能を追加しましたが、より大きな変更には、さらに堅牢なプロセスが必要です。GitHub Copilot CLI は組織の既存の開発フローに合わせて使えるため、適切な方法で必要なものを構築できます。このレッスンから、エージェントを使った一般的な開発プロセスに取り組みます。issue から新機能を作り、コードの妥当性と機能の動作を確認して、最終的にプロジェクトへマージします。

> [!NOTE]
> 機能の作業を続ける間は、同じ会話とブランチを使います。通常はファイルの種類ごとに別のブランチや PR を使いますが、ここでは主要な概念に集中するため、手順を簡略化しています。

このレッスンでは、次の内容を学びます。

- GitHub issue から Copilot との新しい会話を開始する。
- Plan モードで要件を定義する。
- Autopilot モードで新機能を実装する。
- コードをレビューする。
- 転送されたブラウザーで機能を手動検証する。

機能の作業を続ける中で、リポジトリの instruction の更新、既存の `quality-checks` スキルのカスタマイズ、MCP による検証、QA エージェントの作成を行い、機能の PR を作成します。

## シナリオ

Tailspin Toys のカタログが拡大し、訪問者がカテゴリとパブリッシャーでゲームを絞り込める必要があります。バックログの issue に機能が記載されていますが、カテゴリを組み合わせる方法など、コーディング前に合意しておきたい詳細があります。Plan モードで決定事項を整理し、範囲を定めた実装を Autopilot に許可します。

## 背景

AI コーディングエージェントを開発フローに導入しても、基本は変わりません。むしろ、これまで以上に重要になります。多くの開発者は、次のような流れで作業します。

1. 実装内容を記述した issue から始める。
2. 構築するものの計画を立てる。
3. コードを作成してレビューする。
4. テストを実行してコードを検証する。
5. 新しい機能を手動で検証する。
6. プルリクエスト (PR) を作成する。
7. コードレビューと継続的インテグレーションが成功したら、コードをマージする。

> [!NOTE]
> 詳細はチームや組織によって異なりますが、多くの場合は上記の流れを基本とします。

この標準的なアプローチに従うことで、AI が生成したコードが要件を満たし、手書きのコードと同じ確認プロセスを通るようにできます。

## 会話モード

**会話モード**は、エージェントに与える自律性の度合いを制御します。<kbd>Shift</kbd>+<kbd>Tab</kbd> を押すとモードを切り替えられます。

- **Interactive**: 開発者とエージェントが共同で作業します。エージェントは変更を提案し、次の作業に進む前に入力を待ちます。
- **Plan**: エージェントはまず計画を作成します。プロジェクトファイルの編集はできません。
- **Autopilot**: エージェントはコードの作成、テストの実行、タスク完了までの反復を自律的に行います。

まず Plan モードで計画を確認し、その後 Autopilot で実装します。

## issue から開始する

フィルタリングの作業を始める前に、Codespace に戻り、リポジトリとターミナルが準備できていることを確認します。

1. Codespace に戻ります。停止している場合は再起動します。
2. 星評価の PR がマージされていることを確認します。
3. ターミナルが開いていない場合は、<kbd>Control</kbd>+<kbd>\`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux) を押します。
4. `main` を更新し、フィルタリング作業用のブランチを作成します。

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. Copilot CLI を起動します。

   ```bash
   copilot --yolo
   ```

6. <kbd>Tab</kbd> を 2 回押して **Issues** タブを開きます。
7. <kbd>A</kbd> を押してすべての issue を表示します。
8. 矢印キーで **Allow users to filter games by category and publisher** というタイトルの issue を選択します。
9. <kbd>C</kbd> を押して issue をプロンプトに追加し、**Session** タブに戻ります。

プロンプトの先頭に `#7` (または同様の番号) が表示されます。`#` を使うと GitHub の issue やプルリクエスト (PR) をコンテキストに追加できます。

## フィルタリング機能を計画する

計画を立てることで、Copilot に作業を任せる前に機能実装のアプローチを定義できます。複雑な作業では、事前に計画を立てることをお勧めします。Plan モードに切り替えて、Copilot に計画を作成してもらいます。

1. <kbd>Shift</kbd>+<kbd>Tab</kbd> を押して Plan モードに切り替えます。プロンプトの下にあるモード表示が **Plan** であることを確認します。
2. 前の手順で追加した issue の参照の後に、次のプロンプトを入力します。

   ```plaintext
   Create a plan for implementing this feature.
   ```

Copilot はプロジェクトを調査し、最適なアプローチを判断して計画を作成します。

3. フィルタリングの動作について Copilot から質問されたら、希望する内容に基づいて回答します。正解は 1 つではありません。
4. 計画が完成したら、<kbd>Control</kbd>+<kbd>E</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>E</kbd> (Windows/Linux) を押して計画を展開します。
5. 計画をスクロールして確認します。
6. 決定内容と異なる箇所があれば、Copilot に修正を依頼します。

## Autopilot を承認する

計画を作成してレビューしたら、実装に進みます。Autopilot を使って Copilot に作業を任せます。Autopilot では、Copilot が完了したと判断するまで問題に取り組み、反復します。

1. **Accept plan and build on autopilot (recommended)**、またはインストール済みのバージョンで同様のラベルが付いた選択肢を選びます。
2. プロンプトの下にあるモード表示が **Autopilot** であることを確認します。
3. Copilot が計画に沿って反復し、コードを生成してテストを実行する様子を確認します。

> [!NOTE]
> 承認するとすぐに実装が始まる場合があるため、先に計画をレビューしてください。Copilot が依存関係の不足やポートの競合を報告した場合は、チェック完了と判断する前にセットアップの問題を解決します。

## 実装をレビューして検証する

コードが生成されたら、ほかのコードと同じように、マージ前にレビューします。コードを確認し、サイトを起動して動作を確かめます。

1. <kbd>Shift</kbd>+<kbd>Tab</kbd> を押して Interactive モードに切り替えます。モード表示に **Plan** または **Autopilot** が出ていないことを確認します。
2. `/diff` を入力し、フィルタリングの実装とテストを確認します。
3. 結果を issue および計画時の決定事項と照らし合わせます。
4. コードのレビューが終わったら、<kbd>Esc</kbd> を押して差分画面を閉じます。
5. プロジェクトのチェック結果を確認し、失敗があれば Copilot に解決を依頼します。

## 新しい機能を試す

コードに問題がなさそうでも、実際に動作するか確認しましょう。前回と同じようにアプリを起動し、Codespaces の転送ポートからサイトを開きます。

1. Copilot にアプリの起動を依頼します。

   ```plaintext
   Start the app so I can try the filtering feature in my browser. Tell me the URL and leave the server running.
   ```

2. Codespaces でポート `4321` が利用可能と表示されたら、**Open in Browser** を選択します。
3. カテゴリのフィルタリング、パブリッシャーのフィルタリング、計画時に合意した組み合わせを試します。
4. リセット時と結果がない場合の動作が、issue と決定内容に合っていることを確認します。
5. Codespace に戻り、Copilot に起動した開発サーバーを停止するよう依頼します。

## まとめと次のステップ

異なる会話モードを使って機能を構築し、レビューしました。このレッスンでは、次の作業を行いました。

- GitHub issue から Copilot との新しい会話を開始した。
- Plan モードで要件を定義した。
- Autopilot モードで新機能を実装した。
- コードをレビューした。
- 転送されたブラウザーで機能を手動検証した。

次は、[カスタム instruction を使って][next-lesson]コードが文書化されたプラクティスに従うようにし、コード生成についてさらに詳しく確認します。

## リソース

- [GitHub Copilot CLI の Autopilot][autopilot]
- [Copilot CLI のコマンド リファレンス][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
