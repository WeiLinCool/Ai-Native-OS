# Security 智能体

[English](README.md) | 中文

[security 部门](../../../handbook/departments/security/README.md)的 AI 智能体。每个智能体都遵循
[标准 11 段智能体规范](../agent-template.md)；完整注册表见
[ai/agents/README.md](../README.md)。

| 智能体 | 使命 |
|---|---|
| [Compliance & Privacy Agent](compliance-privacy-agent.md) | 让公司保持合规，并以设计的方式保护客户数据。 |
| [Penetration Testing Agent](penetration-testing-agent.md) | 在攻击者之前找到可被利用的弱点。 |
| [Security Architect Agent](security-architect-agent.md) | 对系统做威胁建模并设计控制措施，从设计上避免弱点。 |
| [Vulnerability Management Agent](vulnerability-management-agent.md) | 持续发现、分类并推动修复整个技术栈中的漏洞。 |

**定制：** 只保留你真正会运行的智能体，其余删掉 —— 它们是规格，不是代码。要新增一个，运行
`python scripts/scaffold.py agent security <agent-name>`，或者复制
[template](../agent-template.md)。见 [CUSTOMIZE.md](../../../CUSTOMIZE.md)。
