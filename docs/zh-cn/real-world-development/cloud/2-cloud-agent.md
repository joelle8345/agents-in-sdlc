---
title: "练习 2 - GitHub Copilot cloud agent"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 上一课：自定义指令][previous-lesson] |
|:--|

几乎所有组织都面临技术债务，例如尚未解决的安全问题、需要更新的旧代码，或因时间不足而长期搁置的功能请求。GitHub Copilot cloud agent 可以自主执行更新代码、添加功能等任务。完成工作后，它会创建草稿拉取请求 (PR)，供开发人员审查。这样可以将繁琐任务交给智能体，加快开发流程，让开发人员专注于更重要的工作。

通过 Copilot cloud agent，你将探索：

- 自定义代码生成环境。
- 确保操作安全执行。
- 明确限定议题范围的重要性。
- 将议题分配给 Copilot。

## 场景

Tailspin Toys 希望解决一些技术债务。最初受聘创建网站的承包商没有留下理想的文档——实际上，网站完全缺少文档。团队首先希望为应用程序中所有导出的函数添加 TSDoc 文档注释。

此外，设计团队准备改进游戏发现功能。他们希望游戏详情页显示相关游戏，也就是同一类别中的其他游戏，让访客可以继续浏览。暂时不需要精致的实现，只要能够用于用户体验验收测试即可。虽然这项工作目前受阻，但还有其他优先级更高的议题。

这两类任务都很容易被推迟，适合分配给 Copilot cloud agent。它可以在后台异步处理，开发人员则先处理其他工作，之后再回来审查结果。

## 认识 GitHub Copilot cloud agent

[GitHub Copilot cloud agent](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) 可以像开发人员一样在后台执行任务。可以通过多种方式分配工作，例如[将 GitHub 议题分配给 Copilot](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions)。分配后，Copilot 会创建草稿拉取请求以跟踪进度，设置环境并开始处理任务。你可以在会话进行中或完成后查看其工作。解决方案准备好供审查时，它会在拉取请求中通知你。

## 明确限定指令范围的重要性

GitHub Copilot 没有魔法，不能替你思考。看似简单的操作也可能有复杂细节，因此请[认真限定分配给 Copilot cloud agent 的任务范围][cloud-agent-best-practices]。将其视为人工智能 (AI) 结对编程伙伴：分阶段工作、学习、试验并根据情况调整。加入生成式 AI 并不会改变软件开发的基本原则。

## 本存储库中的自定义指令

前面的练习介绍了自定义指令及其作用。如果已完成自定义指令练习，你已经看到 `.github/copilot-instructions.md` 的效果；若还未完成，现在可以快速查看。在将任务分配给 Copilot cloud agent 之前，只读查看存储库中现有的指令文件，以便稍后观察其影响。

在存储库的 GitHub 网页界面或已运行的 codespace 中打开以下文件：

- `.github/copilot-instructions.md`：查看 **Code standards** 部分，尤其是 TypeScript 约定和 TSDoc 文档注释要求。
- `.github/instructions/unit-tests.instructions.md`：查看 `applyTo` frontmatter，它将指令限定到 `**/*.test.ts` 文件。

下一节将 `Code lacks documentation` 议题分配给云端智能体时，注意生成的 PR 是否包含 TSDoc 文档注释、TypeScript 约定和文件注释头。这些要求来自上述指令文件，后续练习审查 PR 时还会再次查看。

## 为 Copilot cloud agent 设置开发环境

编写代码通常需要特定环境，并需要运行设置脚本，确保环境状态正常。将任务分配给 Copilot 也一样，因为它会以类似软件工程师的方式执行任务。

云端智能体使用 [GitHub Actions][github-actions] 作为工作环境。你可以通过 `.github/workflows/copilot-setup-steps.yml` 配置[专用设置工作流][setup-workflow]，在它开始工作前安装所需开发工具和依赖项。该工作流已预先配置，方便完成实验；它会为 Copilot 安装 Node.js、项目依赖项、端到端测试所需的浏览器二进制文件，并为单体 Astro 应用准备完成迁移和数据填充的 SQLite 数据库：

```yaml
name: "Copilot Setup Steps"

# 允许你在存储库的 "Actions" 选项卡中测试设置步骤
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # 将权限设置为你的步骤所需的最低级别。Copilot 会获得自己的操作令牌。
    permissions:
      # 如果设置步骤需要克隆存储库（例如安装依赖项），则需要 `contents: read` 权限。如果不在设置步骤中克隆存储库，Copilot 会在步骤完成后自动为你克隆。
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # 前端/应用设置 - Node.js（整个应用现为 Astro + Drizzle/libSQL）
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # 迁移并填充本地 SQLite 数据库，为构建和测试准备数据。
      - name: Set up the database
        run: npm run db:setup
```

