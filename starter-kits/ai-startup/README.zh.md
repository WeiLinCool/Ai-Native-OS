# AI 初创公司起步套件

[English](README.md) | 中文

一家核心产品是 AI 系统（LLM 应用、智能体产品、ML 服务）的公司。这个套件继承
AI-Native OS 内核，并补充 AI 原生产品公司特别需要的东西。

## 继承内容保持不变

- 完整的[公司身份](../../handbook/company/)、[治理](../../handbook/governance/)与[内核](../../ai/orchestration/)（[记忆](../../ai/memory/)、[智能体](../../ai/agents/)）。
- [engineering](../../handbook/departments/engineering/)、[product](../../handbook/departments/product/) 和 [post-launch](../../handbook/departments/post-launch/) 部门，以及其他所有核心部门。
- [SDLC](../../handbook/workflows/sdlc.md)、[standards](../../handbook/standards/)、[templates](../../handbook/templates/) 和 [strategy](../../handbook/departments/strategy/)。

## 它新增和强调什么

| 增量 | 文件 |
|---|---|
| AI 专属智能体（LLM、ML、评估、数据） | [agents.md](agents.md) |
| AI 产品与评估标准 | [standards.md](standards.md) |
| AI 交付生命周期（数据 → 评估 → 部署 → 监控漂移） | [workflows.md](workflows.md) |
| 如何把它搭起来 | [getting-started.md](getting-started.md) |

## 为什么需要这些增量

AI 初创公司的生死取决于**评估、成本与模型可靠性**。AI-Native OS 内核已经把
[AI 当作一门工程学科](../../handbook/departments/ai-engineering/README.md)来对待；这个套件让评估门、
提示词/模型版本化、漂移监控和单次请求成本在日常工作流中成为一等公民。

## 更换这个套件

要构建另一种公司类型（例如 `saas` 或 `robotics`），复制这个目录的结构，并把 AI 专属增量换成
你所在领域的增量 —— 继承模型是完全一样的。
