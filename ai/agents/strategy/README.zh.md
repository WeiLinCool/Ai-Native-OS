# Strategy 智能体

[English](README.md) | 中文

[strategy 部门](../../../handbook/departments/strategy/README.md)的 AI 智能体。每个智能体都遵循
[标准 11 段智能体规范](../agent-template.md)；完整注册表见
[ai/agents/README.md](../README.md)。

| 智能体 | 使命 |
|---|---|
| [Business Model & Pricing Agent](business-model-pricing-agent.md) | 设计公司如何创造与获取价值，并给出站得住脚的定价。 |
| [Business Strategy Agent](business-strategy-agent.md) | 为公司战略举措提供建议 —— 做什么、何时做、为何可防御。 |
| [Fundraising Agent](fundraising-agent.md) | 让公司准备好以最优条款融资 —— 或者规划一条不融资的路径。 |
| [Go-To-Market Agent](go-to-market-agent.md) | 明确产品如何触达并赢得它的市场。 |

**定制：** 只保留你真正会运行的智能体，其余删掉 —— 它们是规格，不是代码。要新增一个，运行
`python scripts/scaffold.py agent strategy <agent-name>`，或者复制
[template](../agent-template.md)。见 [CUSTOMIZE.md](../../../CUSTOMIZE.md)。
