# 高管事业部 —— C-suite

[English](README.md) | 中文

高管层位于人类创始人与二十个专业事业部之间。高管在自己的领域内**设定方向并对质量负责**；他们把实现工作委派出去，从不亲自动手。每一位都是下列部门的问责负责人 —— 这正是专家智能体规格上的“**Reports to:** CTO”具有具体含义的原因。

每份规格都遵循[标准 11 段格式](../agent-template.md)。这些规格实现的高管角色，在面向人类的 [handbook/company/roles.md](../../../handbook/company/roles.md) 中有描述。

## 指挥链

```
Human Founder                      one-way doors, money, legal, people — always human
│
└── AI Co-Founder                  direction & judgment: the thesis, the hard calls, the dissent
    │
    └── CEO Agent (kernel)         orchestration: objective → plan → routed work → review → ship
        │
        ├── Chief of Staff         the decision log and the follow-through
        │
        ├── CTO                    Engineering · DevOps · AI · Hardware · Post-Launch
        ├── CPO                    Product · Documentation
        ├── Chief Designer         Design
        ├── Chief Scientist        Research
        ├── COO                    Operations
        ├── CFO                    Finance · Investor Relations
        ├── CRO                    Sales · Customer Success
        ├── CMO                    Marketing
        ├── CDO                    Data
        ├── CSO                    Security
        ├── CLO                    Legal
        └── CPeO                   HR / People
```

**AI Co-Founder 与 CEO Agent** —— 两者刻意是两份不同的工作。[AI Co-Founder](ai-cofounder-agent.md) 负责*公司是否在做正确的事*：论点、单向门，以及持续针对当前计划提出的反对意见。[CEO Agent](../../orchestration/ceo-agent.md) 是[内核](../../orchestration/README.md) —— 它负责*把已经商定的事做成*：把目标变成计划，把计划变成已路由的工作，把工作变成经过评审、批准并交付的产出。如果只能保留一个，请保留 CEO Agent；当问题变成“我们到底该不该做这件事？”时，你需要的才是 Co-Founder。

## 花名册

| 智能体 | 负责 | 监督 |
|---|---|---|
| [AI Co-Founder](ai-cofounder-agent.md) | 论点 · 战略 · 单向门 · 对事情是否奏效的诚实判断 | 高管团队 |
| [CEO Agent](../../orchestration/ceo-agent.md) ↗ | 编排：目标、优先级、冲突解决、里程碑 | 所有事业部（规格位于[内核](../../orchestration/README.md)） |
| [Chief of Staff](chief-of-staff-agent.md) | 决策日志 · 高管节奏 · 跟进落实 | — |
| [CTO](cto-agent.md) | 架构 · 工程质量 · 可扩展性 · 技术债 | [engineering](../engineering/) · [devops](../devops/) · [ai](../ai-engineering/) · [hardware](../hardware/) · [post-launch](../post-launch/) |
| [CPO](cpo-agent.md) | 路线图 · 需求 · 优先级 · PMF | [product](../product/) · [documentation](../documentation/) |
| [Chief Designer](chief-designer-agent.md) | 设计系统 · 交互 · 无障碍 · 工艺 | [design](../design/) |
| [Chief Scientist](chief-scientist-agent.md) | 研究议程 · 科学验证 · [TRL](../../../handbook/departments/research/technology-readiness.md) · 现有技术 | [research](../research/) |
| [COO](coo-agent.md) | 执行 · 运营节奏 · OKR · 流程 · 供应商 | [operations](../operations/) |
| [CFO](cfo-agent.md) | 模型 · 预测 · 现金跑道 · 预算 · 单位经济 | [finance](../finance/) · [investor-relations](../investor-relations/) |
| [CRO](cro-agent.md) | 销售管道 · 预测 · 留存 · 增购 | [sales](../sales/) · [customer-success](../customer-success/) |
| [CMO](cmo-agent.md) | 定位 · 品牌 · 增长 · 发布 | [marketing](../marketing/) |
| [CDO](chief-data-officer-agent.md) | 指标层 · 分析 · 实验 · 治理 | [data](../data/) |
| [CSO](chief-security-officer-agent.md) | 威胁模型 · 隐私 · 合规 · 事件响应 | [security](../security/) |
| [CLO](chief-legal-officer-agent.md) | 合同 · 知识产权 · 许可 · 条款 | [legal](../legal/) |
| [CPeO](chief-people-officer-agent.md) | 招聘 · 入职 · 绩效 · 文化 · 人与智能体的边界 | [hr](../hr/) |

[strategy](../strategy/) 直接向 [AI Co-Founder](ai-cofounder-agent.md) 汇报 —— Co-Founder 所负责的那份思考，正是由这个事业部完成的。

## 三条硬性红线

多数高管分歧由 [CEO Agent](../../orchestration/ceo-agent.md) 解决。有三条不是，任何智能体都不得推翻它们 —— 只有人类创始人可以，且必须书面说明风险：

1. **[CSO](chief-security-officer-agent.md)** —— 已知可被利用的工作不得上线。
2. **[CLO](chief-legal-officer-agent.md)** —— 违法或无法投保的行动不得推进。
3. **[CFO](cfo-agent.md)** —— 任何智能体都不得动用资金。

## 定制

你几乎肯定不需要十四位高管。一家两人的公司需要 [AI Co-Founder](ai-cofounder-agent.md)、[CEO Agent](../../orchestration/ceo-agent.md)、一位 [CTO](cto-agent.md) 和一位 [CPO](cpo-agent.md) —— 其他角色无论有没有对应的文件，都由创始人承担着。当某个领域已经大到超出创始人的注意力范围时，再增加一位高管；没有启用的规格就删掉。删除一个时，重新指向其下各智能体的 **Reports to:** 行，然后运行 `python scripts/check-links.py`。
