# 起步套件

[English](README.md) | 中文

起步套件是一种**预配置的公司类型**，它继承 AI-Native OS 内核，并叠加领域专属实践。克隆仓库、挑一个
起步套件，你就得到了一套适配你这类公司的操作系统。

## 继承模型

- **继承，而不是复制。** 起步套件引用核心部门、智能体与标准；它只添加**增量** —— 新增的智能体、补充的标准、调整过的工作流，以及上手指引。
- **显式覆盖。** 当起步套件改动核心规则时，它会明确说明并解释原因。
- **同一套约定。** 各套件都遵循 [STRUCTURE.md](../STRUCTURE.md) 和 [CONTRIBUTING.md](../CONTRIBUTING.md)。

## 可用套件

| 起步套件 | 适合的公司 |
|---|---|
| [ai-startup/](ai-startup/) | AI 原生产品公司（范例） |
| [saas/](saas/) | 多租户订阅制软件 |
| [developer-tools/](developer-tools/) | API、SDK、CLI 与开发者平台 |
| [enterprise-b2b/](enterprise-b2b/) | 面向大型组织销售（合规、采购） |
| [marketplace/](marketplace/) | 连接供需的双边平台 |
| [consumer-app/](consumer-app/) | 大规模消费级应用（参与度、增长） |
| [robotics/](robotics/) | 自主实体机器人（硬件 + AI） |
| [drone/](drone/) | 无人机（安全关键、强监管） |
| [embedded/](embedded/) | 资源受限硬件上的固件 |
| [iot/](iot/) | 联网设备集群 + 云端 |
| [research-lab/](research-lab/) | 研究优先、IP 驱动的组织 |
| [fintech/](fintech/) | 资金的转移、存储或借贷（牌照、账本、欺诈） |
| [healthtech/](healthtech/) | 患者护理、临床决策或健康数据 |
| [climate-tech/](climate-tech/) | 能源、材料、碳与脱碳（TRL 门控、MRV） |
| [gaming/](gaming/) | 作为持续运营产品的游戏（乐趣、留存、live-ops） |
| [edtech/](edtech/) | 学习产品（有效性、无障碍、学生数据） |

每个套件都继承 AI-Native OS 的全部内核，只添加自己的领域增量（agents、standards、workflows、
getting-started）。**删掉你不用的套件** —— 见 [CUSTOMIZE.md](../CUSTOMIZE.md)。

## 新增一个起步套件

1. 创建 `starter-kits/<company-type>/`。
2. 写一个 `README.md`，说明它**继承**了什么、**新增/覆盖**了什么。
3. 只添加领域增量（`agents.md`、`standards.md`、`workflows.md`、`getting-started.md`）；其余一切都链接到核心。
