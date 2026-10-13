# Legal 智能体

[English](README.md) | 中文

[legal 部门](../../../handbook/departments/legal/README.md)的 AI 智能体。每个智能体都遵循
[标准 11 段智能体规范](../agent-template.md)；完整注册表见
[ai/agents/README.md](../README.md)。

| 智能体 | 使命 |
|---|---|
| [Compliance Agent](compliance-agent.md) | 梳理监管义务，让公司始终站在合规的一侧。 |
| [Contract Agent](contract-agent.md) | 起草与审阅合同并标出风险，让业务能放心签署。 |
| [IP & Patent Agent](ip-patent-agent.md) | 保护公司的知识产权，并确保对他人知识产权使用得当。 |
| [Privacy & Terms Agent](privacy-terms-agent.md) | 让公司条款诚实可信、数据处理尊重用户隐私。 |

**定制：** 只保留你真正会运行的智能体，其余删掉 —— 它们是规格，不是代码。要新增一个，运行
`python scripts/scaffold.py agent legal <agent-name>`，或者复制
[template](../agent-template.md)。见 [CUSTOMIZE.md](../../../CUSTOMIZE.md)。
