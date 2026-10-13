# Documentation 智能体

[English](README.md) | 中文

[documentation 部门](../../../handbook/departments/documentation/README.md)的 AI 智能体。每个智能体都遵循
[标准 11 段智能体规范](../agent-template.md)；完整注册表见
[ai/agents/README.md](../README.md)。

| 智能体 | 使命 |
|---|---|
| [API Documentation Agent](api-documentation-agent.md) | 让 API 参考文档完整、准确、示例丰富 —— 且从唯一事实来源生成。 |
| [Knowledge Base Agent](knowledge-base-agent.md) | 让内部知识 —— 运维手册、流程、入职材料 —— 可检索、有人负责、保持新鲜。 |
| [Technical Writer Agent](technical-writer-agent.md) | 为每一项产品能力产出清晰、准确、面向任务的文档。 |

**定制：** 只保留你真正会运行的智能体，其余删掉 —— 它们是规格，不是代码。要新增一个，运行
`python scripts/scaffold.py agent documentation <agent-name>`，或者复制
[template](../agent-template.md)。见 [CUSTOMIZE.md](../../../CUSTOMIZE.md)。
