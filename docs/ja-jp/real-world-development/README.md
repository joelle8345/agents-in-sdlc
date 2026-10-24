---
title: "実践的な開発"
slug: ja-jp/real-world-development
authors:
  - geektrainer
lastUpdated: 2026-09-16
---

現実的なシナリオ、完成したアプリケーション、共有バックログを使って、ソフトウェア開発ライフサイクル全体で GitHub Copilot を活用します。変更の計画、コードの作成、動作のテスト、プルリクエストのレビュー、エージェントを使った作業管理を繰り返しながら進めます。

## シナリオ

ボードゲームのクラウドファンディングを開発者向けテーマで提供する架空の企業、Tailspin Toys に新しく参加した開発者として作業します。チームのバックログは GitHub issue として登録済みなので、すぐに作業を選べます。機能追加にはフィルタリングやページネーション、品質改善にはアクセシビリティやコーディング規約への対応が含まれています。

## 開発環境を選ぶ

GitHub Copilot は、開発者が作業する環境で利用できます。使いたい開発環境を選んでください。各ワークショップでは、それぞれのセットアップから始め、共通の Tailspin Toys シナリオに取り組みます。

### [GitHub Copilot CLI][cli]

ターミナルでエージェント型アシスタントを使います。Plan モードと Autopilot モード、instruction、スキル、カスタムエージェント、Playwright Model Context Protocol (MCP)、Agent Merge、実用的なスラッシュコマンドを扱います。

### [GitHub Copilot app][app]

エージェントセッションを並行して実行し、セッションモードを切り替え、Canvas で共同作業を行い、デスクトップアプリで GitHub issue とプルリクエストを管理します。

### [GitHub Copilot cloud agent][cloud]

GitHub issue を非同期エージェントに割り当て、作業を案内して進捗を監視し、エージェントが作成したプルリクエストをレビューします。

### [Visual Studio Code][vscode]

Visual Studio Code と GitHub Codespaces で GitHub Copilot を使います。Copilot Chat のエージェントモード、MCP サーバー、カスタムエージェントをエディターから離れずに利用します。

[cli]: cli/
[app]: app/
[cloud]: cloud/
[vscode]: vscode/
