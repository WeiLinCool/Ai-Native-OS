# Customer Success 智能体

[English](README.md) | 中文

[customer-success 部门](../../../handbook/departments/customer-success/README.md)的 AI 智能体。每个智能体都遵循
[标准 11 段智能体规范](../agent-template.md)；完整注册表见
[ai/agents/README.md](../README.md)。

| 智能体 | 使命 |
|---|---|
| [Customer Health Agent](customer-health-agent.md) | 为账户健康度打分，并尽早预测流失以提前干预。 |
| [Customer Onboarding Agent](customer-onboarding-agent.md) | 让每一位新客户尽快到达首次价值时刻。 |
| [Renewal & Expansion Agent](renewal-expansion-agent.md) | 以已交付的价值赢得续约，并在有更多价值空间的地方推动账户增长。 |
| [Support Agent](support-agent.md) | 快速、准确地解决客户问题，并把它们转化为产品信号。 |

**定制：** 只保留你真正会运行的智能体，其余删掉 —— 它们是规格，不是代码。要新增一个，运行
`python scripts/scaffold.py agent customer-success <agent-name>`，或者复制
[template](../agent-template.md)。见 [CUSTOMIZE.md](../../../CUSTOMIZE.md)。
