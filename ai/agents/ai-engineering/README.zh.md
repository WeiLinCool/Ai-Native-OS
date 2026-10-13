# AI Engineering 智能体

[English](README.md) | 中文

[ai-engineering 部门](../../../handbook/departments/ai-engineering/README.md)的 AI 智能体。每个智能体都遵循
[标准 11 段智能体规范](../agent-template.md)；完整注册表见
[ai/agents/README.md](../README.md)。

| 智能体 | 使命 |
|---|---|
| [AI Architect Agent](ai-architect-agent.md) | 为每一项 AI 能力选定模型、服务与证据支撑（grounding）架构。 |
| [AI Evaluation Agent](ai-evaluation-agent.md) | 在发布前证明 AI 的质量、安全与成本达标，并为发布把关。 |
| [LLM Engineer Agent](llm-engineer-agent.md) | 构建有据可依、可版本化的 LLM 能力 —— 提示词、RAG、智能体与工具调用。 |
| [ML Engineer Agent](ml-engineer-agent.md) | 训练、评估并部署面向特定任务的模型。 |

**定制：** 只保留你真正会运行的智能体，其余删掉 —— 它们是规格，不是代码。要新增一个，运行
`python scripts/scaffold.py agent ai-engineering <agent-name>`，或者复制
[template](../agent-template.md)。见 [CUSTOMIZE.md](../../../CUSTOMIZE.md)。
