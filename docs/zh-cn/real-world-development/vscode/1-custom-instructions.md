---
title: "练习 1 - 自定义指令（VS Code）"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 上一课：先决条件][previous-lesson] · [下一课：智能体模式 →][next-lesson]

使用生成式 AI 时，上下文至关重要。如果任务需要以特定方式完成，或 Copilot 需要了解背景信息，就应确保它能获取这些上下文。可以通过多种方式向 Copilot 提供特定上下文，其中重要的一种是[指令文件][instruction-files]，它用于说明代码生成方面的指导。

在本练习中，你将：

- 探索项目特定上下文、编码指南和文档规范如何通过存储库自定义指令及按路径限定的指令文件传递给 Copilot。
- 在当前指令下生成筛选功能的第一个数据切片（发行商辅助函数）。
- 在 `.github/copilot-instructions.md` 中添加一条新的全局存储库规范。
- 再次运行相同提示，观察生成的代码如何采用新规范。
- 将指令更新和筛选功能切片提交到 `main`，以便 Copilot 在下一练习中使用更新后的指导。

> [!CAUTION]
> 生成的代码可能不完全符合某些规范。Copilot 具有概率性而非确定性。本练习旨在观察更新指令后行为的总体变化，而不是逐字匹配输出。

## 指令文件

### 场景

Tailspin Toys 制定了一系列开发实践指南和要求，包括：

- 数据层始终需要单元测试。
- UI 应使用深色模式并具有现代感。
- 应使用 TSDoc 文档注释为代码添加文档。
- 每个文件开头都应添加说明文件用途的注释块。

使用指令文件可以确保 Copilot 获取正确的信息，并按照这些实践完成任务。

### 自定义指令

自定义指令为 Copilot 提供上下文和偏好，帮助它理解编码风格和要求。可以指定编码约定、库以及注释规范等。指令可以应用于整个存储库，也可以应用于特定文件类型，为任务提供上下文。

指令文件有两种：

- `.github/copilot-instructions.md` 是发送给 Copilot 的单个指令文件，适用于该存储库的**每个**请求。它应包含与大多数请求相关的项目级信息。
- `.github/instructions/*.instructions.md` 文件可针对特定语言、文件类型或任务提供指南。

> [!NOTE]
> 不同环境对其他指令格式的支持各不相同。依赖特定格式前，请查看[自定义指令支持参考][custom-instructions-support]。

### 管理指令文件的最佳实践

完整讨论如何创建指令文件超出了本工作坊的范围。不过，示例项目展示了有代表性的做法：

- 将 `copilot-instructions.md` 限定为项目级指导，例如项目说明、结构和全局编码规范。
- 使用 `*.instructions.md` 文件为文件类型（单元测试、Astro 组件、数据层）或特定任务提供具体指导。
- 使用自然语言，保持指导清晰，并提供代码示例说明推荐和不推荐的写法。

创建指令文件没有唯一正确的方法，使用 AI 也是如此。通过实践找到最适合项目的做法。

> [!TIP]
> 每个使用 GitHub Copilot 的项目都应有一套完善的指令文件。浏览本项目的指令文件时，可能会看到针对[界面更新][ui-instructions]和 [Astro][astro-instructions] 等任务的文件。
>
> Copilot 也可以帮助生成指令文件。不同产品界面的操作方式不同，例如 VS Code 中的 **Configure Chat → Generate Agent Instructions**，或 Copilot CLI 中的 `/init`。相关课程会在适用时说明具体操作。
>
> 需要模板或入门示例？可以浏览 [awesome-copilot][awesome-copilot]，其中包含指令文件、自定义智能体和其他资源。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## 探索项目中的自定义指令文件

入门项目已包含一组指令文件。先浏览现有文件，再进行更改，观察其效果。

