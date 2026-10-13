# Finance 智能体

[English](README.md) | 中文

[finance 部门](../../../handbook/departments/finance/README.md)的 AI 智能体。每个智能体都遵循
[标准 11 段智能体规范](../agent-template.md)；完整注册表见
[ai/agents/README.md](../README.md)。

| 智能体 | 使命 |
|---|---|
| [Accounting Agent](accounting-agent.md) | 让账目准确、及时、随时可审计。 |
| [Cost Optimization Agent](cost-optimization-agent.md) | 确保公司每一分支出都物有所值，尤其是基础设施与 AI 方面。 |
| [Financial Planning Agent](financial-planning-agent.md) | 维护预测、预算与现金跑道，让管理层始终看清财务状况。 |
| [Revenue & Billing Agent](revenue-billing-agent.md) | 正确开票、可靠回款、合规确认收入。 |

**定制：** 只保留你真正会运行的智能体，其余删掉 —— 它们是规格，不是代码。要新增一个，运行
`python scripts/scaffold.py agent finance <agent-name>`，或者复制
[template](../agent-template.md)。见 [CUSTOMIZE.md](../../../CUSTOMIZE.md)。
