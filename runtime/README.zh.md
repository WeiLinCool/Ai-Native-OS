# Ai-Native-OS 运行时

[English](README.md) | 中文

**[编排内核](../ai/orchestration/README.md)的可执行形态。**

`ai/agents/` 存放 107 份智能体*规格*。这个包读取它们并运行它们：它会挑选
一次请求所需的智能体，为它们创建临时实例，并行执行相互独立的工作，
评审结果，再综合成答案。

零依赖。试用不需要 API Key。

```bash
python -m ai_native_os run "Design and implement authentication for a web application."
```

---

## 一切都建立在这个区分之上

| | 智能体**定义** | 智能体**实例** |
|---|---|---|
| **是什么** | “这类智能体*是*什么” | “处理*单个*任务的临时智能体” |
| **存在于** | `ai/agents/**/*.md` —— Markdown，受版本控制 | 记忆中，仅在单个任务期间 |
| **数量** | 117（107 份规格 + 内核智能体） | 通常每次运行 3–6 个，上限由 `max_agents` 决定 |
| **生命周期** | 永久 | 创建 → 执行 → 捕获结果 → 终止 |
| **状态** | 不可变、共享 | 自己的任务、限定范围的上下文与工具授权 |
| **类型** | [`AgentDefinition`](ai_native_os/registry/definition.py) | [`AgentInstance`](ai_native_os/orchestration/spawner.py) |

**永远不会有 107 个智能体同时运行。** 注册表存放 117 份定义；一次运行只实例化
任务真正需要的那几个，并在结果被捕获后立即终止每一个。

---

## 流程

```
User request
    │
    ▼
CEO / entry agent ──────────── receives the request, owns the final answer
    │
    ▼
Planner ────────────────────── objective + required capabilities   (ai/orchestration/planner.md)
    │
    ▼
Task Decomposer ────────────── subtask DAG                  (ai/orchestration/task-decomposer.md)
    │
    ▼
Agent Selection ────────────── capability matching against the registry
    │
    ▼
Dynamic Spawning ───────────── one temporary instance per task
    ├── Agent A ──┐
    ├── Agent B ──┤ parallel where independent, sequential where dependent
    └── Agent C ──┘
    │
    ▼
Result Aggregation ─────────── successes, failures, partials, metadata
    │
    ▼
Reviewer panel ─────────────── Reviewer · QA · Security · Documentation
    │                             │
    │                             └── revise → back to the author, with findings
    ▼
Synthesis ──────────────────── the entry agent composes the final answer
    │
    ▼
Final response + Agent Map
```

---

## 组件

| 组件 | 模块 | 其行为来自 |
|---|---|---|
| **智能体注册表** | [`registry/registry.py`](ai_native_os/registry/registry.py) | `ai/agents/**`, `ai/orchestration/*` |
| 规格解析器 | [`registry/parser.py`](ai_native_os/registry/parser.py) | 11 段规格格式 |
| 能力分类法 | [`registry/capabilities.py`](ai_native_os/registry/capabilities.py) | — |
| **规划器** | [`orchestration/planner.py`](ai_native_os/orchestration/planner.py) | [`planner.md`](../ai/orchestration/planner.md) |
| **任务分解器** | [`orchestration/decomposer.py`](ai_native_os/orchestration/decomposer.py) | [`task-decomposer.md`](../ai/orchestration/task-decomposer.md) |
| **智能体选择器** | [`orchestration/selector.py`](ai_native_os/orchestration/selector.py) | [`task-routing.md`](../ai/orchestration/task-routing.md) |
| **智能体创建器** | [`orchestration/spawner.py`](ai_native_os/orchestration/spawner.py) | — |
| **调度器** | [`orchestration/scheduler.py`](ai_native_os/orchestration/scheduler.py) | [`coordinator.md`](../ai/orchestration/coordinator.md) |
| **上下文构建器** | [`orchestration/context.py`](ai_native_os/orchestration/context.py) | [`context-management.md`](../ai/memory/context-management.md) |
| **结果聚合器** | [`orchestration/aggregator.py`](ai_native_os/orchestration/aggregator.py) | — |
| **评审器** | [`orchestration/reviewer.py`](ai_native_os/orchestration/reviewer.py) | [`reviewer.md`](../ai/orchestration/reviewer.md), [`approval-engine.md`](../ai/orchestration/approval-engine.md) |
| **综合器** | [`orchestration/synthesizer.py`](ai_native_os/orchestration/synthesizer.py) | [`ceo-agent.md`](../ai/orchestration/ceo-agent.md) |
| **智能体地图** | [`orchestration/agent_map.py`](ai_native_os/orchestration/agent_map.py) | — |
| **记忆** | [`memory/`](ai_native_os/memory/) | [`ai/memory/`](../ai/memory/README.md), [`retrieval.md`](../ai/memory/retrieval.md) |
| **工具 + 策略** | [`tools/`](ai_native_os/tools/) | 每份规格的第 5 节 |
| **提供方** | [`providers/`](ai_native_os/providers/) | — |
| **可观测性** | [`observability/trace.py`](ai_native_os/observability/trace.py) | [`execution-lifecycle.md`](../ai/orchestration/execution-lifecycle.md) |

