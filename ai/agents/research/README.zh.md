# Research 智能体

[English](README.md) | 中文

[research 部门](../../../handbook/departments/research/README.md)的 AI 智能体。每个智能体都遵循
[标准 11 段智能体规范](../agent-template.md)；完整注册表见
[ai/agents/README.md](../README.md)。

| 智能体 | 使命 |
|---|---|
| [Competitor Analysis Agent](competitor-analysis-agent.md) | 绘制竞争格局，找到可防御的定位空档。 |
| [Market Research Agent](market-research-agent.md) | 为一个已验证的问题测算市场规模并量化需求。 |
| [Opportunity Ranking Agent](opportunity-ranking-agent.md) | 为机会打分并排序，让公司优先追逐最高价值的赌注。 |
| [Problem Discovery Agent](problem-discovery-agent.md) | 发现并验证值得为之创办公司的重要且未被充分满足的问题。 |

**定制：** 只保留你真正会运行的智能体，其余删掉 —— 它们是规格，不是代码。要新增一个，运行
`python scripts/scaffold.py agent research <agent-name>`，或者复制
[template](../agent-template.md)。见 [CUSTOMIZE.md](../../../CUSTOMIZE.md)。
