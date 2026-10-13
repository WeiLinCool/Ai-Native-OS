# Investor Relations 智能体

[English](README.md) | 中文

[investor-relations 部门](../../../handbook/departments/investor-relations/README.md)的 AI 智能体。每个智能体都遵循
[标准 11 段智能体规范](../agent-template.md)；完整注册表见
[ai/agents/README.md](../README.md)。

| 智能体 | 使命 |
|---|---|
| [Board Governance Agent](board-governance-agent.md) | 运行干净的董事会流程 —— 会议准备充分、纪要准确、决议合规。 |
| [Cap Table Agent](cap-table-agent.md) | 保持股权记录准确，并测算融资与股权事件的影响。 |
| [Investor Reporting Agent](investor-reporting-agent.md) | 产出准确、口径一致的投资者更新，并与财务数据对账。 |

**定制：** 只保留你真正会运行的智能体，其余删掉 —— 它们是规格，不是代码。要新增一个，运行
`python scripts/scaffold.py agent investor-relations <agent-name>`，或者复制
[template](../agent-template.md)。见 [CUSTOMIZE.md](../../../CUSTOMIZE.md)。
