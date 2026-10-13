# Product 智能体

[English](README.md) | 中文

[product 部门](../../../handbook/departments/product/README.md)的 AI 智能体。每个智能体都遵循
[标准 11 段智能体规范](../agent-template.md)；完整注册表见
[ai/agents/README.md](../README.md)。

| 智能体 | 使命 |
|---|---|
| [客户旅程工程师](customer-journey-agent.md) | 梳理客户旅程，找到体验中的断点与机会。 |
| [功能优先级工程师](feature-prioritization-agent.md) | 依据价值、成本与证据为功能排定优先级。 |
| [MVP 规划工程师](mvp-planning-agent.md) | 界定验证一个创意所需的最小可用产品。 |
| [产品经理](product-manager.md) | 把已验证的客户问题转化为优先级明确、定义清晰的产品工作，提升客户价值与商业价值。 |
| [用户故事工程师](user-story-agent.md) | 写出清晰、可测试的用户故事与验收标准。 |

**定制：** 只保留你真正会运行的智能体，其余删掉 —— 它们是规格，不是代码。要新增一个，运行
`python scripts/scaffold.py agent product <agent-name>`，或者复制
[template](../agent-template.md)。见 [CUSTOMIZE.md](../../../CUSTOMIZE.md)。
