---
title: "第 10 课 - 回顾和后续步骤"
description: "回顾 Copilot CLI 工作流、两个拉取请求、可复用自定义项和更多资源。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

你已在 Tailspin Toys 的连续工作流中使用 GitHub Copilot CLI。你：

- 准备了 Codespace、安装了 Copilot CLI、探索了项目，并找到了已创建的筛选议题。
- 添加了星级评分，在转发的浏览器中审查结果，并手动合并了第一个拉取请求 (PR)。
- 从筛选议题开始，在 Plan 模式下确定方案，在 Autopilot 模式下实现，并在 Interactive 模式下审查。
- 使用自定义指令引导智能体，自定义现有的 `quality-checks` 技能，并运行单元测试、lint 和类型检查。
- 添加了 Playwright 模型上下文协议 (MCP) 服务器，并在真实浏览器中体验筛选功能。
- 创建并选择质量保证 (QA) 自定义智能体，评估需求、覆盖率、技能结果和浏览器证据。
- 审查了完整筛选更改，并授权 Agent Merge 合并筛选 PR。
- 探索了用于管理上下文、模型、共享和可选云端委托的斜杠命令。

## 已交付的成果

工作坊包含两个 PR 阶段，每个阶段都从更新后的 `main` 创建独立分支：

1. **星级评分：**在游戏卡片上显示现有的 `starRating` 和明确的未评分状态。
2. **筛选和质量工作流：**实现筛选、更新指令并将其应用于功能、自定义 `quality-checks` 报告、创建 QA 配置文件，并包含相关测试。

从规划筛选功能到创建 PR，你一直使用同一对话和分支。为简化工作坊流程，我们将这些更改放在一个 PR 中。

## 不同类型的验证

你通过多种方式检查代码：自动化测试、亲自检查浏览器，以及通过 MCP 让 Copilot 探索浏览器。`quality-checks` 技能运行单元测试、lint 和类型检查，并按新的格式报告结果。QA 在 PR 创建前，将这些结果与需求和测试覆盖率审查结合起来。

新增测试应弥补实际缺口；如果 QA 运行后发现无需新增测试，也可能是合理结果。授权合并前，请审查代码和证据，并在更改后更新受影响的证据。

## 最佳实践

提供给 Copilot 的上下文和工具会影响其工作方式。在本工作坊中，你更新了指令、自定义了技能、创建了 QA 配置文件并配置 MCP 服务器。可以在多个对话中复用这些自定义项，并根据团队需求进行调整。指令设定规范，技能描述可重复执行的任务，自定义智能体定义专家角色，MCP 服务器连接外部工具。请审查实际更改和工具结果，而不只是智能体的总结。

根据任务选择合适的**模式和模型**。使用 **Plan** 先思考实现方案，使用 **Interactive** 协作处理重点更改，使用 **Autopilot** 处理范围明确的任务。常规编辑可选择更快的模型，复杂工作则选择能力更强的模型。

上下文和基础设施同样重要。清楚说明要构建**什么**、**为什么**以及**如何**实现，会显著影响结果。

## 继续探索

你已完成核心工作流，还可以了解一些其他 CLI 功能：

- `/review`：让代码审查智能体分析更改。
- `/rubber-duck`：讨论问题并获取另一种视角。
- `/fleet`：并行协调互不依赖的子任务。
- `/worktree`：隔离另一个任务。
- `/delegate`：将任务发送给 Copilot cloud agent。

## 后续步骤

提高工具使用能力的最佳方法就是持续使用。可将它用于生产代码、业余项目，或一直想做却尚未动手的小应用。与团队分享经验，也向团队成员学习。还可以继续探索文档。

如果想从终端扩展 Tailspin Toys，请继续学习可选的 [Foundry Backer Concierge 系列][foundry]。若要比较不同工作环境，请查看 [VS Code 工作坊][vscode]、[GitHub Copilot app 工作坊][app]或 [Copilot cloud agent 工作坊][cloud]。

## 资源

- [关于 GitHub Copilot CLI][about-cli]
- [Copilot CLI 命令参考][cli-reference]
- [自定义 Copilot CLI][customize-cli]
- [使用 Copilot CLI 管理拉取请求][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
