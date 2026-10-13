# 部门

[English](README.md) | 中文

二十本自成一体的运营手册。每个部门都遵循**同一套结构**（标准 18 个文件 + `templates/` `checklists/` `examples/`），因此懂了一个部门就懂了全部 —— 见
[STRUCTURE.md](../../STRUCTURE.md#standard-department-structure)。

每个部门的 AI 智能体位于 [ai/agents/&lt;department&gt;/](../../ai/agents/README.md)。

**定制：** 删除不需要的部门（连同其智能体目录），保留需要的部门，并从
[templates/department-template/](../templates/department-template/) 新增部门。参见
[CUSTOMIZE.md](../../CUSTOMIZE.md)。

## 构建与产品

| 部门 | 负责什么 |
|---|---|
| [engineering/](engineering/README.md) | 可维护、有测试、安全的软件；标准、评审、交付 |
| [product/](product/README.md) | *正确的*产品 —— 发现、PRD、优先级、路线图、PMF |
| [design/](design/README.md) | 可用、无障碍的体验；[设计系统](design/design-system.md) |
| [post-launch/](post-launch/README.md) | 上线后的可靠性 —— 监控、事故、维护、[技术债](post-launch/technical-debt/)、EOL |
| [ai-engineering/](ai-engineering/README.md) | 构建 AI *产品* —— [RAG](ai-engineering/README.md)、[评估](ai-engineering/evaluation-and-testing.md)、[AI 安全](ai-engineering/ai-security.md) |
| [data/](data/README.md) | 数据管道、指标层、分析、治理 |
| [hardware/](hardware/README.md) | 固件、电子、机械、测试 —— 面向实体产品 |

## 发现与决策

| 部门 | 负责什么 |
|---|---|
| [research/](research/README.md) | 下一步该做什么 —— [创意发散](research/ideation.md)、[TRL](research/technology-readiness.md)、[机会评分](research/opportunity-scoring.md) |
| [strategy/](strategy/README.md) | 构建公司 —— [生命周期](strategy/startup-lifecycle.md)、[市场](strategy/market-analysis.md)、[商业模式](strategy/business-model.md)、[单位经济](strategy/unit-economics.md)、[路演](strategy/pitching.md) |

## 走向市场

| 部门 | 负责什么 |
|---|---|
| [marketing/](marketing/README.md) | 定位、内容/SEO、品牌、增长、发布、[心理学](marketing/psychology.md) |
| [sales/](sales/README.md) | 销售 —— [方法论](sales/methodology.md)、[心理学](sales/psychology.md)、[渠道](sales/channels.md) |
| [customer-success/](customer-success/README.md) | 上手、健康度评分、留存、增购 |

## 运营公司

| 部门 | 负责什么 |
|---|---|
| [operations/](operations/README.md) | 节奏、项目管理、流程、供应商与知识管理 |
| [hr/](hr/README.md) | 招聘、入职、绩效、文化 |
| [finance/](finance/README.md) | 预测、预算、会计、计费、现金跑道、成本 |
| [legal/](legal/README.md) | 合同、知识产权、合规、隐私与条款 |
| [security/](security/README.md) | 威胁建模、渗透测试、漏洞管理、合规 |
| [devops/](devops/README.md) | CI/CD、基础设施即代码、发布、可靠性 |
| [documentation/](documentation/README.md) | 产品与 API 文档、知识库、时效性 |
| [investor-relations/](investor-relations/README.md) | 投资人更新、董事会治理、股权结构表 |
