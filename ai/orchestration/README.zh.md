# 编排 —— 内核

[English](README.md) | 中文

编排让 AI-Native OS 能把一个请求转化为经过协同、评审、批准并执行的工作，并交给一支由专业化[智能体](../agents/README.md)组成的员工队伍。没有哪个智能体在大决策上独自工作；内核让许多只专注单一领域的专家表现得像一个可靠的组织。

> **这个内核是可执行的。** 下面的页面规定行为；[runtime.md](runtime.md)
> 指向执行这些行为的代码 —— 为请求挑选智能体、为它们创建临时实例、
> 并行执行相互独立的工作、评审结果，再综合成答案。
> 用 `python -m ai_native_os run "<your request>"` 运行它。

---

## 编排模型

```
Request
  │
  ▼
CEO Agent ──────────────► sets objective, delegates
  │
  ▼
Planner ────────────────► breaks work into a plan
  │
  ▼
Task Decomposer ────────► subtasks + dependencies
  │
  ▼
Coordinator ────────────► routes subtasks to specialist agents (see task-routing.md)
  │        ▲
  │        │ context from Memory Manager + Knowledge Manager
  ▼        │
Specialist Agents ──────► produce deliverables
  │
  ▼
Reviewers (Reviewer · QA · Security · Documentation)
  │
  ▼
Approval Engine ────────► gates + Human-in-the-Loop where required
  │
  ▼
Execution Engine ───────► executes/ships, enforces quality gates
  │
  ▼
Continuous Improvement Engine ──► captures lessons → Memory
```

## 组件

### 协调智能体（完整规格）
| 组件 | 职责 |
|---|---|
| [ceo-agent.md](ceo-agent.md) | 编排一切；只委派，从不实现 |
| [planner.md](planner.md) | 把目标转化为执行计划 |
| [task-decomposer.md](task-decomposer.md) | 把计划拆成带依赖关系的子任务 |
| [coordinator.md](coordinator.md) | 在智能体之间路由与调度工作 |
| [memory-manager.md](memory-manager.md) | 提供并更新[记忆](../memory/) |
| [knowledge-manager.md](knowledge-manager.md) | 提供检索到的[知识](../memory/knowledge-base.md) |
| [reviewer.md](reviewer.md) | 通用的正确性与质量评审 |
| [qa-reviewer.md](qa-reviewer.md) | 测试与质量评审 |
| [security-reviewer.md](security-reviewer.md) | 安全评审 |
| [documentation-reviewer.md](documentation-reviewer.md) | 文档评审 |

### 引擎与流程
| 组件 | 职责 |
|---|---|
| [approval-engine.md](approval-engine.md) | 施加质量门与 Human-in-the-Loop 审批 |
| [execution-engine.md](execution-engine.md) | 执行已批准的工作；强制执行质量门 |
| [continuous-improvement-engine.md](continuous-improvement-engine.md) | 把结果转化为经验教训 |
| [task-routing.md](task-routing.md) | 子任务如何映射到智能体 |
| [execution-lifecycle.md](execution-lifecycle.md) | 委派、冲突解决、重试逻辑、生命周期状态 |
| [runtime.md](runtime.md) | 可执行内核：智能体**定义**与运行中的**实例** |

引擎执行[治理](../../handbook/governance/)：即[决策框架](../../handbook/governance/decision-framework.md)、
[质量门](../../handbook/governance/quality-gates.md)和[完成的定义](../../handbook/governance/definition-of-done.md)。
