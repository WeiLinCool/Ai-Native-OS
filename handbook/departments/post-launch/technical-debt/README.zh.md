# 技术债

[English](README.md) | 中文

技术债不是道德缺陷 —— 它是在时间压力下做出的有意取舍。不可接受的是**没有记录、没有跟踪、也没有偿还**的技术债。这个文件夹就是让技术债保持可见并不断缩小的体系。

治理规则来自 [上线后标准](../standards.md)：只有当技术债**被记录、被估算、被排定优先级并安排了偿还计划**时才允许存在 —— 而且每个迭代都要分配容量偿还一部分。

## 索引

| 文件 | 用途 |
|---|---|
| [policy.md](policy.md) | 何时允许承担技术债，以及附带条件 |
| [tracking.md](tracking.md) | 技术债如何被记录并保持可见 |
| [prioritization.md](prioritization.md) | 技术债项之间、以及与功能之间如何排序 |
| [repayment-plan.md](repayment-plan.md) | 技术债如何排期与偿还 |
| [review-process.md](review-process.md) | 技术债由谁、如何评审 |
| [metrics.md](metrics.md) | 技术债趋势如何衡量 |

## 谁在运行它

[技术债智能体](../../../../ai/agents/post-launch/technical-debt-agent.md) 负责扫描、记录
并排序技术债；[工程](../../engineering/technical-debt-policy.md) 负责偿还容量；
趋势发布在[维护仪表盘](../dashboards.md)上。