---

## 智能体选择

选择由能力驱动。任何地方都不存在 `if task == X: use agent Y` 这样的表。

每份定义在加载时都会用**能力分类法**匹配它自己的规格文本、标题和文件夹来打标签。
任务所需的能力随后会与每一份定义逐一打分：

| 信号 | 权重 | 原因 |
|---|---|---|
| 精确能力匹配 | ×3.0，随深度放大 | 该智能体的规格声明了这项能力 |
| 能力**深度** | 每多一个信号短语 +0.25 | Database Engineer 提到数据库五次；API Architect 一次 |
| 以该能力命名 | +1.0 | “Database Engineer”*就是*数据库智能体 |
| 同一命名空间 | ×1.25 | `security.pentest` 仍然指向安全事业部 |
| 词法贴合度（IDF） | ×2.0 | 捕捉分类法中没有对应短语的措辞 |
| 所属事业部 | +0.75 | 结构性先验 |
| 委派者 | **排除** | 高管负责委派；它从不拥有交付物 |

直接查看：

```bash
python -m ai_native_os select "threat model the login flow" -c security.threat-modeling
```

```
  score  agent                                                matched capabilities
   6.50  security/security-architect-agent                    security.threat-modeling
   4.25  security/penetration-testing-agent                   security.threat-modeling
   2.50  security/compliance-privacy-agent                    security.threat-modeling
```

**新增一个智能体不需要写代码。** 把一份新的 11 段 Markdown 规格放进
`ai/agents/<division>/`，它会在下次运行时被发现、打标签并可被选择。

---

## 并行执行

[调度器](ai_native_os/orchestration/scheduler.py)遍历任务 DAG，并在*它自己的*依赖完成的
那一刻启动任务 —— 它不会等待整个批次。相互独立的任务最多并发到 `max_parallel`；
有依赖关系的任务在构造上就不可能重叠。

```
Task A ──┐                         Research
Task B ──┼──→ aggregator              ↓
Task C ──┘                         Analysis
                                      ↓
   concurrent                    Recommendation
                                   sequential
```

失败的任务只会把它自己的依赖方标记为 `SKIPPED`。运行的其他部分继续，缺口会在
最终答案中说明，而不是被隐藏。被标记为 `optional` 的依赖失败时不会阻塞
它的依赖方。

---

## 评审循环

聚合之后，与工作所涉及关注点对应的评审智能体会**并行**处理合并后的结果。
它们的结论按最差优先合并：

```
approve → approve_with_changes → revise → reject → escalate → block
```

- **revise / reject** → 受影响的任务会连同发现一起退回*它们的原始作者*
  （确定性失败会退回作者，依据
  [`execution-lifecycle.md`](../ai/orchestration/execution-lifecycle.md) —— 绝不盲目重试）。
  受 `max_iterations` 和 `max_attempts_per_task` 约束。
- **escalate** → 运行会结束，但会被标记给人类。
- **block** → 只有安全评审员能发出。它会把运行置为 `AWAITING_APPROVAL`，并且
  永远不会被自动清除（[`approval-engine.md`](../ai/orchestration/approval-engine.md)）。

评审员*运行失败*时会升级。它永远不会悄悄批准。

---

## 上下文隔离

每个实例接收自己的任务、父目标、**它真正依赖的任务的输出**、自己的评审发现，
以及一次有界的记忆检索。它不会接收对话、兄弟分支
或同伴的输出。

智能体没有自己写的所有内容都会被包裹：

```
<untrusted source="agent:research/market-research-agent">
...another agent's output...
</untrusted>
```

并且每个系统提示词都声明这类块是**数据，而不是指令**。`AgentResult.context_keys`
准确记录了一个实例被赋予了哪些切片，因此隔离性事后可审计。

---

## 护栏

