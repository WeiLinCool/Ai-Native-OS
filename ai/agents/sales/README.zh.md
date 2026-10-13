# Sales 智能体

[English](README.md) | 中文

[sales 部门](../../../handbook/departments/sales/README.md)的 AI 智能体。每个智能体都遵循
[标准 11 段智能体规范](../agent-template.md)；完整注册表见
[ai/agents/README.md](../README.md)。

| 智能体 | 使命 |
|---|---|
| [Account Executive Agent](account-executive-agent.md) | 以诚实的、发现驱动的销售流程，从锁定机会走到成交。 |
| [Deal Desk Agent](deal-desk-agent.md) | 让各笔交易的定价、条款与预测保持一致、干净。 |
| [Prospecting Agent](prospecting-agent.md) | 识别并甄别最有可能高度契合的客户账户。 |
| [Sales Engineer Agent](sales-engineer-agent.md) | 诚实地证明技术契合度，让对的交易向前推进，错的不必拖到后期才卡住。 |

**定制：** 只保留你真正会运行的智能体，其余删掉 —— 它们是规格，不是代码。要新增一个，运行
`python scripts/scaffold.py agent sales <agent-name>`，或者复制
[template](../agent-template.md)。见 [CUSTOMIZE.md](../../../CUSTOMIZE.md)。
