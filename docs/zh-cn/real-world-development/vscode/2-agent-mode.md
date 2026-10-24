---
title: "练习 2 - 使用 Copilot Agent Mode 添加新功能"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

即使是最简单的应用更新，通常也需要修改多个文件并执行测试等操作。开发人员的工作流程通常包括查找所有相关文件、进行更改、运行测试、调试、找出遗漏文件并再次修改，过程可能反复进行。

Copilot Agent Mode 正适合处理这类任务。

Copilot Agent Mode 可在集成开发环境 (IDE) 中更自主地工作。它会先探索现有项目结构，再执行必要更新、运行测试等任务，并自动修复发现的问题。下面来了解如何使用 Agent Mode 为网站添加新功能。

> [!NOTE]
> 名称相似，但智能体模式和云端智能体适用于两种不同体验。智能体模式在 IDE 中执行任务，可快速反馈和交互。云端智能体则像团队中的结对程序员一样异步工作，通过议题和拉取请求与你协作。

在本练习中，你将了解：

- Copilot Agent Mode 如何探索项目、识别相关文件并协调进行更改。
- GitHub Copilot Agent Mode 如何跨用户界面 (UI) 和数据层实现新功能。
- 如何在合并前审查 Copilot Agent Mode 生成的更改和测试。

## 场景

随着游戏列表增长，你希望用户能够按类别和发行商筛选。上一练习已添加发行商辅助函数，现在将使用 Copilot Agent Mode 完成数据层、UI 和测试的其余工作。

## 运行 Tailspin Toys 网站

修改代码前，先浏览 Tailspin Toys 网站，了解其当前功能。

该网站是一个以开发者为主题的桌游众筹平台，允许用户浏览游戏列表并查看详情。它是一个单体 Astro 应用，在构建时将页面渲染为静态超文本标记语言 (HTML)。页面通过 Drizzle ORM 在 frontmatter 中直接查询本地 SQLite 数据库；没有单独的后端应用程序编程接口 (API) 或客户端 UI 框架。可复用的数据访问辅助函数位于 `src/lib/`，交互功能则使用标准文档对象模型 (DOM) API 编写小型、范围明确的 Astro `<script>`。

### 启动网站

项目提供了 `npm run dev` 任务，用于启动单体 Astro 开发服务器。在 GitHub Codespace 中按以下步骤运行：

1. 返回 codespace。上一练习后应已切回 `main`。
2. 按 <kbd>Control</kbd>+<kbd>`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（Windows/Linux），在 Codespace 中打开新终端。
3. 创建并切换到筛选功能分支：

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. 运行以下命令启动网站：

   ```bash
   npm run dev
   ```

   Astro 开发服务器准备就绪后，应会显示类似以下的提示：

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> 如果出现提示，询问是否打开 `http://localhost:4321` 的浏览器窗口，请选择 **x** 关闭对话框。

5. 按住 <kbd>Command</kbd>（Mac）或 <kbd>Ctrl</kbd>（Windows/Linux），然后在终端中选择 Astro 服务器地址 `http://localhost:4321`，打开网站。

> [!NOTE]
> 在 codespace 中选择终端里的 localhost URL 时，系统会自动将其重定向到 `https://<your-codespace-name>-4321.app.github.dev/`。这是指向 codespace 的专用隧道，此时网站服务器正在 codespace 中运行。

### 浏览网站

网站启动后，可以查看其功能，主要包括：

- **主页**：显示桌游列表及其标题、图片和说明。
- **游戏详情页**：选择游戏后会打开详情页，显示游戏标题、说明、发行商和类别等信息。

## 使用 Copilot 探索待办事项

> [!TIP]
> **打开 Copilot Chat**
>
> 开始以下练习前，返回 codespace，打开 Copilot Chat 面板并选择 **New Chat**，开始一个干净的对话。各练习中的模式和模型选择可能不同，步骤会在适用时说明。

网站的初始版本可以正常使用，但我们希望增加新功能。先查看待办事项。使用模板设置项目时，系统已自动创建一组议题。让 GitHub Copilot 显示这些议题。

1. 在 Chat 视图的智能体下拉菜单中选择 **Agent**。**Agent** 智能体可以自主规划并跨文件实现更改、运行终端命令和调用工具。

   ![Chat 视图中的智能体选择器](../../../_images/shared-chat-mode-selector.png)

2. 从可用模型列表中选择 **Claude Sonnet 4.5**。

> [!CAUTION]
> 本工作坊的作者并未表示偏好任何特定模型。编写本工作坊时使用了 Claude Sonnet 4.5，因此说明中也列出了它，希望代码建议相对一致，从而提供良好体验。但由于大型语言模型具有概率性，你看到的建议可能与工作坊示例不同，这是正常且预期的情况。

