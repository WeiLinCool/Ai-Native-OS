# Design 智能体

[English](README.md) | 中文

[design 部门](../../../handbook/departments/design/README.md)的 AI 智能体。每个智能体都遵循
[标准 11 段智能体规范](../agent-template.md)；完整注册表见
[ai/agents/README.md](../README.md)。

| 智能体 | 使命 |
|---|---|
| [Accessibility Agent](accessibility-agent.md) | 对照 WCAG 审计每一个界面，并推动整改直至通过。 |
| [Design System Agent](design-system-agent.md) | 维护设计系统的组件、token 与无障碍能力，使其成为唯一事实来源。 |
| [Interaction Designer Agent](interaction-designer-agent.md) | 设计流程、状态、反馈与动效，让每一次交互都清晰且容错。 |
| [UI Designer Agent](ui-designer-agent.md) | 依据需求产出符合无障碍要求、贴合设计系统的视觉设计。 |
| [UX Research Agent](ux-research-agent.md) | 研究用户，把行为、需求与痛点呈现为设计决策的证据。 |

**定制：** 只保留你真正会运行的智能体，其余删掉 —— 它们是规格，不是代码。要新增一个，运行
`python scripts/scaffold.py agent design <agent-name>`，或者复制
[template](../agent-template.md)。见 [CUSTOMIZE.md](../../../CUSTOMIZE.md)。
