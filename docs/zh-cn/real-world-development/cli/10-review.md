---
title: "第 10 课 - 总结与后续步骤"
description: "回顾 Copilot CLI 工作流程、两个拉取请求、可复用的自定义项和更多资源。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

你在 Tailspin Toys 的连续工作流程中使用了 GitHub Copilot CLI。你完成了以下工作：

- 准备 Codespace、安装 Copilot CLI、探索项目并找到预先创建的筛选议题。
- 添加星级评分，在转发的浏览器中检查结果，并手动合并了第一个拉取请求 (PR)。
- 从筛选议题开始，在 Plan 模式下确定方案，在 Autopilot 模式下构建，并在 Interactive 模式下审查。
- 使用自定义指令引导代理，然后自定义现有的 `quality-checks` 技能，并使用它运行单元测试、lint 和类型检查。
- 添加 Playwright 模型上下文协议 (MCP) 服务器，并使用它在真实浏览器中探索筛选功能。
- 创建并选择质量保证 (QA) 自定义代理，以评估需求、覆盖率、技能结果和浏览器证据。
- 审查完整的筛选更改，并授权 Agent Merge 合并筛选 PR。
- 探索用于管理上下文、选择模型、共享会话以及可选委托给云代理的斜杠命令。

## 交付成果

本研讨课包含两个 PR 里程碑，每个里程碑都在从更新后的 `main` 创建的独立分支上完成：

1. **星级评分：** 在游戏卡片上显示现有的 `starRating` 和明确的未评分状态。
2. **筛选与质量工作流程：** 实现筛选，更新指令并将其应用于该功能，自定义 `quality-checks` 报告，创建 QA 配置，并加入相关测试。

从规划筛选功能到创建 PR，你始终使用同一会话和分支。为了简化研讨课，我们将这部分工作合并到一个 PR 中。

## 多种验证方式

你通过多种方式检查代码：自动化测试、亲自检查浏览器，以及 Copilot 通过 MCP 探索真实浏览器。`quality-checks` 技能运行单元测试、lint 和类型检查，并以新格式报告结果。创建 PR 前，QA 将这些结果与需求和测试覆盖率审查结合起来。

添加的测试应弥补真实的覆盖缺口；QA 运行不需要添加新测试也可能是正确的。授权合并前应审查代码和证据，并在更改后更新受影响的证据。

## 最佳实践

提供给 Copilot 的上下文和工具会影响它的工作。在本研讨课中，你更新了指令、自定义了技能、创建了 QA 配置并配置了 MCP 服务器。跨会话复用这些自定义项，并根据团队需求调整。指令设定标准，技能描述可重复的任务，自定义代理定义专业角色，MCP 服务器连接外部工具。应审查实际更改和工具结果，而不只是代理的总结。

根据任务选择合适的**模式和模型**。在构建前梳理方案时使用 **Plan**，处理范围明确的更改并保持参与时使用 **Interactive**，仅对范围清晰的任务使用 **Autopilot**。日常编辑选择速度更快的模型，复杂工作选择推理能力更强的模型。

上下文与基础设施同样重要。清楚描述想构建*什么*、*为什么*以及*如何构建*，会显著影响结果。

## 继续探索

你已经完成核心工作流程。还可以了解 Copilot CLI 的其他功能：

- 使用 `/review` 请求代码审查代理分析更改。
- 使用 `/rubber-duck` 讨论问题并获得另一种观点。
- 使用 `/fleet` 并行协调独立的子任务。
- 使用 `/worktree` 隔离单独的任务。
- 使用 `/delegate` 将任务发送给 Copilot 云代理。

## 后续步骤

提升任何工具使用能力的最佳方式就是持续使用它。将它用于生产代码、个人项目，或那个构思多年却一直没动手的小应用。与团队分享所学，也向团队学习。一如既往，继续查阅文档。

若要从终端扩展 Tailspin Toys，请继续学习可选的 [Foundry Backer Concierge 系列][foundry]。若要比较其他环境，请参阅 [VS Code 研讨课][vscode]、[GitHub Copilot 应用研讨课][app]或 [Copilot 云代理研讨课][cloud]。

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
