---
title: "练习 0：先决条件"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

开始 Copilot cloud agent 练习前，需要先做好准备。你将创建 Tailspin Toys 存储库副本，并启动一个 [codespace][codespaces]，用于编辑指令文件和审查云端智能体生成的工作。

## 设置实验存储库

从[模板存储库][template-repository]创建自己的存储库副本。新副本包含实验所需的所有文件，后续练习都会使用它。

1. 在新的浏览器窗口中打开 [Tailspin Toys 模板][tailspin-template]。
2. 在实验存储库页面选择 **Use this template**，然后选择 **Create a new repository**。

   ![Use this template 按钮](../../../_images/ex0-use-template.png)

3. 如果你正在参加 GitHub 或 Microsoft 主办的活动，请遵循导师提供的说明。否则，可以在你有权使用 GitHub Copilot 的组织中创建新存储库。

   ![存储库模板设置输入界面](../../../_images/ex0-repository-settings.png)

4. 记下创建的存储库路径（**organization-or-user-name/repository-name**），后续实验中会用到。

## 创建 codespace

接下来，使用 codespace 完成实验练习。

[GitHub Codespaces][codespaces] 是基于云的开发环境，可让你直接在浏览器中编写、运行和调试代码。它提供功能齐全的集成开发环境 (IDE)，支持多种编程语言、扩展和工具。

1. 打开新建的存储库。
2. 选择绿色的 **Code** 按钮。

   ![选择 Code 按钮](../../../_images/ex0-code-button.png)

3. 选择 **Codespaces** 选项卡，再选择 **+** 按钮创建新的 Codespace。

   ![创建新的 codespace](../../../_images/ex0-create-codespace.png)

创建 codespace 需要几分钟，但仍比手动安装所有服务快得多。等待期间可以探索 GitHub Copilot 的其他功能，接下来的练习会介绍这些功能。

> [!CAUTION]
> 后续练习还会返回此 codespace。现在先让它保持打开，并保留在浏览器选项卡中。

> [!NOTE]
> 本工作坊可以在 codespace 或本地 [dev container][dev-containers] 中运行。两者都会安装顺利完成工作坊所需的先决条件。如果要在本地运行，请在 VS Code 中打开克隆的存储库，并在提示时选择 **Reopen in Container**。VS Code 会构建与 codespace 相同的 dev container。

## 总结

恭喜！你已创建实验存储库副本，并开始创建 codespace。后续练习会在此环境中与 Copilot cloud agent 协作。

## 下一步

接下来添加云端智能体要遵循的自定义指令。继续学习[练习 1 - 自定义指令][next-lesson]。

## 资源

- [GitHub Codespaces 概述][codespaces]
- [从模板创建存储库][template-repository]
- [Codespaces 入门][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[next-lesson]: ../1-custom-instructions/
[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers
