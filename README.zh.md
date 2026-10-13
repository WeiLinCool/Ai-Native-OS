# Ai-Native-OS

[English](README.md) | 中文

> **面向 AI 原生科技公司的开源操作系统。**
>
> 版本：3.2 · 克隆它、改造它，让公司从创意一路跑到全球规模。

AI-Native OS 不是提示词合集、代码模板或商业计划书。它是 AI 原生公司如何运转的**唯一事实来源**：组织结构、工程文化、产品研发、研究、运营、AI 智能体员工队伍、编排、记忆、标准、模板、手册，以及按行业划分的起步套件。

它**不绑定行业**、**模块化**。没有任何内容预设某种具体业务。每个部门都是一本自成一体的微型运营手册，遵循同一套结构，因此整个系统可预期、可扩展、可复制。

**规模：** 一个 [AI 高管团队](ai/agents/executive/README.md) · 20 个完整部门 · 107 个 AI 智能体 · 16 个起步套件 · 每个目录都用自身的 `README.md` 自我索引。

**而且它真的会跑。** [运行时](runtime/README.md)会真正编排这些智能体 —— 见下文。

---

## 两侧结构与定制

仓库从中间一分为二。只要清楚自己在哪一侧，定制就一目了然：

| | [handbook/](handbook/README.md) —— 人**读**的部分 | [ai/](ai/README.md) —— AI **运行**的部分 |
|---|---|---|
| **内容** | 公司身份、治理、20 本部门手册、工作流、标准、手册、模板、指南 | 107 份智能体规格（高管团队 + 20 个事业部）、编排内核、记忆系统 |
| **你改它是为了** | 描述*你*的公司如何运转 | 决定有哪些智能体、工作如何路由 |
| **读者** | 创始人、员工、新入职者 | 智能体员工队伍 |

还有第三部分，它*执行*第二部分：[runtime/](runtime/README.md)。

---

## 智能体真的会运行

[运行时](runtime/README.md)读取 [ai/agents/](ai/agents/README.md) 中的智能体规格并编排它们。它挑选请求所需的智能体，只为这些智能体创建临时实例，并行执行相互独立的工作，评审结果，再综合成答案。零依赖，试用不需要 API Key：

```bash
python -m ai_native_os run "Design and implement authentication for a web application."
```

```
CEO Agent
|-- Planner
|   `-- Task Decomposer
|       |-- Software Architect Agent                    [delegated]
|       |   |-- Backend Engineer Agent                       [done]
|       |   |-- Frontend Engineer Agent                      [done]
|       |   `-- API Architect Agent                          [done]
|       `-- Chief Security Officer Agent                [delegated]
|           `-- Security Architect Agent                     [done]
|-- Review panel (3)                                      [approve]
`-- CEO Agent                                                [done]
```

这 107 份规格是**定义** —— 模板。一次运行只实例化它需要的那几个，并在工作完成后终止它们；永远不会同时有 107 个智能体在跑。参见 [ai/orchestration/runtime.md](ai/orchestration/runtime.md)。

---

## 如何定制

AI-Native OS 出厂即完整。要让它成为*你的*系统，主要是**删掉不需要的东西**、**填上你是谁**。按这个顺序来：

**1. 让它成为你的公司** *（约 30 分钟）* —— 编辑这五个文件。它们是唯一定义你身份的地方，其余一切都回指它们。
[mission](handbook/company/mission.md) · [vision](handbook/company/vision.md) · [principles](handbook/company/principles.md) · [structure](handbook/company/structure.md) · [roles](handbook/company/roles.md)

**2. 选一个起步套件** *（约 10 分钟）* —— 挑一个与你公司类型匹配的[套件](#起步套件)。它会告诉你先启用哪些部门，并补充行业标准。其余的套件删掉。

**3. 只保留需要的部门** *（约 30 分钟）* —— 第一天不需要全部二十个。典型的早期软件公司跑 `product`、`engineering`、`design`、`post-launch`、`strategy`。
删除一个部门：删掉 `handbook/departments/<name>/` 和 `ai/agents/<name>/`，从各索引中去掉它的行，再从 [scripts/check-structure.py](scripts/check-structure.py) 的 `DEPARTMENT_NAMES` 中移除，然后运行下面的检查。
新增一个部门：`python scripts/scaffold.py department <name>`。

**4. 挑选你的智能体** *（约 20 分钟）* —— 打开 [ai/agents/README.md](ai/agents/README.md)，留下真正会用的，删掉其余。新增一个：`python scripts/scaffold.py agent <department> <agent-name>`。

**5. 调整规则** *（持续进行）* —— 按你想要的严格程度调整[质量门](handbook/governance/quality-gates.md)、[决策框架](handbook/governance/decision-framework.md)以及各部门的 `standards.md`。

### 一眼看清该改什么

| | 文件 | 说明 |
|---|---|---|
| ✏️ **总是要改** | `handbook/company/*`、`ai/agents/*` | 这*就是*你的公司和你的员工队伍 |
| ⚙️ **经常要改** | 部门的 `standards.md`、`metrics.md`、`quality-gates.md`、`governance/*` | 按你的标准来调 |
| 📖 **读，但别改** | `handbook/guides/*` | 是给你的指导，不是配置 |
| 🔒 **别动** | `handbook/templates/*`、`STRUCTURE.md`、`scripts/*`、`.github/*` | 保持整个系统一致的框架 |

### 验证你的改动

```bash
python scripts/check-links.py        # 所有内部链接均可解析
python scripts/check-structure.py    # 部门与智能体规格符合约定
python scripts/check-conventions.py  # 每个目录自索引、无占位文本
python runtime/run_tests.py          # 运行时仍能编排你的智能体
node --experimental-strip-types scripts/run-gates.ts   # 双语 README 配对保持一致
```

五项检查在每次 push 和 PR 时都由 CI 运行。如果你删掉了某个部门，`check-links.py` 会指出所有仍指向它的链接。

👉 完整细节（包括如何手工新增部门或智能体）：**[CUSTOMIZE.md](CUSTOMIZE.md)**。

---

## 目录结构

```
ai-native-os/
│
├── handbook/                  ◀── EVERYTHING YOU READ ─────────────────────────
│   ├── company/                   identity: mission, vision, principles, structure, roles
│   ├── governance/                decision framework, quality gates, definition of done
│   │
│   ├── departments/               20 department manuals, each the same 18-file shape:
│   │   ├── engineering/  product/  design/  post-launch/  ai-engineering/
│   │   ├── research/  strategy/  data/  hardware/
│   │   ├── marketing/  sales/  customer-success/
│   │   └── operations/  hr/  finance/  legal/  security/  devops/
│   │       documentation/  investor-relations/
│   │           └─ README · mission · vision · principles · organization · roles
│   │              agents · workflows · playbooks · sops · decision-frameworks
│   │              standards · review-process · quality-gates · automation
│   │              metrics · dashboards · tools + templates/ checklists/ examples/
│   │
│   ├── workflows/                 cross-department processes (the 20-phase SDLC)
│   ├── standards/                 index of every company-wide standard
│   ├── playbooks/                 brainstorm · MVP · launch · sprint · hiring · fundraising
│   ├── templates/                 department-template/ + documents/ (PRD, RFC, ADR, OKR…)
│   └── guides/                    company-building-guide · onboarding-paths · okrs · example-company
│
├── ai/                        ◀── EVERYTHING THE AI RUNS ON ──────────────────
│   ├── agents/                    107 agent specs
│   │   ├── executive/             the C-suite: AI Co-Founder · CTO · CPO · COO · CFO · CMO · CRO
│   │   │                          Chief Designer/Scientist/Data/Security/Legal/People · Chief of Staff
│   │   └── engineering/ product/ post-launch/ design/ research/ ai-engineering/ …
│   │                              one folder per department, each reporting to its executive
│   ├── orchestration/             the kernel: CEO agent, planner, engines, reviewers
│   └── memory/                    14 memory types + retrieval, retention, versioning
│
├── runtime/                   ◀── THE KERNEL, EXECUTABLE ──────────────────────
│   ├── ai_native_os/              registry · planner · decomposer · selector · spawner
│   │                              scheduler · reviewer · synthesizer · agent map
│   │                              providers (anthropic · openai · local · mock) · tools · memory
│   └── tests/                     220 tests, stdlib only, no API keys needed
│
├── starter-kits/              ◀── PICK YOUR COMPANY TYPE ────────────────────
│   └── ai-startup/ saas/ developer-tools/ enterprise-b2b/ marketplace/
│       consumer-app/ robotics/ drone/ embedded/ iot/ research-lab/
│
├── scripts/                       doc CI tooling: checkers, doc gates, scaffolding
├── .github/                       issue/PR templates, community health, CI workflows
│
└── README.md  CUSTOMIZE.md  STRUCTURE.md  GLOSSARY.md
    CONTRIBUTING.md  CHANGELOG.md  ROADMAP.md  LICENSE
```

---

## 本页目录

- [如何定制](#如何定制) · [目录结构](#目录结构)
- [从这里开始](#从这里开始) · [元信息与约定](#元信息与约定)
- [handbook 阅读侧](#handbook-阅读侧)
- [ai 机器侧](#ai-机器侧)
- [创始人旅程](#创始人旅程) —— 创意 → 验证 → 构建 → 发布 → 销售 → 融资 → 规模化
- [起步套件](#起步套件) · [自动化](#自动化)
- [设计哲学](#设计哲学) · [贡献与扩展](#贡献与扩展) · [许可证](#许可证)

---

## 从这里开始

1. **第一次创业？** 读 **[公司构建指南](handbook/guides/company-building-guide.md)** —— 需要掌握的能力，以及构建和经营一家公司的完整步骤。
2. **想把它变成你的公司？** 按 **[CUSTOMIZE.md](CUSTOMIZE.md)** 操作。
3. **要采用这套 OS？** [公司身份](handbook/company/README.md) → [治理](handbook/governance/README.md) → [内核](ai/orchestration/README.md) + [记忆](ai/memory/README.md)。
4. **要做某类特定公司？** 选一个[起步套件](#起步套件)。

> 每个目录都有自己的 `README.md` 作为索引。本页是顶层索引；点开任意链接即可进入该区域的索引查看完整内容。

## 元信息与约定

| 文件 | 用途 |
|---|---|
| [CUSTOMIZE.md](CUSTOMIZE.md) | 如何把这个仓库变成你自己的 |
| [STRUCTURE.md](STRUCTURE.md) | 仓库地图 + 命名与写作约定 |
| [GLOSSARY.md](GLOSSARY.md) | 共享词汇表 |
| [CONTRIBUTING.md](CONTRIBUTING.md) | 如何新增部门、智能体和文档 |
| [CHANGELOG.md](CHANGELOG.md) · [ROADMAP.md](ROADMAP.md) | 变更记录 · 下一步计划 |
| [LICENSE](LICENSE) | MIT |

---

## handbook 阅读侧

完整索引：**[handbook/README.md](handbook/README.md)**

| 区域 | 内容 |
|---|---|
| [company/](handbook/company/README.md) | [mission](handbook/company/mission.md) · [vision](handbook/company/vision.md) · [principles](handbook/company/principles.md) · [structure](handbook/company/structure.md) · [roles](handbook/company/roles.md) |
| [governance/](handbook/governance/README.md) | [决策框架](handbook/governance/decision-framework.md) · [质量门](handbook/governance/quality-gates.md) · [沟通规则](handbook/governance/communication-rules.md) · [完成的定义](handbook/governance/definition-of-done.md) · [失败处理](handbook/governance/failure-handling.md) |
| [workflows/](handbook/workflows/README.md) | 20 阶段 [SDLC](handbook/workflows/sdlc.md) |
| [standards/](handbook/standards/README.md) | 全公司标准的索引 |
| [templates/](handbook/templates/README.md) | [部门模板](handbook/templates/department-template/) · 17 个[文档模板](handbook/templates/documents/README.md)：[PRD](handbook/templates/documents/prd.md) · [RFC](handbook/templates/documents/rfc.md) · [ADR](handbook/templates/documents/adr.md) · [事故报告](handbook/templates/documents/incident-report.md) · [安全评审](handbook/templates/documents/security-review.md) · [发布检查清单](handbook/templates/documents/release-checklist.md) · [OKR](handbook/templates/documents/okr.md) · [一页纸](handbook/templates/documents/one-pager.md) · [录用通知](handbook/templates/documents/offer-letter.md) · [劳动合同](handbook/templates/documents/employment-agreement.md) · [董事会汇报](handbook/templates/documents/board-update.md) · [销售方案](handbook/templates/documents/sales-proposal.md) · [QBR](handbook/templates/documents/qbr.md) · [DPA](handbook/templates/documents/dpa.md) |
| [playbooks/](handbook/playbooks/README.md) | [头脑风暴](handbook/playbooks/brainstorming-ideas.md) · [验证创意](handbook/playbooks/validating-an-idea.md) · [打造 MVP](handbook/playbooks/building-an-mvp.md) · [发布](handbook/playbooks/launching-a-product.md) · [跑一个迭代](handbook/playbooks/running-a-sprint.md) · [招聘工程师](handbook/playbooks/hiring-an-engineer.md) · [路演](handbook/playbooks/pitching-to-investors.md) · [融资](handbook/playbooks/fundraising.md) · [客户投诉](handbook/playbooks/handling-a-customer-complaint.md) · [团队扩张](handbook/playbooks/scaling-a-team.md) · [国际化扩张](handbook/playbooks/international-expansion.md) |
| [guides/](handbook/guides/README.md) | [公司构建指南](handbook/guides/company-building-guide.md) · [入职路径](handbook/guides/onboarding-paths.md) · [OKR](handbook/guides/okrs.md) · [完整示例](handbook/guides/example-company.md) |

### 部门 20 个

完整索引：**[handbook/departments/README.md](handbook/departments/README.md)**

| 部门 | 负责什么 |
|---|---|
| [engineering/](handbook/departments/engineering/README.md) | 可维护、有测试、安全的软件；标准、评审、交付 |
| [product/](handbook/departments/product/README.md) | *正确的*产品 —— 发现、PRD、优先级、路线图、PMF |
| [post-launch/](handbook/departments/post-launch/README.md) | 上线后的可靠性 —— 监控、事故、维护、[技术债](handbook/departments/post-launch/technical-debt/)、EOL |
| [design/](handbook/departments/design/README.md) | 可用、无障碍的体验；[设计系统](handbook/departments/design/design-system.md) |
| [research/](handbook/departments/research/README.md) | 下一步该做什么 —— [创意发散](handbook/departments/research/ideation.md)、[TRL](handbook/departments/research/technology-readiness.md)、[机会评分](handbook/departments/research/opportunity-scoring.md) |
| [ai-engineering/](handbook/departments/ai-engineering/README.md) | 构建 AI 产品 —— RAG、[评估](handbook/departments/ai-engineering/evaluation-and-testing.md)、[提示词标准](handbook/departments/ai-engineering/prompt-engineering.md)、[AI 安全](handbook/departments/ai-engineering/ai-security.md) |
| [strategy/](handbook/departments/strategy/README.md) | 构建公司 —— [生命周期](handbook/departments/strategy/startup-lifecycle.md)、[市场](handbook/departments/strategy/market-analysis.md)、[商业模式](handbook/departments/strategy/business-model.md)、[单位经济](handbook/departments/strategy/unit-economics.md) |
| [security/](handbook/departments/security/README.md) | 威胁建模、渗透测试、漏洞管理、合规、隐私 |
| [devops/](handbook/departments/devops/README.md) | CI/CD、基础设施即代码、发布、可靠性（DORA/SRE） |
| [finance/](handbook/departments/finance/README.md) | 预测、预算、会计、计费、现金跑道、成本 |
| [legal/](handbook/departments/legal/README.md) | 合同、知识产权、合规、隐私与条款 |
| [hr/](handbook/departments/hr/README.md) | 招聘、入职、绩效、文化 |
| [operations/](handbook/departments/operations/README.md) | 节奏、项目管理、流程、供应商与知识管理 |
| [marketing/](handbook/departments/marketing/README.md) | 定位、内容/SEO、品牌、增长、[心理学](handbook/departments/marketing/psychology.md) |
| [sales/](handbook/departments/sales/README.md) | 销售 —— [方法论](handbook/departments/sales/methodology.md)、[心理学](handbook/departments/sales/psychology.md)、[渠道](handbook/departments/sales/channels.md) |
| [customer-success/](handbook/departments/customer-success/README.md) | 上手、健康度评分、留存、增购 |
| [data/](handbook/departments/data/README.md) | 数据管道、指标层、分析、治理 |
| [documentation/](handbook/departments/documentation/README.md) | 产品与 API 文档、知识库、时效性 |
| [hardware/](handbook/departments/hardware/README.md) | 固件、电子、机械、测试 —— 面向实体产品 |
| [investor-relations/](handbook/departments/investor-relations/README.md) | 投资人更新、董事会治理、股权结构表 |

---

## ai 机器侧

完整索引：**[ai/README.md](ai/README.md)**

| 区域 | 内容 |
|---|---|
| [agents/](ai/agents/README.md) | **107 份智能体规格**的注册表 + [标准 11 段规格](ai/agents/agent-template.md) |
| [agents/executive/](ai/agents/executive/README.md) | **AI 高管团队** —— [AI Co-Founder](ai/agents/executive/ai-cofounder-agent.md) · [CTO](ai/agents/executive/cto-agent.md) · [CPO](ai/agents/executive/cpo-agent.md) · [COO](ai/agents/executive/coo-agent.md) · [CFO](ai/agents/executive/cfo-agent.md) · [CRO](ai/agents/executive/cro-agent.md) · [CMO](ai/agents/executive/cmo-agent.md) · [Chief Designer](ai/agents/executive/chief-designer-agent.md) · [Chief Scientist](ai/agents/executive/chief-scientist-agent.md) · [CDO](ai/agents/executive/chief-data-officer-agent.md) · [CSO](ai/agents/executive/chief-security-officer-agent.md) · [CLO](ai/agents/executive/chief-legal-officer-agent.md) · [CPeO](ai/agents/executive/chief-people-officer-agent.md) · [Chief of Staff](ai/agents/executive/chief-of-staff-agent.md) |
| [orchestration/](ai/orchestration/README.md) | [CEO 智能体](ai/orchestration/ceo-agent.md) · [规划器](ai/orchestration/planner.md) · [任务分解器](ai/orchestration/task-decomposer.md) · [协调器](ai/orchestration/coordinator.md) · [评审员](ai/orchestration/reviewer.md) · [QA](ai/orchestration/qa-reviewer.md)/[安全](ai/orchestration/security-reviewer.md)/[文档](ai/orchestration/documentation-reviewer.md)评审员 · [审批](ai/orchestration/approval-engine.md)/[执行](ai/orchestration/execution-engine.md)/[持续改进](ai/orchestration/continuous-improvement-engine.md)引擎 · [生命周期](ai/orchestration/execution-lifecycle.md) |
| [memory/](ai/memory/README.md) | 14 类记忆（会话 → 公司、项目、客户、决策、[经验教训](ai/memory/lessons-learned.md)、[提示词](ai/memory/prompt-memory.md)、[知识库](ai/memory/knowledge-base.md)……）+ [上下文](ai/memory/context-management.md) · [检索](ai/memory/retrieval.md) · [保留与版本化](ai/memory/retention-and-versioning.md) |

> 别把 `ai/`（AI **员工队伍**）和 [handbook/departments/ai-engineering/](handbook/departments/ai-engineering/README.md)（构建 AI 产品的**学科**）混为一谈。

---

## 创始人旅程

一家公司走过的端到端路径，以及每个阶段对应的确切文档。[公司构建指南](handbook/guides/company-building-guide.md)讲述了整条弧线。

| 阶段 | 去哪看 |
|---|---|
| **0 · 头脑风暴** | [创意发散](handbook/departments/research/ideation.md) · [手册](handbook/playbooks/brainstorming-ideas.md) |
| **1 · 验证创意** | [创意验证](handbook/departments/strategy/idea-validation.md) · [产品发现](handbook/departments/product/discovery.md) · [手册](handbook/playbooks/validating-an-idea.md) |
| **2 · 评估与排序** | [技术成熟度（TRL）](handbook/departments/research/technology-readiness.md) · [机会评分](handbook/departments/research/opportunity-scoring.md) · [市场分析](handbook/departments/strategy/market-analysis.md) |
| **3 · 商业模式** | [商业模式与定价](handbook/departments/strategy/business-model.md) · [单位经济](handbook/departments/strategy/unit-economics.md) |
| **4 · 构建** | [SDLC](handbook/workflows/sdlc.md) · [MVP 手册](handbook/playbooks/building-an-mvp.md) · [工程](handbook/departments/engineering/README.md) · [设计](handbook/departments/design/README.md) |
| **5 · 发布** | [发布手册](handbook/playbooks/launching-a-product.md) · [发布管理](handbook/departments/post-launch/release-management.md) |
| **6 · 销售** | [怎么卖](handbook/departments/sales/methodology.md) · [买方心理学](handbook/departments/sales/psychology.md) · [在哪卖](handbook/departments/sales/channels.md) · [GTM](handbook/departments/strategy/go-to-market.md) |
| **7 · 融资** | [路演](handbook/departments/strategy/pitching.md) · [寻找投资人](handbook/departments/strategy/finding-investors.md) · [融资手册](handbook/playbooks/fundraising.md) |
| **8 · 运营与规模化** | [运营节奏](handbook/guides/company-building-guide.md) · [OKR](handbook/guides/okrs.md) · [持续改进](handbook/departments/post-launch/continuous-improvement.md) |

---

## 起步套件

预配置的公司类型，继承 AI-Native OS 内核并叠加行业差异 —— 见 [starter-kits/](starter-kits/README.md)。

[ai-startup](starter-kits/ai-startup/) · [saas](starter-kits/saas/) · [developer-tools](starter-kits/developer-tools/) · [enterprise-b2b](starter-kits/enterprise-b2b/) · [marketplace](starter-kits/marketplace/) · [consumer-app](starter-kits/consumer-app/) · [robotics](starter-kits/robotics/) · [drone](starter-kits/drone/) · [embedded](starter-kits/embedded/) · [iot](starter-kits/iot/) · [research-lab](starter-kits/research-lab/) · [fintech](starter-kits/fintech/) · [healthtech](starter-kits/healthtech/) · [climate-tech](starter-kits/climate-tech/) · [gaming](starter-kits/gaming/) · [edtech](starter-kits/edtech/)

## 自动化

| 脚本 | 用途 |
|---|---|
| [scripts/scaffold.py](scripts/scaffold.py) | 从模板生成新的部门或智能体 |
| [scripts/check-links.py](scripts/check-links.py) | 所有内部链接均可解析 |
| [scripts/check-structure.py](scripts/check-structure.py) | 部门与智能体规格符合约定 |
| [scripts/check-conventions.py](scripts/check-conventions.py) | 每个目录自索引；无占位文本 |
| [scripts/run-gates.ts](scripts/run-gates.ts) | 文档门禁：双语 README 配对保持一致 |
| [scripts/i18n-record.py](scripts/i18n-record.py) | 重新记录双语配对哈希 |

这三项检查在每次 push 和 PR 时都由 CI 运行（[.github/](.github/) 里还放了 issue/PR 模板、行为准则、安全策略、支持渠道、赞助配置和一个过期 issue 机器人）。

---

## 设计哲学

- **两侧分明** —— [handbook/](handbook/README.md) 给人，[ai/](ai/README.md) 给智能体员工队伍。边界清晰，所以定制路径也清晰。
- **模块化且不绑定行业** —— 支持 SaaS、AI、机器人、嵌入式、IoT、硬件、无人机、医疗健康、金融科技、气候科技、研究实验室、开发者工具、消费级与企业级。
- **处处同一套结构** —— 每个部门都用[标准结构](STRUCTURE.md#standard-department-structure)；每个智能体都用[标准规格](ai/agents/agent-template.md)。可预期，才可扩展。
- **证据胜于假设 · 第一性原理 · 长期价值** —— 见 [handbook/company/principles.md](handbook/company/principles.md)。
- **生产可用，绝不占位** —— 每份文档都写成真正会被使用的样子。

---

## 贡献与扩展

新增部门：复制 [handbook/templates/department-template/](handbook/templates/department-template/) 并填写。新增智能体：复制 [ai/agents/agent-template.md](ai/agents/agent-template.md)。提交 PR 前先运行 `python scripts/check-links.py` 和 `python scripts/check-structure.py`。完整约定见 [CONTRIBUTING.md](CONTRIBUTING.md)。

> 最初催生本仓库的单文件运营手册被拆解成了上面的结构。它的完整文本保留在 git 历史中（拆解前的 `README.md`）。

---

## 许可证

AI-Native OS 基于 [MIT 许可证](LICENSE) 发布 —— 可自由克隆、定制并商用。

---

## 致谢

AI-Native OS 是 **[rojenwai/CompanyOS](https://github.com/rojenwai/CompanyOS)**（MIT）的 fork，被重组为 handbook/ + ai/ 两侧结构并加上可执行的运行时。上游版权声明保留在 [LICENSE](LICENSE) 中。
