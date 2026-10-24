---
slug: zh-cn/real-world-development/cloud
title: "GitHub Copilot cloud agent"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

**[GitHub Copilot cloud agent](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent)** 让 GitHub Copilot 能在云端异步工作。你在 GitHub 上分配任务后，云端智能体会在后台接手任务、探索存储库、进行更改并创建拉取请求，让你可以处理其他工作。

在这些练习中，你将添加云端智能体要遵循的自定义指令，然后分配 GitHub 议题并让它实现工作。你还将审查并使用自定义智能体来引导其工作方式，在智能体仪表板中监控并引导会话，最后审查它创建的拉取请求并迭代改进结果。

## 练习

| 练习 | 主题 | 说明 |
|----------|-------|-------------|
| [0. 先决条件][ex0] | 设置 | 创建存储库和 codespace |
| [1. 自定义指令][ex1] | 上下文 | 添加云端智能体将遵循的自定义指令 |
| [2. Cloud Agent][ex2] | 异步智能体 | 将议题分配给 Copilot cloud agent |
| [3. 自定义智能体][ex3] | 专用智能体 | 审查并使用自定义智能体 |
| [4. 管理智能体][ex4] | 监控 | 监控并引导智能体会话 |
| [5. 迭代][ex5] | 审查 | 审查拉取请求 (PR)、迭代改进 Copilot 的工作并选择后续步骤 |

## 先决条件

参加本工作坊前，请确保具备以下条件：

- [ ] 拥有 GitHub 账户，并启用了 **Copilot Student、Pro、Pro+、Business 或 Enterprise** 计划
- [ ] 账户或组织已启用 Copilot cloud agent

> [!TIP]
> 没有付费计划？已验证学生可通过 [GitHub Education][callout-student-plan-education] 免费使用 GitHub Copilot。**Copilot Student** 计划包含本工作坊所用的智能体、模型上下文协议 (MCP)、代码审查和 Copilot CLI 功能，因此可用于完成所有工作环境的练习。

[callout-student-plan-education]: https://github.com/education/students

> [!NOTE]
> Copilot Student、Pro、Pro+、Business 和 Enterprise 计划均提供 cloud agent，只有 Copilot Free 除外。Copilot Business 或 Enterprise 计划需要管理员为组织启用此功能。

> [!NOTE]
> 本工作环境不涉及 MCP。若要探索如何将 MCP 服务器与 Copilot 配合使用，请查看 [CLI 工作环境][cli-harness]或 [VS Code 工作环境][vscode-harness]。

## 开始

**[从练习 0：先决条件开始 →][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-custom-instructions/
[ex2]: 2-cloud-agent/
[ex3]: 3-custom-agents/
[ex4]: 4-managing-agents/
[ex5]: 5-iterating/
[cli-harness]: ../cli/
[vscode-harness]: ../vscode/
