# Post Launch 智能体

[English](README.md) | 中文

[post-launch 部门](../../../handbook/departments/post-launch/README.md)的 AI 智能体。每个智能体都遵循
[标准 11 段智能体规范](../agent-template.md)；完整注册表见
[ai/agents/README.md](../README.md)。

| 智能体 | 使命 |
|---|---|
| [API 兼容性工程师](api-compatibility-agent.md) | 守护 API 兼容性，让升级不会打断客户。 |
| [缺陷分类工程师](bug-triage-agent.md) | 快速、准确地对每一个新报的缺陷分类并派发。 |
| [数据库维护工程师](database-maintenance-agent.md) | 让数据库保持健康、有备份、性能良好。 |
| [依赖更新工程师](dependency-update-agent.md) | 让依赖保持更新且安全，不引入回归。 |
| [文档维护工程师](documentation-maintenance-agent.md) | 让文档随产品变化保持准确、完整。 |
| [基础设施健康工程师](infrastructure-health-agent.md) | 持续监控基础设施，及早发现并处理劣化。 |
| [维护经理](maintenance-manager.md) | 统筹上线后的维护工作，为可靠性排定优先级。 |
| [性能监控工程师](performance-monitoring-agent.md) | 持续观测性能，在用户察觉前发现退化。 |
| [回归工程师](regression-agent.md) | 在上线前捕捉回归，守住既有行为。 |
| [安全补丁工程师](security-patch-agent.md) | 及时给已知漏洞打补丁，缩短暴露窗口。 |
| [技术债工程师](technical-debt-agent.md) | 识别、排序并偿还技术债，让交付速度可持续。 |

**定制：** 只保留你真正会运行的智能体，其余删掉 —— 它们是规格，不是代码。要新增一个，运行
`python scripts/scaffold.py agent post-launch <agent-name>`，或者复制
[template](../agent-template.md)。见 [CUSTOMIZE.md](../../../CUSTOMIZE.md)。
