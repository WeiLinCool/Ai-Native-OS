# Engineering 智能体

[English](README.md) | 中文

[engineering 部门](../../../handbook/departments/engineering/README.md)的 AI 智能体。每个智能体都遵循
[标准 11 段智能体规范](../agent-template.md)；完整注册表见
[ai/agents/README.md](../README.md)。

| 智能体 | 使命 |
|---|---|
| [API 架构师](api-architect.md) | 设计清晰、一致、可版本化且文档完善的 API。 |
| [后端工程师](backend-engineer.md) | 在既定架构内构建可靠、安全的服务端服务与数据访问层。 |
| [云工程师](cloud-engineer.md) | 设计并运营公司赖以运行的云基础设施。 |
| [数据库工程师](database-engineer.md) | 设计、运维并优化支撑产品的数据存储。 |
| [前端工程师](frontend-engineer.md) | 构建快速、无障碍、易维护的 Web 界面。 |
| [移动端工程师](mobile-engineer.md) | 构建可靠、高性能、体验出色的移动应用。 |
| [性能工程师](performance-engineer.md) | 度量并优化系统性能，让产品在负载下依然流畅。 |
| [QA 工程师](qa-engineer.md) | 通过系统化的测试与质量把关防止缺陷流出。 |
| [重构工程师](refactoring-agent.md) | 在不改变外部行为的前提下持续改善内部结构。 |
| [软件架构师](software-architect.md) | 定义并守护系统架构，让它在演进中保持可维护。 |

**定制：** 只保留你真正会运行的智能体，其余删掉 —— 它们是规格，不是代码。要新增一个，运行
`python scripts/scaffold.py agent engineering <agent-name>`，或者复制
[template](../agent-template.md)。见 [CUSTOMIZE.md](../../../CUSTOMIZE.md)。
