---
title: "Lesson 10 - 振り返りと次のステップ"
description: "Copilot CLI のワークフロー、2 つのプルリクエスト、再利用可能なカスタマイズ、参考リソースを振り返ります。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

GitHub Copilot CLI を使い、Tailspin Toys の一連のワークフローに取り組みました。具体的には、次の作業を行いました。

- Codespace を準備し、Copilot CLI をインストールして、プロジェクトを確認し、用意されたフィルタリングの issue を見つけた。
- 星評価を追加し、転送されたブラウザーで結果を確認して、最初のプルリクエスト (PR) を手動でマージした。
- フィルタリングの issue から始め、Plan モードでアプローチを定義し、Autopilot モードで構築して、Interactive モードでレビューした。
- カスタム instruction でエージェントを案内し、既存の `quality-checks` スキルをカスタマイズして、単体テスト、lint、型チェックを実行した。
- Playwright Model Context Protocol (MCP) サーバーを追加し、実際のブラウザーでフィルタリングを確認した。
- 品質保証 (QA) カスタムエージェントを作成・選択し、要件、テスト範囲、スキルの結果、ブラウザーでの根拠を評価した。
- フィルタリングの変更全体をレビューし、フィルタリングの PR で Agent Merge を承認した。
- コンテキスト、モデル、共有、任意のクラウド委任に使うスラッシュコマンドを確認した。

## リリースした内容

ワークショップでは、更新された `main` からそれぞれ別のブランチを作成し、2 つの PR を作成します。

1. **星評価:** 既存の `starRating` と、未評価であることを示す状態をゲームカードに表示します。
2. **フィルタリングと品質ワークフロー:** フィルタリングを実装し、instruction を更新して機能に適用します。`quality-checks` のレポートをカスタマイズし、QA プロファイルを作成して、関連するテストを追加します。

フィルタリングの計画から PR の作成までは、同じ会話とブランチを使いました。ワークショップを簡潔にするため、これらの作業を 1 つの PR にまとめました。

## さまざまな検証方法

自動テスト、ブラウザーでの手動確認、MCP を使った Copilot によるブラウザー確認など、複数の方法でコードを確認しました。`quality-checks` スキルでは単体テスト、lint、型チェックを実行し、追加した形式で結果を報告しました。QA は PR の前に、要件とテスト範囲のレビューと合わせて結果をまとめました。

追加するテストは実際の不足を補うものにしてください。新しいテストが不要という QA の結果も正しい場合があります。マージを承認する前にコードと根拠を確認し、変更後は影響を受ける検証結果を更新してください。

## ベスト プラクティス

Copilot に渡すコンテキストとツールによって、作業内容は変わります。このワークショップでは、instruction を更新し、スキルをカスタマイズし、QA プロファイルを作成し、MCP サーバーを構成しました。これらのカスタマイズは会話をまたいで再利用し、チームのニーズに合わせて調整できます。instruction は標準を定義し、スキルは繰り返し可能なタスクを記述し、カスタムエージェントは専門的な役割を定義し、MCP サーバーは外部ツールに接続します。エージェントの要約だけでなく、実際の変更とツールの結果を確認してください。

タスクに合わせて**モードとモデル**を選びます。構築前にアプローチを検討するには **Plan**、範囲を絞った変更で作業に関与し続けるには **Interactive**、範囲が明確なタスクには **Autopilot** を使います。定型的な編集には高速なモデル、複雑な作業には高性能なモデルを選びます。

インフラストラクチャと同じように、コンテキストも重要です。何を、なぜ、どのように構築するかを明確に説明すると、出力は大きく変わります。

## さらに試す

中心的なワークフローは完了しました。次に確認できる CLI の機能を紹介します。

- `/review` でコードレビューエージェントに変更を分析してもらう。
- `/rubber-duck` で問題について話し合い、別の視点を得る。
- `/fleet` で独立したサブタスクを並列に調整する。
- `/worktree` で別のタスクを分離する。
- `/delegate` でタスクを Copilot cloud agent に送る。

## 次のステップ

どのツールも、使い続けることが上達への近道です。実運用のコード、趣味のコード、長年考えていた小さなアプリなどで試してください。チームで知見を共有し、ほかの開発者からも学びましょう。ドキュメントも引き続き確認してください。

ターミナルから Tailspin Toys を拡張する場合は、オプションの [Foundry Backer Concierge シリーズ][foundry]に進みます。ほかの環境と比較するには、[VS Code ワークショップ][vscode]、[GitHub Copilot app ワークショップ][app]、または [Copilot cloud agent ワークショップ][cloud]を確認してください。

## リソース

- [GitHub Copilot CLI について][about-cli]
- [Copilot CLI のコマンド リファレンス][cli-reference]
- [Copilot CLI のカスタマイズ][customize-cli]
- [Copilot CLI でプルリクエストを管理する][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
