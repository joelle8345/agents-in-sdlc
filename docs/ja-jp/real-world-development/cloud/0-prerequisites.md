---
title: "Exercise 0: 前提条件"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Copilot cloud agent の演習を始める前に、準備が必要です。Tailspin Toys リポジトリの自分用コピーを作成し、instruction file の編集と cloud agent が作成した作業のレビューに使う [Codespace][codespaces] を起動します。

## ラボ用リポジトリを設定する

コード作成に使うリポジトリのコピーを作ります。[テンプレート][template-repository]からインスタンスを作成します。新しいインスタンスにはラボに必要なすべてのファイルが含まれています。

1. 新しいブラウザーウィンドウで [Tailspin Toys テンプレート][tailspin-template]を開きます。
2. ラボ用リポジトリのページで **Use this template** ボタンを選択し、**Create a new repository** を選択して自分用コピーを作成します。

    ![Use this template ボタン](../../../_images/ex0-use-template.png)

3. GitHub または Microsoft が主催するイベントの一環としてワークショップに参加している場合は、メンターの指示に従ってください。それ以外の場合は、GitHub Copilot を利用できる Organization に新しいリポジトリを作成できます。

    ![リポジトリのテンプレート設定を入力する画面](../../../_images/ex0-repository-settings.png)

4. 作成したリポジトリのパス (**organization-or-user-name/repository-name**) を記録します。ラボの後半で使用します。

## Codespace を作成する

次に、Codespace を使ってラボの演習に取り組みます。

[GitHub Codespaces][codespaces] は、ブラウザーから直接コードの作成、実行、デバッグを行えるクラウドベースの開発環境です。複数のプログラミング言語、拡張機能、ツールに対応した IDE を利用できます。

1. 作成したリポジトリを開きます。
2. 緑色の **Code** ボタンを選択します。

    ![Code ボタンを選択する画面](../../../_images/ex0-code-button.png)

3. **Codespaces** タブを選択し、**+** ボタンを選択して新しい Codespace を作成します。

    ![新しい Codespace を作成する画面](../../../_images/ex0-create-codespace.png)

Codespace の作成には数分かかりますが、必要なサービスを手動でインストールするよりはるかに短時間で済みます。作成中に GitHub Copilot のほかの機能を確認できます。次はそれらの機能を見ていきます。

> [!CAUTION]
> 今後の演習でこの Codespace に戻ります。今はブラウザーのタブを開いたままにしてください。

> [!NOTE]
> このワークショップは Codespace またはローカルの [開発コンテナー][dev-containers]内で実行するように構成されています。どちらも必要な前提条件がインストールされた環境を提供します。ローカルで実行する場合は、クローンしたリポジトリを VS Code で開き、メッセージが表示されたら **Reopen in Container** を選択します。Codespace と同じ開発コンテナーが構築されます。

## まとめ

ラボ用リポジトリのコピーを作成し、Copilot cloud agent と並行して作業するために使う Codespace の作成を開始しました。

## 次のステップ

次は、cloud agent が従うカスタム instruction を追加します。[演習 1「カスタム instruction」][next-lesson]に進みます。

## リソース

- [GitHub Codespaces の概要][codespaces]
- [テンプレートからリポジトリを作成する][template-repository]
- [Codespaces の使用を開始する][codespaces-quickstart]

[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers
[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[next-lesson]: ../1-custom-instructions/
