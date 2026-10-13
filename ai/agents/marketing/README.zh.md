# Marketing 智能体

[English](README.md) | 中文

[marketing 部门](../../../handbook/departments/marketing/README.md)的 AI 智能体。每个智能体都遵循
[标准 11 段智能体规范](../agent-template.md)；完整注册表见
[ai/agents/README.md](../README.md)。

| 智能体 | 使命 |
|---|---|
| [Brand & Communications Agent](brand-communications-agent.md) | 让定位保持锋利，让公司的声音在各渠道一致且可信。 |
| [Content Marketing Agent](content-marketing-agent.md) | 打造有机内容引擎，吸引并教育合适的客户。 |
| [Growth Marketing Agent](growth-marketing-agent.md) | 通过有纪律的实验找到并放大高效的获客渠道。 |
| [SEO Agent](seo-agent.md) | 通过技术 SEO 与内容 SEO 带来高质量的自然流量。 |

**定制：** 只保留你真正会运行的智能体，其余删掉 —— 它们是规格，不是代码。要新增一个，运行
`python scripts/scaffold.py agent marketing <agent-name>`，或者复制
[template](../agent-template.md)。见 [CUSTOMIZE.md](../../../CUSTOMIZE.md)。
