# 手册

[English](README.md) | 中文

面向反复出现情况的全公司运营手册。事故与可靠性手册放在执行它们的部门里，即
[post-launch/playbooks/](../departments/post-launch/playbooks/)。

## 跨部门手册

| 手册 | 场景 |
|---|---|
| [brainstorming-ideas.md](brainstorming-ideas.md) | 生成公司/产品创意池（阶段 0） |
| [validating-an-idea.md](validating-an-idea.md) | 在构建之前低成本验证创意 |
| [building-an-mvp.md](building-an-mvp.md) | 界定并交付第一个版本 |
| [launching-a-product.md](launching-a-product.md) | 把产品从就绪带到发布 |
| [running-a-sprint.md](running-a-sprint.md) | 反复执行的构建节奏 |
| [hiring-an-engineer.md](hiring-an-engineer.md) | 严谨地补充工程力量 |
| [pitching-to-investors.md](pitching-to-investors.md) | 向投资人路演融资 |
| [fundraising.md](fundraising.md) | 融资（或决定不融资） |
| [handling-a-customer-complaint.md](handling-a-customer-complaint.md) | 客户不满意 |
| [scaling-a-team.md](scaling-a-team.md) | 在扩大团队规模的同时不丢掉有效的做法 |
| [international-expansion.md](international-expansion.md) | 进入一个新的国家 |

## 运营手册（放在各自部门中）

| 场景 | 手册 |
|---|---|
| 处理事故 / 宕机 | [post-launch/playbooks/critical-outage.md](../departments/post-launch/playbooks/critical-outage.md) |
| 安全事件 | [post-launch/playbooks/security-breach.md](../departments/post-launch/playbooks/security-breach.md) |
| 紧急热修复 / 回滚 | [post-launch/playbooks/emergency-hotfix.md](../departments/post-launch/playbooks/emergency-hotfix.md) · [rollback.md](../departments/post-launch/playbooks/rollback.md) |
| 工程时间上的情况（CI 失败、不稳定测试、大规模重构） | [engineering/playbooks.md](../departments/engineering/playbooks.md) |
| 产品上的情况（没有 PMF、功能无人采用） | [product/playbooks.md](../departments/product/playbooks.md) |

## 新增一份手册

每份手册都要写明**触发条件**（“何时使用”）、编号的**步骤**（它们链接到负责该工作的部门），
以及**成功标准**和一个**升级条件**。部门特有的情况
应放进该部门的 `playbooks.md`。
