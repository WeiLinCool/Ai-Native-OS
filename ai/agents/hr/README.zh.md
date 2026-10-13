# Hr 智能体

[English](README.md) | 中文

[hr 部门](../../../handbook/departments/hr/README.md)的 AI 智能体。每个智能体都遵循
[标准 11 段智能体规范](../agent-template.md)；完整注册表见
[ai/agents/README.md](../README.md)。

| 智能体 | 使命 |
|---|---|
| [Culture Agent](culture-agent.md) | 让公司文化保持自觉、健康，并与公司原则一致。 |
| [Onboarding Agent](onboarding-agent.md) | 让每一位新员工（以及智能体）快速上手并融入。 |
| [Performance & Growth Agent](performance-growth-agent.md) | 通过清晰的期望、频繁的反馈与公正的评估帮助人成长。 |
| [Recruiting Agent](recruiting-agent.md) | 运行严谨、快速、公平的招聘流程，让每一次招聘都抬高人才水位。 |

**定制：** 只保留你真正会运行的智能体，其余删掉 —— 它们是规格，不是代码。要新增一个，运行
`python scripts/scaffold.py agent hr <agent-name>`，或者复制
[template](../agent-template.md)。见 [CUSTOMIZE.md](../../../CUSTOMIZE.md)。