1. 返回 Codespace。
2. 在 Codespaces 编辑器（不是终端）中打开 `.github/copilot-instructions.md`。
3. 浏览文件，留意项目简介和编码指南。这些指令适用于你在此存储库中与 Copilot 的所有交互。
4. 打开 `.github/instructions` 文件夹并浏览其中内容，注意 Astro 文件、Drizzle 数据层、测试等指令。
5. 打开 `.github/instructions/unit-tests.instructions.md`。查看顶部的 `applyTo` 字段，它设置了决定适用文件的 glob。
6. 打开 `.github/instructions/drizzle.instructions.md`，查看其中指向其他指令文件和项目现有文件的链接。这些链接可将较大的指令集拆分为可复用文件，并为 Copilot 提供示例。

> [!NOTE]
> `copilot-instructions.md` 中的 **Code formatting requirements** 部分记录了项目编码规范，但目前尚未要求在代码中添加文档。接下来将添加 TSDoc 文档注释和文件注释头的规则。

## 为更改创建分支

遵循最佳实践，为更改创建分支。

1. 返回上一练习中使用的 codespace。
2. 按 <kbd>Control</kbd>+<kbd>`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（Windows/Linux）打开新终端。
3. 创建并切换到新分支：

   ```bash
   git checkout -b custom-instructions
   ```

## 更新指令前先使用 Copilot Chat

> [!TIP]
> **打开 Copilot Chat**
>
> 开始以下练习前，返回 codespace，打开 Copilot Chat 面板并选择 **New Chat**，开始一个干净的对话。各练习中的模式和模型选择可能不同，步骤会在适用时说明。

要了解自定义指令的影响，先在当前指令文件下发送提示。稍后更新指令后，再发送相同提示并比较结果。

1. 关闭之前练习中打开的编辑器选项卡，让 Copilot 仅获取所需上下文。
2. 打开 `src/lib/publishers.ts`，让 Copilot 知道辅助函数应放在哪里。
3. 在 Chat 视图的智能体下拉菜单中选择 **Agent**，使 Copilot 能够应用文件更改。

   ![Chat 视图中的智能体选择器](../../../_images/shared-chat-mode-selector.png)

4. 发送以下提示：

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

5. Copilot 会探索项目并应用代码更新，通常会同时修改辅助函数文件及其测试。
6. 注意生成的辅助函数是带类型的函数，以 `db` 客户端作为第一个参数，并返回带类型的发行商数组。这来自 `.github/instructions/drizzle.instructions.md` 中适用于 `src/lib/*.ts` 的数据层约定。
7. 注意生成的代码**没有** TSDoc 文档注释和文件级注释头。

> [!CAUTION]
> Copilot 具有概率性，因此即使没有明确要求，也可能添加文档注释。如果发生这种情况也没问题；本练习的重点仍是观察更新指令后行为的一致性变化。

## 添加新的存储库规范

如前所述，`.github/copilot-instructions.md` 用于向 Copilot 提供项目级信息。现在添加编码规范，以改进代码建议。

1. 重新打开 `.github/copilot-instructions.md`。
2. 找到 **Code formatting requirements** 部分（应在第 27 行附近）。注意此处记录了项目编码规范，但尚无代码文档规则，因此生成的辅助函数没有文档注释。
3. 在现有规范下方添加以下 Markdown，要求 Copilot 添加文件注释头和 TSDoc 文档注释：

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. 保存 `copilot-instructions.md`。

> [!TIP]
> 如前一课所示，指令文件可以放在存储库级别（`.github/copilot-instructions.md`）提供全局指导，也可以使用 `*.instructions.md` 文件为特定语言、文件类型或任务提供指导。你刚添加的文档注释规则属于全局项目规范，因此适合放在存储库级文件中。

## 重新运行提示并观察变化

1. 返回 Copilot Chat，选择 **New Chat** 清除上下文。
2. 再次选择 `src/lib/publishers.ts`，让 Copilot 聚焦于正确文件。
3. 发送与之前**完全相同的提示**：

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

4. 注意生成的文件现在以类似以下注释块开头：

   ```typescript
   /**
    * Publisher data-access helpers for the Tailspin Toys Crowd Funding platform.
    * Provides functions to retrieve publisher information from the database.
    */
   ```

5. 注意生成的函数现在包含类似以下的 TSDoc 注释：

   ```typescript
   /**
    * Returns a list of all publishers with their id and name.
    *
    * @param db - The Drizzle database client.
    * @returns A promise that resolves to an array of publisher objects.
    */
   ```

你已引导 Copilot 遵循新的项目规范，并将其应用于实际代码，下一练习会在此基础上继续开发。

## 提交指令并推送分支

指令文件和其他项目资源一样，应通过源代码管理进行维护。现在提交并推送分支。

1. 按 <kbd>Control</kbd>+<kbd>`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（Windows/Linux）打开新终端。
2. 在终端中运行以下命令，确认指令更新和辅助函数更改已存在：

   ```bash
   git status
   ```

