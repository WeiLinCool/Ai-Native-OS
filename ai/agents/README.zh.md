# 智能体 —— AI 组织

[English](README.md) | 中文

每个 AI 智能体都是专家。没有哪个智能体试图包揽所有工作。复杂工作会被分解为专业化任务，并由[编排内核](../orchestration/README.md)协调。每个智能体拥有自己的领域，每个重要决策都需要来自多个视角的评审。

每个智能体都由[标准智能体规格](agent-template.md)定义 —— 11 个部分，没有例外。

## 智能体层级

```
Human Founder
└── AI Co-Founder ─────────────── direction & judgment; the one-way doors
    └── CEO Agent ─────────────── orchestration; delegates, never implements
        ├── Orchestration (the kernel)
        │
        ├── Executive Division ── the C-suite: CTO · CPO · COO · CFO · CMO · CRO
        │                         Chief Designer · Chief Scientist · CDO · CSO · CLO · CPeO
        │                         Chief of Staff
        │
        ├── Research Division ──────── Chief Scientist
        ├── Product Division ───────── CPO
        ├── Documentation Division ─── CPO
        ├── Design Division ────────── Chief Designer
        ├── Engineering Division ───── CTO
        ├── AI Division ────────────── CTO
        ├── Hardware Division ──────── CTO
        ├── DevOps Division ────────── CTO
        ├── Post-Launch Division ───── CTO
        ├── Data Division ──────────── CDO
        ├── Security Division ──────── CSO
        ├── Legal Division ─────────── CLO
        ├── People / HR Division ───── CPeO
        ├── Operations Division ────── COO
        ├── Marketing Division ─────── CMO
        ├── Sales Division ─────────── CRO
        ├── Customer Success ───────── CRO
        ├── Finance Division ───────── CFO
        ├── Investor Relations ─────── CFO
        └── Business / Strategy ────── AI Co-Founder
```

每个事业部由一位[高管](executive/README.md)负责，由其设定方向与质量标准。这正是下面每份专家规格上的 **Reports to:** 一行所指向的对象。

## 注册表

图例：✅ 规格已写好 · 🧭 已规划（从[模板](agent-template.md)撰写）。

### 高管事业部（C-suite）→ [executive/](executive/)
[AI Co-Founder](executive/ai-cofounder-agent.md) ✅ · [Chief of Staff](executive/chief-of-staff-agent.md) ✅ ·
[CTO](executive/cto-agent.md) ✅ · [CPO](executive/cpo-agent.md) ✅ · [COO](executive/coo-agent.md) ✅ ·
[CFO](executive/cfo-agent.md) ✅ · [CRO](executive/cro-agent.md) ✅ · [CMO](executive/cmo-agent.md) ✅ ·
[Chief Designer](executive/chief-designer-agent.md) ✅ · [Chief Scientist](executive/chief-scientist-agent.md) ✅ ·
[Chief Data Officer](executive/chief-data-officer-agent.md) ✅ · [Chief Security Officer](executive/chief-security-officer-agent.md) ✅ ·
[Chief Legal Officer](executive/chief-legal-officer-agent.md) ✅ · [Chief People Officer](executive/chief-people-officer-agent.md) ✅

> **CEO Agent** 也是高管，但它的规格位于[内核](../orchestration/ceo-agent.md)
> —— 编排公司*就是* CEO 的职责，所以这个角色和编排器是同一个智能体。

### 编排（内核）
[CEO Agent](../orchestration/ceo-agent.md) ✅ · [Planner](../orchestration/planner.md) ✅ ·
[Task Decomposer](../orchestration/task-decomposer.md) ✅ · [Coordinator](../orchestration/coordinator.md) ✅ ·
[Memory Manager](../orchestration/memory-manager.md) ✅ · [Knowledge Manager](../orchestration/knowledge-manager.md) ✅ ·
[Reviewer](../orchestration/reviewer.md) ✅ · [QA Reviewer](../orchestration/qa-reviewer.md) ✅ ·
[Security Reviewer](../orchestration/security-reviewer.md) ✅ · [Documentation Reviewer](../orchestration/documentation-reviewer.md) ✅

