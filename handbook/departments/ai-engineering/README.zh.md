# AI 工程

[English](README.md) | 中文

AI 被视为一门工程学科，而不是写提示词。该部门负责构建可靠智能系统所需的标准、评估与安全。多智能体编排与记忆位于 [orchestration/](../../../ai/orchestration/) 和 [memory/](../../../ai/memory/)；本部门覆盖 AI 特有的工程实践。它向 [CTO](../../company/roles.md) 汇报，并由 [Chief Scientist](../../company/roles.md) 提供科学验证。

## 索引

| 文件 | 用途 |
|---|---|
| [mission.md](mission.md) | 该部门为何存在 |
| [vision.md](vision.md) | 它将走向何方 |
| [principles.md](principles.md) | 不可妥协的运营原则 |
| [organization.md](organization.md) | 结构、汇报线与接口 |
| [roles.md](roles.md) | 人类与 AI 角色及职责 |
| [agents.md](agents.md) | 在此运作的 AI 智能体 |
| [workflows.md](workflows.md) | 核心可重复流程 |
| [playbooks.md](playbooks.md) | 情境化的分步指南 |
| [sops.md](sops.md) | 标准作业程序 |
| [decision-frameworks.md](decision-frameworks.md) | 决策如何做出 |
| [standards.md](standards.md) | 部门专属标准 |
| [review-process.md](review-process.md) | 工作如何被评审 |
| [quality-gates.md](quality-gates.md) | 工作推进前必须通过什么 |
| [automation.md](automation.md) | 哪些环节已自动化 |
| [metrics.md](metrics.md) | 衡量什么 |
| [dashboards.md](dashboards.md) | 指标如何呈现 |
| [tools.md](tools.md) | 使用的工具 |


### 领域深入阅读
- [design-principles.md](design-principles.md) - 任何 AI 系统必备的八项要素
- [prompt-engineering.md](prompt-engineering.md) - 提示词标准与版本管理
- [evaluation-and-testing.md](evaluation-and-testing.md) - 如何验证模型
- [ai-security.md](ai-security.md) - 威胁与防御
- [技术成熟度（TRL）](../research/technology-readiness.md) - 新型模型从实验室走向生产的成熟度

## 接口

AI 把模型、提示词和评估交给 [工程](../engineering/README.md) 集成；grounding 数据来自 [数据](../data/README.md) 和[知识库](../../../ai/memory/knowledge-base.md)；安全发现提交给 [安全](../security/README.md)；漂移由 [上线后](../post-launch/README.md) 监控。