3. 暂存并提交指令更新，以及 Copilot 为辅助函数基础修改的所有文件：

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # If git status shows additional supporting updates (for example tests), add those files too.
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

4. 将分支推送到存储库：

   ```bash
   git push -u origin custom-instructions
   ```

## 创建并合并拉取请求

分支推送后，创建拉取请求并关联待办事项中的文档规范议题。也可以手动完成，不过 Copilot 已连接项目 GitHub 工具，可以让它查找议题、创建 PR 并关闭议题，然后合并 PR。

> [!NOTE]
> 这是第一次让 Copilot 代表你操作 GitHub。项目模板已在工作区中配置 GitHub 工具，无需额外设置。Copilot 首次使用时，VS Code 可能会提示你登录 GitHub。按照提示授权即可。稍后课程会介绍此连接使用的模型上下文协议 (MCP)。

1. 在 codespace 中打开 Copilot Chat。
2. 按 <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd>（Windows/Linux）打开 Copilot Chat 视图，并确认智能体选择器中选中 **Agent**。
3. 让 Copilot 查找与指令文件更新相关的议题，并从当前分支创建 PR，说明指令更新和新增的发行商辅助函数基础：

   ```plaintext
   Find the issue related to updating the instructions file. Create a new PR from the current branch, highlight that the PR closes that issue, and include that we also added the publishers helper foundation for the upcoming filtering work.
   ```

4. Copilot 会开始查找议题并创建 PR。
5. 如果系统提示 **Allow** Copilot 代表你执行 GitHub 操作，请先审查命令，再酌情选择 **Allow**。
6. 创建 PR 后，使用以下提示让 Copilot 合并 PR 并将分支切回 main：

   ```plaintext
   Merge the PR into main. Then return to main locally, and pull the latest code so we are up to date.
   ```

7. 如果系统提示 **Allow** Copilot 代表你执行 GitHub 操作和 shell 命令，请先审查命令，再酌情选择 **Allow**。

现在，你已借助 GitHub Copilot 创建并合并了拉取请求。

## 总结和后续步骤

你已探索 Copilot 如何从指令文件获取上下文，并使用 VS Code 中的 Copilot Chat：

- 发送代码生成提示，观察 Copilot 根据**现有**指令生成的结果。
- 在 `.github/copilot-instructions.md` 中添加新的全局存储库规范。
- 再次发送相同提示，观察生成的代码如何采用新规范。
- 将指令更新和辅助函数基础提交到 `main`，以便下一练习继续使用。

接下来，在[智能体模式][next-lesson]中使用这些指令，让 Copilot 跨代码库添加新功能。

## 资源

- [用于自定义 GitHub Copilot 的指令文件][instruction-files]
- [创建自定义指令的最佳实践][instructions-best-practices]
- [编写更好的 Copilot 自定义指令的 5 个技巧][copilot-instructions-five-tips]
- [GitHub Copilot 个人自定义指令][personal-instructions]
- [Awesome Copilot：指令文件及其他资源合集][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
