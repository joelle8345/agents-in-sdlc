---
title: "第 4 课 - 使用自定义指令引导 Copilot"
description: "探索存储库指令，添加文档规范，并将其应用于筛选代码。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

使用生成式人工智能 (AI) 时，上下文至关重要。如果任务需要按特定方式完成，就应让 Copilot 能够获取相关指导。[指令文件][instruction-files]不仅说明希望编写什么代码，也说明代码应如何组织。现在你已构建筛选功能，接下来将探索 Copilot 使用的指令、添加文档规范，并将其应用到代码中。

在本课中，你将：

- 探索存储库指令和按路径限定的指令文件如何传递给智能体。
- 更新指令文件，确保遵循编码规范。
- 了解指令文件对代码的影响。

## 场景

Tailspin Toys 制定了一系列开发规范和要求，包括：

- 注释应说明意图和不明显的决策，而不是复述代码。
- `db/` 和 `src/lib/` 中导出的函数应使用 TSDoc/JSDoc 说明用途、参数和返回值；如果存在可注入的 `db` 参数，也应记录。
- 可复用 Astro 组件应说明其 `Props` 契约；相关代码更改时，注释也应保持最新。
- 应保留现有格式和 lint 指南。

通过指令文件，确保 Copilot 获得必要信息，以遵循这些实践完成任务。

## 指令文件

自定义指令为 Copilot 提供上下文和偏好，帮助它理解编码风格和要求。可以指定编码约定、库以及注释规范等。指令可以应用于整个存储库，也可以应用于特定文件类型，为任务提供上下文。

指令文件有两种：

- `.github/copilot-instructions.md` 是发送给 Copilot 的单个指令文件，适用于该存储库的**每个**请求。它应包含适用于大多数请求的项目级信息。
- `.github/instructions/*.instructions.md` 文件可针对特定语言、文件类型或任务提供指南。

> [!NOTE]
> 不同环境对其他指令格式的支持各不相同。依赖特定格式前，请查看[自定义指令支持参考][custom-instructions-support]。

## 探索项目中的自定义指令文件

启动项目时已包含一组指令文件。先查看现有文件，再进行更改，观察其效果。

1. 返回 Codespace。
2. 在 Codespaces 编辑器（不是终端）中打开 `.github/copilot-instructions.md`。
3. 查看项目简介和编码指南。此文件适用于 Copilot 在此存储库中的所有交互。
4. 打开 `.github/instructions` 文件夹并浏览文件，其中包含 Astro、Drizzle 数据层、测试等方面的指令。
5. 打开 `.github/instructions/unit-tests.instructions.md`。查看顶部的 `applyTo` 字段，它设置了决定适用文件的 glob。
6. 打开 `.github/instructions/drizzle.instructions.md`，查看其中指向其他指令文件和项目现有文件的链接。这些链接可将较大的指令集拆分为可复用文件，并为 Copilot 提供代码示例。

> [!NOTE]
> `copilot-instructions.md` 中的 **Code formatting guidance** 部分记录了项目编码规范，但目前尚未要求在代码中添加文档。接下来将添加 TSDoc 文档注释和文件注释头的规则。

## 更新指令以符合团队规范

现有文件是一个良好开端，但仍有缺漏。修改核心 `copilot-instructions.md` 文件，确保新生成的 TypeScript 代码包含 TSDoc 注释。

1. 在 `.github/copilot-instructions.md` 中找到 **Code formatting guidance** 部分。
2. 在该部分末尾添加以下项目：

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

文件会自动保存。

## 使用更新后的指导

Copilot CLI 会在对话开始时加载存储库指令。保存指令后，退出并恢复筛选对话，这样 Copilot 就能在保留功能上下文的同时使用新指导。

1. 如果筛选对话仍在运行，输入 `/exit` 退出。Copilot CLI 会自动保存对话。
2. 在存储库根目录的 `game-filters-cli` 分支上，恢复已保存的对话：

   ```bash
   copilot --resume
   ```

   如果系统提示，请选择筛选对话，并确认已检出 `game-filters-cli` 分支。
3. 让 Copilot 应用更新后的指导：

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

4. 输入 `/diff`，查看已更改的 TypeScript 文件。注意新生成的 TSDoc 注释，并确认注释准确说明了代码。

## 总结和后续步骤

你已探索 Copilot 如何从指令文件获取上下文，并将新规范应用于功能。具体来说，你：

- 探索了存储库指令和按路径限定的指令文件如何传递给智能体。
- 更新了指令文件，确保遵循编码规范。
- 观察了指令文件对代码的影响。

接下来，[自定义并运行可复用的 quality-checks 技能][next-lesson]，确保一致地运行 lint 和测试。

## 资源

- [为 Copilot CLI 添加自定义指令][instruction-files]
- [自定义指令支持][custom-instructions-support]
- [创建自定义指令的最佳实践][instructions-best-practices]
- [编写更好的 Copilot 自定义指令的 5 个技巧][copilot-instructions-five-tips]
- [Awesome Copilot：指令文件及其他资源合集][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
