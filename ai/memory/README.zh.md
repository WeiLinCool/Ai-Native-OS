# 记忆

[English](README.md) | 中文

记忆是持久化、结构化的知识，让 AI-Native OS 随时间不断改进，而不是每个会话都从头重新学习。[记忆管理器](../orchestration/memory-manager.md)和[知识管理器](../orchestration/knowledge-manager.md)负责读写；记忆**未经校验绝不修改**。

## 记忆类型

| 存储 | 范围 | 文件 |
|---|---|---|
| 会话 | 仅当前对话 | [session-memory.md](session-memory.md) |
| 项目 | 单个项目的架构、需求、决策 | [project-memory.md](project-memory.md) |
| 公司 | 标准、原则、约定、政策 | [company-memory.md](company-memory.md) |
| 部门 | 部门的运营知识 | [department-memory.md](department-memory.md) |
| 用户 | 偏好、目标、约束、既往工作 | [user-memory.md](user-memory.md) |
| 客户 | 客户上下文与历史 | [customer-memory.md](customer-memory.md) |
| 研究 | 研究发现、基准、来源 | [research-memory.md](research-memory.md) |
| 架构 | 系统设计及其理由 | [architecture-memory.md](architecture-memory.md) |
| 决策 | 决策及其作出原因 | [decision-memory.md](decision-memory.md) |
| 会议 | 会议决策与行动项 | [meeting-memory.md](meeting-memory.md) |
| 文档 | 规范文档索引 | [documentation-memory.md](documentation-memory.md) |
| 经验教训 | 什么奏效，什么失败 | [lessons-learned.md](lessons-learned.md) |
| 提示词 | 可复用、带版本的提示词 | [prompt-memory.md](prompt-memory.md) |
| 知识库 | 概念、算法、参考资料 | [knowledge-base.md](knowledge-base.md) |

## 横切机制

| 关注点 | 文件 |
|---|---|
| 上下文如何被组装与限定 | [context-management.md](context-management.md) |
| 记忆如何被检索 | [retrieval.md](retrieval.md) |
| 更新、保留与版本化 | [retention-and-versioning.md](retention-and-versioning.md) |

## 原则

- **只做经过校验的写入** —— 不存在凭空捏造的记忆；每个事实都有来源和时间戳。
- **正确的记忆，正确的范围** —— 会话事实未经提升绝不泄漏进公司记忆。
- **可检索** —— 一切都带标签，供[检索](retrieval.md)使用。
- **版本化** —— 记忆的变更可追溯、可回滚。
