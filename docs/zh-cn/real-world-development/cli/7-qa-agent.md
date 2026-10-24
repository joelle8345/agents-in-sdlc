---
title: "第 7 课 - 创建并使用质量保证 (QA) 智能体"
description: "创建质量保证 (QA) 自定义智能体，结合议题要求、quality-checks 技能和 Playwright 模型上下文协议 (MCP)。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

你已使用 `quality-checks` 技能运行自动化检查，也使用 Playwright 模型上下文协议 (MCP) 在浏览器中观察筛选体验。现在，将这些能力整合到自定义智能体中，并为它定义明确的质量保证 (QA) 流程。

在本课中，你将：

- 探索自定义智能体如何使用指令、技能和 MCP 工具。
- 创建并检查可复用的质量保证配置文件。
- 选择 QA 智能体，根据筛选议题审查其发现。

## 场景

Tailspin Toys 希望在创建拉取请求 (PR) 前，一致地检查需求、代码质量、自动化检查、测试覆盖率和浏览器行为。自定义智能体可以协调 QA 流程，并提供可复用报告。

## 什么是自定义智能体？

自定义智能体是通过 Markdown 配置文件定义的 Copilot 专用版本。配置文件描述智能体的用途、指令和可用工具。本工作坊将在 `.github/agents/qa.agent.md` 中定义 QA 角色，并在 Copilot CLI 中选择该角色。

此前使用的自定义项各有不同用途：存储库指令说明团队规范；`quality-checks` 技能打包可重复执行的检查；Playwright MCP 提供浏览器工具；QA 配置文件则告诉 Copilot 如何使用这些能力评估需求并报告发现。它不会取代这些功能，也不需要另开对话。

## 创建 QA 配置文件

创建功能 PR 前，让 Copilot 创建可复用的 QA 配置文件。配置文件会定义 QA 执行的检查以及必须遵守的边界。

1. 返回 Codespace，并确认筛选对话处于 Interactive 模式。
2. 让默认智能体创建新的自定义智能体：

   ```plaintext
   Create a custom agent named QA in .github/agents/qa.agent.md. It should check features against their issues and agreed requirements, follow the repository instructions, run the quality-checks skill, use Playwright MCP to verify behavior, and add tests when coverage is missing.

   Have it report each requirement as pass, fail, or blocked with supporting evidence. It must ask before changing implementation code, and it must not commit changes or open pull requests.

   Just create the profile for now so I can review it.
   ```

## 检查配置文件

使用新智能体前，先检查其配置文件，确认 Copilot 正确记录了预期的 QA 工作流和边界，避免只要求验证时却生成不完整或范围过大的智能体。

1. 输入 `/diff` 并打开 `.github/agents/qa.agent.md`。
2. 阅读 frontmatter。`description` 是必需字段；`name` 为可选字段，但添加后会显示清晰的智能体名称。
3. 阅读配置文件指令，确认 QA 会从需求出发、遵循存储库指令、运行 `quality-checks` 技能并使用 Playwright MCP。
4. 确认 QA 会提供支持证据、在更改实现代码前征求许可，并且不会提交更改或创建拉取请求。
5. 如果生成的配置文件遗漏任何职责或边界，请让默认智能体先修改，再继续操作。

## 根据议题运行 QA

Copilot CLI 会在对话开始时加载项目智能体。创建配置文件后，恢复同一筛选对话，再选择 QA，使其能够使用已有议题和规划决策。

1. 使用以下提示启用智能体：

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> 刚创建的智能体可能尚未显示在可用智能体列表中，但仍可通过上述命令启用。

2. 使用以下提示，让 QA 智能体审查功能：

   ```plaintext
   Review the filtering feature against the issue and the decisions in our plan. Is it ready for a PR?
   ```

3. QA 智能体开始工作。
4. 完成后，阅读它提供的报告。

## 总结和后续步骤

你已将可复用的专家角色加入工作流，并审阅了它的工作。在本课中，你：

- 探索了自定义智能体如何使用指令、技能和 MCP 工具。
- 创建并检查了可复用的质量保证配置文件。
- 选择了 QA 智能体，并根据筛选议题审查其发现。

现在，已有实现、技能更新、QA 配置文件、测试和验证报告，可以开始审查。接下来，将它们[汇总到功能 PR 中并使用 Agent Merge][next-lesson]。

## 资源

- [为 Copilot CLI 创建自定义智能体][create-agents]
- [自定义智能体配置][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
