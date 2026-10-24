---
title: "练习 4 - 监控和管理智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

在前几项练习中，你让 Copilot cloud agent 承担了三项不同任务，以改进用户体验并添加功能。虽然云端智能体以异步、自主方式运行，但监控任务也很重要。

可以使用多种工具管理分配给云端智能体的任务，包括 GitHub.com 上的[智能体页面][agents-page]。在这个任务控制中心，可以查看所有拥有未关闭拉取请求 (PR) 的智能体任务，了解已执行的操作，甚至引导正在进行的会话。

在本课中，你将：

- 浏览智能体页面，监控云端智能体任务。
- 引导正在进行的会话，要求添加额外功能。

## 场景

将高对比度模式任务分配给智能体后，团队认为也应该添加浅色模式。既然已经在更新网站样式和添加切换功能，便可以一并实现浅色模式。你将引导智能体同时添加浅色模式和高对比度模式。

## 查看 Copilot cloud agent 任务

查看分配给 Copilot cloud agent 的任务状态。

1. 打开 [Copilot 智能体页面](https://github.com/copilot/agents)。
2. 查看主窗格和左侧窗格中的任务列表。应能看到分配给 Copilot 的任务，包括：
   - 更新代码文档。
   - 生成用于修改游戏的应用程序编程接口 (API)。
   - 为网站添加高对比度模式。
3. 选择一个正在运行的任务，查看 Copilot 已执行的操作，例如：
   - 从存储库检出代码。
   - 创建 Copilot 工作环境。
   - 设置模型上下文协议 (MCP) 服务器。
   - 执行完成所分配任务的各项步骤。

> [!NOTE]
> 具体列出的步骤会根据 Copilot 的工作状态和处理方式而变化。

4. 另请查看右侧显示的拉取请求 (PR) 窗格，其中可以查看 PR 和已更改文件，以便进一步监控。

## 引导云端智能体

查看当前活动任务后，让 Copilot 在实现高对比度模式时也添加浅色模式切换。

1. 选择正在添加高对比度模式的会话。具体标题取决于 Copilot 使用的名称和当前工作状态。

   ![任务控制中心中的无障碍会话](../../../_images/ex6-accessibility-session.png)

2. 观察会话几分钟，直到状态显示设置已完成并开始执行任务。看到类似下方的消息时，表示已进入此阶段。
3. 在 **Steer active session while Copilot is working** 对话框中输入以下提示：

   ```plaintext
   While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
   ```

   ![智能体页面上的云端智能体任务，其中突出显示了 steer active session while copilot is working 对话框](../../../_images/ex6-steer-cloud-agent-task.png)

4. 按 <kbd>Enter</kbd> 发送提示。
5. 注意 Copilot 会确认收到提示，并将其纳入工作流程。

## 让 Copilot 继续工作

和之前一样，Copilot 会继续处理更新后的任务。它会先完成收到消息时正在执行的步骤，然后将新请求纳入工作流程。

这同样需要几分钟，可以趁此暂停并回顾目前学到和探索的内容。

## 总结和后续步骤

本课介绍了 Copilot 智能体页面，它是监控和引导 GitHub Copilot cloud agent 任务的中心。通过此任务控制中心，可以跟踪所有活动任务和已完成任务、审查正在执行的工作，并重定向进行中的任务以调整范围或提供额外指导。

本课探索了以下内容：

- 使用任务控制中心和智能体页面监控云端智能体任务。
- 重定向正在进行的会话，要求添加额外功能。

Copilot 正在完成无障碍功能。接下来，[迭代改进 Copilot 创建的拉取请求][next-lesson]。

## 资源

- [Copilot 智能体页面][agents-page]
- [关于自定义智能体][custom-agents]

---

| [← 上一课：自定义智能体][previous-lesson] | [下一课：迭代改进 Copilot 的工作 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
