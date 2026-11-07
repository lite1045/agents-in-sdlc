---
title: "第 7 课 - 创建并使用质量保证 (QA) 代理"
description: "创建质量保证 (QA) 自定义代理，结合议题要求、quality-checks 技能和 Playwright MCP 进行审查。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

你已使用 `quality-checks` 技能运行自动化检查，并通过 Playwright MCP 在浏览器中观察筛选功能。现在将这些能力整合到一个自定义代理中，并为它定义清晰的 QA 流程。

本课将：

- 了解自定义代理如何结合说明、技能和 MCP 工具。
- 创建并检查可复用的质量保证配置。
- 选择 QA 代理，并让它根据筛选议题审查结果。

## 场景

在创建拉取请求 (PR) 前，Tailspin Toys 希望统一检查需求、代码质量、自动化检查、测试覆盖率和浏览器行为。自定义代理可以协调 QA 流程，并生成可复用的报告。

## 什么是自定义代理？

自定义代理是在 Markdown 配置文件中定义的 Copilot 专用版本。配置文件说明代理的用途、指令和可用工具。在本工作坊中，你将在 `.github/agents/qa.agent.md` 中定义 QA 角色，并在 Copilot CLI 中选择它。

你使用的自定义项各有不同用途：存储库说明描述团队标准；`quality-checks` 技能封装可重复运行的检查；Playwright MCP 提供浏览器工具；QA 配置则指导 Copilot 如何利用这些能力评估需求并报告结果。它不会取代其他自定义项，也不需要另开对话。

## 创建 QA 配置

在打开功能 PR 前，让 Copilot 创建可复用的 QA 配置。配置将明确 QA 执行的检查及其必须遵循的边界。

1. 返回 Codespace，并确认筛选对话处于 Interactive 模式。
2. 让默认代理创建新的自定义代理：

   ```plaintext
   Create a custom agent named QA in .github/agents/qa.agent.md. It should check features against their issues and agreed requirements, follow the repository instructions, run the quality-checks skill, use Playwright MCP to verify behavior, and add tests when coverage is missing.

   Have it report each requirement as pass, fail, or blocked with supporting evidence. It must ask before changing implementation code, and it must not commit changes or open pull requests.

   Just create the profile for now so I can review it.
   ```

## 检查配置文件

使用新代理前，先检查其配置，确认 Copilot 捕捉到了预期的 QA 流程和边界。这样可以避免代理在你只想验证功能时进行不完整或范围过大的更改。

1. 输入 `/diff` 并打开 `.github/agents/qa.agent.md`。
2. 阅读 frontmatter。`description` 为必填项；`name` 是可选项，但添加它能为代理提供清晰的显示名称。
3. 阅读配置说明，确认 QA 会从需求出发、遵循存储库说明、运行 `quality-checks` 技能并使用 Playwright MCP。
4. 确认 QA 会提供支持证据、修改实现代码前会先询问，而且不会提交更改或创建拉取请求。
5. 如果生成的配置缺少任何职责或边界，请让默认代理修改后再继续。

## 根据议题运行 QA

创建配置后，Copilot CLI 会在对话开始时加载项目代理。恢复同一个筛选对话，然后选择 QA，以便它使用已有的议题和计划决策。

1. 使用以下提示启用代理：

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> 由于刚创建代理，它可能暂时不会显示在可用代理列表中。它已经存在，以上命令仍会启用它。

2. 使用以下提示，让 QA 代理审查功能：

   ```plaintext
   Review the filtering feature against the issue and the decisions in our plan. Is it ready for a PR?
   ```

3. QA 代理会开始工作！
4. 完成后阅读它提供的报告。

## 总结和后续步骤

你添加了一个可复用的专用代理，并审查了它的工作。本课中，你：

- 了解了自定义代理如何结合说明、技能和 MCP 工具。
- 创建并检查了可复用的质量保证配置。
- 选择了 QA 代理，并让它根据筛选议题审查结果。

现在，功能实现、技能更新、QA 配置、测试和验证报告都已准备就绪，可以进入审查环节。接下来，[整合这些内容并创建功能 PR，再使用 Agent Merge][next-lesson]。

## 资源

- [为 Copilot CLI 创建自定义代理][create-agents]
- [自定义代理配置][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