| 限制 | 默认值 | 阻止 |
|---|---|---|
| `max_agents` | 12 | 失控创建 |
| `max_depth` | 3 | 无界嵌套 |
| `max_iterations` | 2 | 无休止的计划/评审循环 |
| `max_parallel` | 4 | 资源耗尽 |
| `max_attempts_per_task` | 2 | 重试循环 |
| `task_timeout_s` | 120 | 智能体卡死 |
| `run_timeout_s` | 600 | 运行卡死 |
| `max_total_tokens` | 400 000 | 成本 |
| `max_tool_calls_per_agent` | 8 | 工具循环 |
| `max_context_chars` | 24 000 | 上下文膨胀 |

每一条都在代码中强制执行，并有测试覆盖。触到某条限制会让运行降级 —— 它带着已有的结果
结束并说明情况 —— 而不是崩溃。

---

## 安全模型

被创建的智能体按模型生成的指令行动，因此它们被视为不可信：

- **没有 shell，没有网络，不能写文件系统。** 这些工具只以明确拒绝的形式存在。
- **默认拒绝工具。** 一次授权必须同时通过运行时黑名单、规格自身的禁止项，以及
  变更型工具检查。被创建的智能体始终严格弱于运行它的进程。
- **路径沙箱。** 读取被限制在 `ai/`、`handbook/`、`starter-kits/`；绝对路径、根路径、
  目录穿越和非文本文件都会被拒绝。
- **没有秘密能到达智能体。** API Key 位于提供方层；`ToolContext` 不携带任何
  环境或提供方句柄。
- **记忆写入只是提案。** 任何临时实例都不能写入持久化的组织记忆；
  晋升是一个单独的、受策略门控的步骤（默认关闭）。

---

## 提供方

编排器只与一个接口对话，从不直接对接厂商 SDK。

| 名称 | 后端 |
|---|---|
| `mock` | 离线、确定性。默认值。 |
| `anthropic` | Messages API（`ANTHROPIC_API_KEY`） |
| `openai` | Chat Completions（`OPENAI_API_KEY`） |
| `local` | 任何 OpenAI 兼容服务器 —— Ollama、vLLM、LM Studio —— 通过 `--base-url` |

```bash
python -m ai_native_os run "..." --provider anthropic --model claude-sonnet-5
python -m ai_native_os run "..." --provider local --base-url http://localhost:11434/v1
```

用 `ai_native_os.providers.register_provider(name, factory)` 注册你自己的提供方。

### 关于 mock 提供方

`mock` 是一个真实提供方，用基于规则的方式代替模型，因此离线运行会走**真正的**编排
路径 —— 真实注册表、真实能力匹配、真实 DAG 调度、真实评审循环。它的文本输出会被
标注为 `[simulated output]`。它用于演练这套机制，
也用于测试；它不是模型推理的替代品。

---

## 运行方式

```bash
python -m ai_native_os doctor                     # check specs, memory, and paths
python -m ai_native_os run "<request>"            # orchestrate, offline
python -m ai_native_os run "<request>" -v         # stream every event
python -m ai_native_os run "<request>" --map m.json --save run.json
python -m ai_native_os agents list --division security
python -m ai_native_os agents show cto-agent
python -m ai_native_os select "<task>" -c <capability>
python -m ai_native_os capabilities
python -m ai_native_os map m.json                 # render a saved Agent Map
```

在 Python 中：

```python
from ai_native_os import Orchestrator, RuntimeConfig

config = RuntimeConfig.load()                  # auto-detects the repo root
orchestrator = Orchestrator(config)
run = orchestrator.run_sync("Design and implement authentication.")

print(run.final_output)
print(orchestrator.agent_map(run))             # the execution graph, as data
```

配置也可以来自仓库根目录的 `ai-native-os.json`：

```json
{
  "provider": { "name": "anthropic", "model": "claude-sonnet-5" },
  "limits":   { "max_agents": 8, "max_parallel": 3 },
  "denied_tools": ["shell", "write_file", "http_request", "remember"]
}
```

---

## 智能体地图

每次运行都会产生一份可序列化的执行图 —— UI 渲染的数据。它是运行记录的纯投影，
因此可以随时从保存的运行中重建。

```json
{
  "run_id": "run_a97b09b5",
  "root_task": "Design and implement authentication for a web application.",
  "status": "completed",
  "nodes": [
    { "id": "entry", "parent_id": null, "kind": "entry", "agent": "CEO Agent", "status": "completed" },
    { "id": "supervisor:executive/chief-security-officer-agent", "parent_id": "decomposer",
      "kind": "supervisor", "agent": "Chief Security Officer Agent", "spawned": false,
      "status": "delegated" },
    { "id": "task:task_3f9a", "parent_id": "supervisor:executive/chief-security-officer-agent",
      "kind": "agent", "agent": "Security Architect Agent", "status": "completed",
      "spec_state": "DONE", "spawned": true, "duration_s": 0.004,
      "usage": { "total_tokens": 812 }, "context_keys": ["your task", "why this work exists"] }
  ],
  "edges": [
    { "from": "decomposer", "to": "supervisor:executive/chief-security-officer-agent", "type": "delegates" },
    { "from": "task:task_1", "to": "task:task_4", "type": "depends_on" }
  ],
  "counts": { "nodes": 11, "spawned": 5, "completed": 5, "failed": 0, "currently_running": [] }
}
```

