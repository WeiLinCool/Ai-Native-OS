# 模板

[English](README.md) | 中文

AI-Native OS 中各处复用的脚手架。

| 模板 | 用途 |
|---|---|
| [department-template/](department-template/) | 新[部门](../../STRUCTURE.md#standard-department-structure)的标准结构 —— 复制整个文件夹。 |
| [documents/](documents/) | 全公司文档模板（PRD、RFC、ADR、事故报告……）。 |

智能体规格模板与智能体放在一起：[agents/agent-template.md](../../ai/agents/agent-template.md)。

## 如何使用

- **新增部门？** 把 `department-template/` 复制为 `<department>/` 并填写。
- **新增文档？** 把 `documents/` 中对应的文件复制到相关部门的 `templates/` 或工作目录。
- **新增智能体？** 复制 `agents/agent-template.md`。

绝不要让复制来的占位文本留在完成的文档里 —— 参见 [CONTRIBUTING.md](../../CONTRIBUTING.md)。