> [!NOTE]
> 由于大型语言模型 (LLM) 具有概率性，Copilot 可能会使用不同的模型上下文协议 (MCP) 命令，但仍应能够完成任务。

3. 向 Copilot 发送以下提示，询问待办事项中的议题：

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. 选择 **Continue** 运行列出所有议题的命令。
5. 查看生成的议题列表。

注意 Copilot 还根据它认为对用户最有帮助的程度，为待办事项排定了优先级。

## 审查指令文件

让智能体生成代码前，先查看用于向 Copilot 提供工作上下文的指令文件。本练习会使用[用户界面 (UI)](https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md) 文件，其中说明了如何为网站添加功能。

1. 在 codespace 中打开 `.github/instructions/ui.instructions.md`。
2. 查看添加功能的总体指南，包括：
   - 架构概述。
   - 组件设计、可测试性和无障碍原则。
   - 指向 Astro、Tailwind CSS 和 Drizzle 等特定文件类型指令的链接。

> [!TIP]
> 指令文件可以引用其他指令文件，也可以引用项目中的文件。路径相对于指令文件所在位置。这样可以复用指导、拆分复杂指令，并提供示例和模板。

## 实现筛选功能

要完成筛选功能，至少需要对应用进行三项独立更新：

- 添加或完善数据层 (`src/lib/`) 中剩余的筛选逻辑。
- 添加或更新筛选行为测试。
- 更新游戏列表页，加入筛选 UI。

此外，合并前还需要运行并通过测试。Copilot Agent Mode 可以代为完成这些任务，现在开始添加功能。

1. 可以继续当前 Copilot 对话，也可以选择 **New Chat** 开始新对话。
2. 选择 **Add Context**、**Instructions** 和 **ui** 指令文件。

   ![选择 UI 指令文件的示例](../../../_images/ex3-select-instructions-file.png)

3. 确认 Chat 视图的智能体下拉菜单中仍选中 **Agent**。

   ![Chat 视图中的智能体选择器](../../../_images/shared-chat-mode-selector.png)

4. 确认仍选中模型 **Claude Sonnet 4.5**。
5. 使用以下提示，根据待办事项中的相关议题实现功能：

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. 观察 Copilot 如何先探索项目，找到与功能相关的文件。它应会找到数据层辅助函数、UI 和测试，然后修改文件并运行测试。

   ![Copilot 正在探索项目文件](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot 会执行多项任务，例如探索项目、修改文件和运行测试。根据任务和代码库复杂程度，可能需要几分钟。过程中，代码编辑器可能会显示 **Keep** 和 **Undo** 按钮。Copilot 完成后，所有更改都会显示 **Keep** 或 **Undo** 选项，因此无需在工作进行时选择。

7. Copilot 提示时，选择 **Continue** 运行测试。

   ![Copilot Chat 窗格中的对话框，询问用户是否同意运行测试](../../../_images/ex3-agent-mode-run-tests.png)

8. 过程中可能会暂停，甚至有测试暂时失败。这没有关系。Copilot 会在生成代码和运行测试之间反复迭代，直到完成任务且不再发现错误。

   ![Copilot Agent Mode 完整对话会话](../../../_images/ex3-agent-mode-proposed-changes.png)

9. 检查生成的代码，留意潜在问题。

> [!CAUTION]
> 务必审查 Copilot 或任何人工智能 (AI) 工具生成的代码。

10. 返回正在运行网站的浏览器，体验新功能。
11. 确认功能正常并审查代码后，在 Copilot Chat 窗口中选择 **Keep**。

## 总结和后续步骤

恭喜！在本练习中，你使用 GitHub Copilot Agent Mode 为 Tailspin Toys 网站添加了新功能。你了解了：

- GitHub Copilot Agent Mode 如何跨 UI 和数据层实现新功能。
- Copilot Agent Mode 如何探索项目、识别相关文件并协调进行更改。
- 如何在合并前审查 Copilot Agent Mode 生成的更改和测试。

接下来，使用 [Playwright MCP 服务器测试功能][next-lesson]，并为其创建拉取请求。

### 奖励探索练习——实现分页

随着游戏列表增长，网站需要支持分页。使用本练习学到的技能，让 Copilot 更新网站，实现分页。提示中可以考虑：

- 遵循现有最佳实践，包括使用现有指令文件。
- 确定分页方式，例如允许用户选择每页条目数，或使用固定数值。
- 编写提示时提供 Copilot 所需的指导，使实现符合预期。
- 可能需要与 GitHub Copilot 迭代，提出更改请求并提供上下文。这是使用 Copilot 的正常流程。

## 资源

- [Copilot 的 ask、edit 和 agent 模式：功能与适用场景][choose-mode]
- [VS Code 中的智能体模式][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