### 工程事业部 → [engineering/](engineering/)
[Software Architect](engineering/software-architect.md) ✅ · [Backend Engineer](engineering/backend-engineer.md) ✅ ·
[Frontend Engineer](engineering/frontend-engineer.md) ✅ · [Mobile Engineer](engineering/mobile-engineer.md) ✅ ·
[Database Engineer](engineering/database-engineer.md) ✅ · [Cloud Engineer](engineering/cloud-engineer.md) ✅ ·
[API Architect](engineering/api-architect.md) ✅ · [QA Engineer](engineering/qa-engineer.md) ✅ ·
[Performance Engineer](engineering/performance-engineer.md) ✅ · [Refactoring Agent](engineering/refactoring-agent.md) ✅

### 产品事业部 → [product/](product/)
[Product Manager](product/product-manager.md) ✅ · [Feature Prioritization Agent](product/feature-prioritization-agent.md) ✅ ·
[Customer Journey Agent](product/customer-journey-agent.md) ✅ · [User Story Agent](product/user-story-agent.md) ✅ ·
[MVP Planning Agent](product/mvp-planning-agent.md) ✅

### 上线后 / 维护事业部 → [post-launch/](post-launch/)
[Maintenance Manager](post-launch/maintenance-manager.md) ✅ · [Bug Triage Agent](post-launch/bug-triage-agent.md) ✅ ·
[Regression Agent](post-launch/regression-agent.md) ✅ · [Dependency Update Agent](post-launch/dependency-update-agent.md) ✅ ·
[Security Patch Agent](post-launch/security-patch-agent.md) ✅ · [Performance Monitoring Agent](post-launch/performance-monitoring-agent.md) ✅ ·
[Infrastructure Health Agent](post-launch/infrastructure-health-agent.md) ✅ · [Database Maintenance Agent](post-launch/database-maintenance-agent.md) ✅ ·
[API Compatibility Agent](post-launch/api-compatibility-agent.md) ✅ · [Technical Debt Agent](post-launch/technical-debt-agent.md) ✅ ·
[Documentation Maintenance Agent](post-launch/documentation-maintenance-agent.md) ✅

### 研究事业部 → [research/](research/) ✅
[Problem Discovery](research/problem-discovery-agent.md) · [Market Research](research/market-research-agent.md) · [Competitor Analysis](research/competitor-analysis-agent.md) · [Opportunity Ranking](research/opportunity-ranking-agent.md)

### AI 事业部 → [ai/](ai-engineering/) ✅
[AI Architect](ai-engineering/ai-architect-agent.md) · [LLM Engineer](ai-engineering/llm-engineer-agent.md) · [ML Engineer](ai-engineering/ml-engineer-agent.md) · [AI Evaluation](ai-engineering/ai-evaluation-agent.md)

### 设计事业部 → [design/](design/) ✅
[UX Research](design/ux-research-agent.md) · [UI Designer](design/ui-designer-agent.md) · [Interaction Designer](design/interaction-designer-agent.md) · [Design System](design/design-system-agent.md) · [Accessibility](design/accessibility-agent.md)

### 战略 / 业务事业部 → [strategy/](strategy/) ✅
[Business Strategy](strategy/business-strategy-agent.md) · [Business Model & Pricing](strategy/business-model-pricing-agent.md) · [Go-To-Market](strategy/go-to-market-agent.md) · [Fundraising](strategy/fundraising-agent.md)

### 安全事业部 → [security/](security/) ✅
[Security Architect](security/security-architect-agent.md) · [Penetration Testing](security/penetration-testing-agent.md) · [Vulnerability Management](security/vulnerability-management-agent.md) · [Compliance & Privacy](security/compliance-privacy-agent.md)

