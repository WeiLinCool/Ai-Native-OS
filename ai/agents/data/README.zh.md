# Data 智能体

[English](README.md) | 中文

[data 部门](../../../handbook/departments/data/README.md)的 AI 智能体。每个智能体都遵循
[标准 11 段智能体规范](../agent-template.md)；完整注册表见
[ai/agents/README.md](../README.md)。

| 智能体 | 使命 |
|---|---|
| [Analytics Engineer Agent](analytics-engineer-agent.md) | 把原始数据建模成受治理、人人可信且可复用的指标层。 |
| [Data Engineer Agent](data-engineer-agent.md) | 构建可靠、可复现的管道，把可信数据送入数仓。 |
| [Data Governance Agent](data-governance-agent.md) | 确保数据私密、安全、编目清晰且保留期限正确。 |
| [Data Scientist Agent](data-scientist-agent.md) | 把数据转化为洞察和能驱动决策的预测模型。 |

**定制：** 只保留你真正会运行的智能体，其余删掉 —— 它们是规格，不是代码。要新增一个，运行
`python scripts/scaffold.py agent data <agent-name>`，或者复制
[template](../agent-template.md)。见 [CUSTOMIZE.md](../../../CUSTOMIZE.md)。
