# Devops 智能体

[English](README.md) | 中文

[devops 部门](../../../handbook/departments/devops/README.md)的 AI 智能体。每个智能体都遵循
[标准 11 段智能体规范](../agent-template.md)；完整注册表见
[ai/agents/README.md](../README.md)。

| 智能体 | 使命 |
|---|---|
| [CI/CD Engineer Agent](cicd-engineer-agent.md) | 构建并维护从提交到生产的自动化流水线。 |
| [Platform Engineer Agent](platform-engineer-agent.md) | 以基础设施即代码的方式提供并管理可复现的环境。 |
| [Release Engineer Agent](release-engineer-agent.md) | 编排安全、渐进的发布以及干净的回滚。 |
| [Site Reliability Agent](site-reliability-agent.md) | 让生产环境在 SLO 与错误预算内保持可靠。 |

**定制：** 只保留你真正会运行的智能体，其余删掉 —— 它们是规格，不是代码。要新增一个，运行
`python scripts/scaffold.py agent devops <agent-name>`，或者复制
[template](../agent-template.md)。见 [CUSTOMIZE.md](../../../CUSTOMIZE.md)。