它看起来与其他 GitHub 工作流类似，但有几个关键点：

- 其中只有一个名为 `copilot-setup-steps` 的作业。该作业会在 Copilot 开始处理 PR 前由 GitHub Actions 执行。
- `workflow_dispatch` 触发器允许你在存储库的 **Actions** 选项卡中手动运行工作流。这便于测试工作流是否成功，而不必等待 Copilot 触发。

## 添加文档

大多数项目都存在过时信息或完全缺少文档的问题。这类技术债务常常无人处理，会降低效率、增加维护难度，也让新开发人员更难加入团队。Copilot 擅长生成文档，因此很适合将此类议题分配给 Copilot cloud agent。它会在后台生成所需文档，稍后的练习会审查其工作。

1. 在新的浏览器选项卡中打开 github.com 上的存储库。
2. 选择 **Issues** 选项卡。
3. 选择 **New issue** 打开新议题对话框。
4. 选择 **Blank issue** 创建空白议题。
5. 将 **Title** 设置为 `Code lacks documentation`。
6. 将 **Description** 设置为：

   ```plaintext
   Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
   ```

7. 选择 **Create** 创建议题。
8. 在右侧选择 **Assign to Copilot** 打开分配对话框。

   ![将 Copilot 分配给议题](../../../_images/shared-assign-copilot.png)

9. 选择 **Assign**。
10. 选择 **Pull Requests** 选项卡。
11. 打开新生成的拉取请求 (PR)，标题类似 `[WIP]: Code lacks documentation`。如果列表中尚未出现新 PR，请稍等片刻并刷新浏览器。
12. 几分钟后，Copilot 应会创建待办事项列表。

> [!NOTE]
> Copilot 的待办事项列表可能需要几分钟才会显示在 PR 中。Copilot 正在创建环境（运行前面介绍的工作流）、分析项目并确定最佳处理方案。

13. 查看待办列表及其计划执行的任务。
14. 向下滚动 PR 时间线，查看 Copilot 已开始处理议题的更新。
15. 选择 **View session** 按钮。

   ![Copilot 会话视图](../../../_images/ex4-view-session.png)

> [!CAUTION]
> 可能需要刷新窗口才能看到更新后的状态指示器。

16. 浏览实时会话，查看 Copilot 如何解决问题，包括探索代码、了解当前状态、暂停思考并确定适当计划，以及生成代码。

这可能需要几分钟。Copilot cloud agent 的主要目标之一是异步执行任务，让开发人员可以专注于其他工作。接下来利用这一能力，再给云端智能体分配另一项任务，然后转而为应用编写新功能。

## 在游戏详情页添加相关游戏

GitHub Copilot cloud agent 的一个重要优势是能够分担工作，让你专注于一组任务，而智能体处理另一组任务。即使为设计团队添加相关游戏区域不一定要花很长时间，也可以利用这段时间处理其他工作。现在将此任务分配给 Copilot cloud agent。

1. 返回 github.com 上的存储库。
2. 选择 **Issues** 选项卡。
3. 选择 **New issue** 打开新议题对话框。
4. 选择 **Blank issue** 使用空白模板。
5. 将 **Title** 设置为 `Show related games on the game details page`。
6. 将 **Description** 设置为：

   ```markdown
   We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
   ```

7. 选择 **Create** 创建议题。
8. 在右侧选择 **Assign to Copilot** 打开分配对话框。

   ![将 Copilot 分配给议题](../../../_images/shared-assign-copilot.png)

9. 选择 **Assign**。

稍后，你会看到议题的第一条评论中出现一组 👀，表示 Copilot 已开始处理。

![Copilot 使用眼睛表情符号表示正在处理议题](../../../_images/ex4-issue-eyes-emoji.png)

Copilot 正在处理第二项请求。Copilot cloud agent 的工作方式与软件工程师相似，因此无需持续监控，完成后再审查即可。现在转而创建并使用自定义智能体。

## 总结和后续步骤

本课介绍了 [GitHub Copilot cloud agent][copilot-agents]。你可以将议题分配给云端智能体，让它异步处理。可以用 Copilot 解决技术债务、创建新功能，或协助将代码从一个框架迁移到另一个框架。

本课探索了以下内容：

- 自定义代码生成环境。
- 确保操作安全执行。
- 明确限定议题范围的重要性。
- 将议题分配给 Copilot。

云端智能体正在后台工作，现在可以转而创建并使用自定义智能体。[Copilot cloud agent 也可使用模型上下文协议 (MCP) 服务器][cloud-agent-mcp]，并且可以使用前面模块介绍的自定义指令。

## 资源

- [关于 Copilot cloud agent][copilot-agents]
- [将 GitHub 议题分配给 Copilot][assign-issue]
- [Copilot cloud agent 设置工作流最佳实践][cloud-agent-best-practices]

| [下一课：自定义智能体 →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