节点类型：`entry`、`kernel`、`supervisor`、`agent`、`reviewer`、`synthesis`。
边类型：`delegates`、`depends_on`、`reviewed_by`、`reports_to`。

`supervisor` 节点带有 `spawned: false`。它们是从规格自身的汇报线中抽出的责任链 ——
CTO 被表示为工程工作的负责人，**而不会创建 CTO
的实例**。

`render_tree()` 为终端绘制同一份文档。

---

## 可观测性

每次运行都会把 JSONL 追踪写入 `.ai-native-os/runs/<run_id>.jsonl`，每个事件一行：

```
run.started · plan.created · tasks.decomposed · agent.selected · agent.spawned · agent.started
agent.completed | agent.failed | agent.timeout · agent.terminated · tool.called | tool.denied
task.status · task.skipped · task.retry · review.started · review.completed · approval.required
memory.proposed · limit.exceeded · synthesis.started · run.completed
```

每条都带有运行 id、任务 id、智能体 id、父智能体、时间戳以及该步骤特有的数据。

---

## 测试

220 个测试，仅用标准库 `unittest`，无网络、无 API Key —— mock 提供方代替模型。

```bash
python runtime/run_tests.py          # from the repo root
python -m unittest discover -s tests # from runtime/
pytest tests                         # if you have pytest
```

| 文件 | 覆盖内容 |
|---|---|
| [`test_registry.py`](tests/test_registry.py) | 发现、两种头部写法、能力提取、层级关系、新规格变为可被选择 |
| [`test_selector.py`](tests/test_selector.py) | 按能力选择、深度加权、委派者排除、团队选择、评审员选择 |
| [`test_decomposer.py`](tests/test_decomposer.py) | 规划、分解，以及敌意模型输出 —— 环、重复 id、前向引用、垃圾内容 |
| [`test_graph.py`](tests/test_graph.py) | DAG 校验、拓扑序、批次、就绪性、可选依赖 |
| [`test_scheduler.py`](tests/test_scheduler.py) | 真实并发、强制顺序、依赖失败、超时、取消 |
| [`test_spawner.py`](tests/test_spawner.py) | 实例生命周期、工具授权、`max_agents`、`max_depth`、工具调用预算 |
| [`test_tools.py`](tests/test_tools.py) | 沙箱逃逸、权限拒绝、被拒工具、记忆提案 |
| [`test_context.py`](tests/test_context.py) | 上下文隔离、不可信包裹、截断、发现注入 |
| [`test_reviewer.py`](tests/test_reviewer.py) | 结论合并、安全阻断、评审员失败、聚合 |
| [`test_memory.py`](tests/test_memory.py) | 检索契约、“没有可靠来源”、晋升门控、草稿本作用域 |
| [`test_orchestrator.py`](tests/test_orchestrator.py) | 端到端运行、并行、评审循环、失败处理、预算、取消 |
| [`test_agent_map.py`](tests/test_agent_map.py) | 地图形态、层级、元数据、纯投影、失败可见性 |
| [`test_providers.py`](tests/test_providers.py) | 提供方解析、预检、Anthropic 与 OpenAI 线格式、JSON 提取 |
| [`test_config.py`](tests/test_config.py) | 根目录发现、限制校验、预算计数器、配置文件 |

---

## 扩展它

- **新增智能体** —— 写 Markdown 规格。别的都不用做。
- **新增能力** —— 在 `TAXONOMY` 中加一条（[`capabilities.py`](ai_native_os/registry/capabilities.py)）。
- **新增提供方** —— 实现 `Provider.complete`，调用 `register_provider`。
- **新增工具** —— 定义一个 `Tool`，把它加入 `BUILTIN_TOOLS`，通过 `default_tools` 授权。
- **分布式运行** —— `DAGScheduler` 是唯一假定本地执行的组件。把它的
  `execute` 可调用对象替换为队列生产者，就是接入 worker 与分布式运行的接缝。

关于实现前对已有内容的调研，以及运行时为何是这个形态，参见
[docs/architecture-assessment.md](docs/architecture-assessment.md)。
