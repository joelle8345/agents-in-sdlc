---
title: "第 6 课 - 使用 Playwright MCP 验证功能"
description: "在 Copilot CLI 中检查或配置 Playwright MCP，并在浏览器中体验筛选功能。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

前面提到过，编写代码不只是把代码写出来。我们还要处理数据、外部服务，并让 Copilot 使用更多自动化工具。这时就需要模型上下文协议 (MCP) 服务器。MCP 服务器让 Copilot 能使用 CLI 内置功能之外的工具和服务。

在本课中，你将：

- 了解模型上下文协议 (MCP) 以及 Copilot CLI 如何使用它。
- 如果尚未配置 Playwright MCP 服务器，则添加该服务器。
- 让智能体操作浏览器并体验筛选功能。

## 场景

单元测试和端到端测试固然重要，但验证用户界面 (UI) 更新还需要实际与之交互。你希望 Copilot 能像用户一样使用正在开发的网站，进一步自动化更改验证，并提升对更新符合预期的信心。

## 什么是模型上下文协议 (MCP)？

[模型上下文协议 (MCP)][mcp-blog-post]为人工智能 (AI) 智能体提供了与外部工具和服务通信的方式。借助 MCP，AI 智能体可以实时访问最新信息，并代表你执行操作。

这些工具和资源通过 MCP 服务器访问。MCP 服务器充当 AI 智能体与外部工具和服务之间的桥梁。每个 MCP 服务器都提供一组 AI 智能体可访问的工具和资源。

以下是一些常用 MCP 服务器：

- **[GitHub MCP Server][github-mcp]**：提供管理 GitHub 存储库、议题和拉取请求的 API。
- **[Playwright MCP Server][playwright-mcp-server]**：使用 Playwright 提供浏览器自动化功能。

还有许多其他 MCP 服务器。GitHub 提供 [MCP 注册表][mcp-registry]，方便发现和参与生态系统。

> [!CAUTION]
> 请像对待项目中的其他依赖项一样对待 MCP 服务器。使用前请审查其源代码、验证发布者，并考虑安全影响。

## 添加 Playwright MCP 服务器

如果 Copilot CLI 中尚无 Playwright MCP 服务器，请添加它，以便 Copilot 像用户一样与网站交互。

> [!NOTE]
> 如果 Copilot CLI 已配置 Playwright MCP，请跳过以下设置步骤，继续下一节。

1. 返回 Codespace。
2. 在 Copilot CLI 中输入以下命令，打开添加 MCP 服务器对话框：

   ```plaintext
   /mcp add
   ```

3. 名称输入 `playwright`，然后按 <kbd>Tab</kbd>。
4. 按 <kbd>Enter</kbd> 确认服务器类型为 **STDIO**，然后按 <kbd>Tab</kbd>。
5. 在 **Command** 对话框中粘贴：

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

6. 按 <kbd>Control</kbd>+<kbd>S</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>S</kbd>（Windows/Linux）保存新 MCP 服务器。
7. 按 <kbd>Esc</kbd> 退出 MCP 对话框。

## 让 Copilot 通过 Playwright 体验功能

之前你已手动确认功能符合预期。现在使用 Copilot 可访问的 Playwright MCP 服务器执行相同检查。

1. 使用以下提示，让 Copilot 使用 Playwright MCP 服务器验证功能：

   ```plaintext
   Start the app and use Playwright MCP to check filtering against the issue and our plan. Tell me what works and what doesn't, without making changes. Stop the server you started when you're done.
   ```

> [!NOTE]
> 通常无需明确告诉 Copilot 使用 MCP 服务器，它一般会自行判断。不过，明确指定目标工具有助于提高结果一致性，也可以节省一些令牌。

2. 观察 Copilot 列出在浏览器中确认功能是否正常的各个步骤。
3. 阅读报告，确认行为符合预期。

Copilot 会启动服务器、使用 Playwright 与网站交互、停止服务器，并向你汇报结果。

## 总结和后续步骤

恭喜！你已使用 Playwright MCP 服务器，让 Copilot CLI 在真实浏览器中体验功能。回顾一下，你：

- 了解了模型上下文协议 (MCP) 以及 Copilot CLI 如何使用它。
- 如果 Playwright MCP 服务器尚未配置，则添加了它。
- 让智能体操作浏览器并体验筛选功能。

接下来，你将[创建 QA 自定义智能体][next-lesson]，将技能和浏览器工具结合到专门的角色中。

## 资源

- [MCP 到底是什么，为什么大家都在谈论它？][mcp-blog-post]
- [Microsoft Playwright MCP Server][playwright-mcp-server]
- [为 Copilot CLI 添加 MCP 服务器][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
