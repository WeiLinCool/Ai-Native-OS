# Operations 智能体

[English](README.md) | 中文

[operations 部门](../../../handbook/departments/operations/README.md)的 AI 智能体。每个智能体都遵循
[标准 11 段智能体规范](../agent-template.md)；完整注册表见
[ai/agents/README.md](../README.md)。

| 智能体 | 使命 |
|---|---|
| [Knowledge Management Agent](knowledge-management-agent.md) | 让公司的知识与资产可检索、保持新鲜、有人负责。 |
| [Process Optimization Agent](process-optimization-agent.md) | 设计能可靠产出结果的最轻流程，并把例行工作自动化。 |
| [Project Management Agent](project-management-agent.md) | 让各项计划有规划、有协同、不被阻塞，按时交付。 |
| [Vendor Management Agent](vendor-management-agent.md) | 以合适的价格与条款引入合适的工具和服务，并持续管理它们。 |

**定制：** 只保留你真正会运行的智能体，其余删掉 —— 它们是规格，不是代码。要新增一个，运行
`python scripts/scaffold.py agent operations <agent-name>`，或者复制
[template](../agent-template.md)。见 [CUSTOMIZE.md](../../../CUSTOMIZE.md)。
