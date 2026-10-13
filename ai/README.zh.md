# AI 机器侧

[English](README.md) | 中文

**AI 智能体员工队伍运行所依赖的一切。** 这不是关于 AI 的阅读材料，而是关于智能体本身、它们如何被协调以及它们会记住什么的运行规范。

人类一侧位于 [handbook/](../handbook/README.md)。注意区分：

- **`ai/`**（本目录）—— AI *员工队伍*：有哪些智能体，工作如何被路由、评审、批准和记忆。
- **[handbook/departments/ai-engineering/](../handbook/departments/ai-engineering/README.md)** —— 构建 AI 产品的*学科*（RAG、评估、提示词标准、AI 安全）。那是阅读材料。

## 索引

| 区域 | 内容 | 需要定制？ |
|---|---|---|
| [agents/](agents/README.md) | **107 份智能体规格**的注册表 —— [executive/](agents/executive/README.md) 高管团队，外加每个部门一个文件夹，全部遵循[标准 11 段规格](agents/agent-template.md) | ✏️ **总是** —— 启用/移除/新增智能体 |
| [orchestration/](orchestration/README.md) | 内核 —— [CEO 智能体](orchestration/ceo-agent.md) · [规划器](orchestration/planner.md) · [任务分解器](orchestration/task-decomposer.md) · [协调器](orchestration/coordinator.md) · [评审员](orchestration/reviewer.md) · [审批](orchestration/approval-engine.md)/[执行](orchestration/execution-engine.md)/[持续改进](orchestration/continuous-improvement-engine.md)引擎 · [生命周期](orchestration/execution-lifecycle.md) · [运行时](orchestration/runtime.md) | ⚙️ 有时 |
| [memory/](memory/README.md) | 14 类记忆（会话、项目、公司、客户、决策、[经验教训](memory/lessons-learned.md)、[提示词](memory/prompt-memory.md)、[知识库](memory/knowledge-base.md)……）+ [检索](memory/retrieval.md) · [保留与版本化](memory/retention-and-versioning.md) | ⚙️ 有时 |

## 它与 handbook 如何衔接

[handbook/departments/](../handbook/departments/README.md) 中的每个部门在这里都有一个对应的智能体文件夹（`ai/agents/<department>/`）。部门的 `agents.md` 为它们建立索引；智能体执行该部门的[标准](../handbook/standards/README.md)，并通过它的[质量门](../handbook/governance/quality-gates.md)。

在它们之上，[agents/executive/](agents/executive/README.md) 实现了 handbook 所描述的[高管角色](../handbook/company/roles.md) —— 每位高管负责一个或多个部门，这正是每份专家智能体规格上的 **Reports to:** 一行所指向的对象。

## 运行它

这些规格是可执行的。[运行时](../runtime/README.md)会读取 [agents/](agents/README.md) 中的智能体定义，并针对一个请求编排它们 —— 挑选相关智能体、创建临时实例、并行执行相互独立的工作、评审结果，再综合成答案。关于它所依赖的“定义与实例”之分，见 [orchestration/runtime.md](orchestration/runtime.md)。

```bash
python -m ai_native_os run "Design and implement authentication for a web application."
```

## 定制

- **只启用你需要的智能体。** 其余的删掉 —— 它们是运行时会按需实例化的规格，而不是会常驻运行的进程。
- **新增一个智能体：** 复制 [agents/agent-template.md](agents/agent-template.md) 并填写全部 11 个部分。
- **保留内核。** `orchestration/` 和 `memory/` 是框架；只有当你打算改变工作如何被路由或记忆时才改动它们。

见 [CUSTOMIZE.md](../CUSTOMIZE.md)。