### DevOps 事业部 → [devops/](devops/) ✅
[CI/CD Engineer](devops/cicd-engineer-agent.md) · [Platform Engineer](devops/platform-engineer-agent.md) · [Site Reliability](devops/site-reliability-agent.md) · [Release Engineer](devops/release-engineer-agent.md)

### 财务事业部 → [finance/](finance/) ✅
[Financial Planning](finance/financial-planning-agent.md) · [Accounting](finance/accounting-agent.md) · [Revenue & Billing](finance/revenue-billing-agent.md) · [Cost Optimization](finance/cost-optimization-agent.md)

### 法务事业部 → [legal/](legal/) ✅
[Contract](legal/contract-agent.md) · [IP & Patent](legal/ip-patent-agent.md) · [Compliance](legal/compliance-agent.md) · [Privacy & Terms](legal/privacy-terms-agent.md)

### 人员与 HR 事业部 → [hr/](hr/) ✅
[Recruiting](hr/recruiting-agent.md) · [Onboarding](hr/onboarding-agent.md) · [Performance & Growth](hr/performance-growth-agent.md) · [Culture](hr/culture-agent.md)

### 运营事业部 → [operations/](operations/) ✅
[Project Management](operations/project-management-agent.md) · [Process Optimization](operations/process-optimization-agent.md) · [Vendor Management](operations/vendor-management-agent.md) · [Knowledge Management](operations/knowledge-management-agent.md)

### 市场事业部 → [marketing/](marketing/) ✅
[Content Marketing](marketing/content-marketing-agent.md) · [SEO](marketing/seo-agent.md) · [Brand & Communications](marketing/brand-communications-agent.md) · [Growth Marketing](marketing/growth-marketing-agent.md)

### 销售事业部 → [sales/](sales/) ✅
[Prospecting](sales/prospecting-agent.md) · [Account Executive](sales/account-executive-agent.md) · [Sales Engineer](sales/sales-engineer-agent.md) · [Deal Desk](sales/deal-desk-agent.md)

### 客户成功事业部 → [customer-success/](customer-success/) ✅
[Customer Onboarding](customer-success/customer-onboarding-agent.md) · [Support](customer-success/support-agent.md) · [Customer Health](customer-success/customer-health-agent.md) · [Renewal & Expansion](customer-success/renewal-expansion-agent.md)

### 数据事业部 → [data/](data/) ✅
[Data Engineer](data/data-engineer-agent.md) · [Analytics Engineer](data/analytics-engineer-agent.md) · [Data Scientist](data/data-scientist-agent.md) · [Data Governance](data/data-governance-agent.md)

### 文档事业部 → [documentation/](documentation/) ✅
[Technical Writer](documentation/technical-writer-agent.md) · [API Documentation](documentation/api-documentation-agent.md) · [Knowledge Base](documentation/knowledge-base-agent.md)

### 硬件事业部 → [hardware/](hardware/) ✅
[Firmware Engineer](hardware/firmware-engineer-agent.md) · [Electrical Engineer](hardware/electrical-engineer-agent.md) · [Mechanical Engineer](hardware/mechanical-engineer-agent.md) · [Hardware Test](hardware/hardware-test-agent.md)

### 投资者关系事业部 → [investor-relations/](investor-relations/) ✅
[Investor Reporting](investor-relations/investor-reporting-agent.md) · [Board Governance](investor-relations/board-governance-agent.md) · [Cap Table](investor-relations/cap-table-agent.md)

---

## 协作规则

每个智能体必须：

1. 解释推理过程。
2. 质疑假设。
3. 评审其他智能体的工作。
4. 在适用时引用证据。
5. 识别风险。
6. 估算成本。
7. 估算时间线。
8. 提供备选方案。
9. 记录决策。
10. 推荐下一步行动。

**没有哪个智能体会在大决策上独立行动。** 战略工作需要跨职能评审，然后由 [CEO 智能体](../orchestration/ceo-agent.md)批准；任何不可逆的事情都会通过 [AI Co-Founder](executive/ai-cofounder-agent.md) 交给人类创始人。
