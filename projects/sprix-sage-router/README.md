# Sprix SAGE Router

- 仓库：[wang2122/sprix-sage-router](https://github.com/wang2122/sprix-sage-router)
- 快照：2026-08-19 抓取；GitHub REST API 显示 153 stars、9 forks、0 个开放 issue，MIT；创建于 2026-08-18，数值会变化。
- 分类：Agent 框架与技能生态

## 定位

`Sprix SAGE Router` 是面向开放 A2A（Agent2Agent）网络的多 agent 路由研究原型。它在任务已开始执行的状态下，比较继续由当前 agent 完成（SELF）、补充协作者（COLLABORATE）和整体交接（HANDOFF）三种路线，并考虑能力、权限、预算、截止时间、上下文转移与任务 DAG。

## 用法

上游将其定位为 Python 3.10+ 的研究预览：克隆后可运行 `python demo.py`，再以 `python -m unittest -v` 和 `python benchmark.py` 检查演示和仿真基准。集成时先把真实 agent 的 Agent Card、权限、报价和任务状态映射为只读候选输入；由系统外部保留人工批准、身份认证、任务传输和撤销控制。

项目当前输出的是路由决策，README 明确说明并不负责实际发送 A2A 任务。因此，不应把 demo 中的 agent 能力、成本或成功率直接用于生产排班或自动委派。

## 原理

SAGE 用约束过滤先排除无权限或不兼容候选，再在 SELF、HANDOFF 与受限规模的协作团队间搜索。它将剩余需求组织为 DAG，估计角色分配、关键路径延迟、成本、风险和上下文转移损耗；完成后把可用的结果、成本和延迟回灌给按需求条件化的信任与出价校准模型。

## 价值

- 将“该不该换人、找谁协作、何时交接”从单一能力排行扩展为可审阅的多约束决策。
- 把任务依赖、成本与截止时间显式留在路由输出中，便于人工检查关键路径和协作开销。
- 为 A2A 的发现/传输层提供一个可替换的决策层原型，而非绑定某一家 agent 服务。

## 风险边界

- 仓库自述为 early-stage research preview；其 benchmark 是外部仿真器上的多 seed 测试，不是生产 trace、真实市场或因果效果证据。
- 能力分数、报价和结果反馈可被虚报、投毒或受选择偏差影响；路由器不是身份认证、沙箱、支付托管或安全策略系统。
- 转交任务可能泄露上下文、凭据或客户数据；即使决策理由可读，也必须有最小权限、内容脱敏、审计、人工批准和可撤销执行边界。

## 补充建议

1. 先用合成任务与固定 agent 集比较 SELF、HANDOFF、协作三种路线的真实成本、延迟、成功率和错误恢复。
2. 将能力、成本和完成反馈视为不可信输入；对签名 Agent Card、预算上限、权限过滤和拒绝服务场景做对抗测试。
3. 在任何自动任务发送之前保留人工批准和回滚路径，并为跨 agent 上下文设置最小化、过期和删除规则。

## 参考资料

- [项目 README、算法与 benchmark 说明](https://github.com/wang2122/sprix-sage-router)
- [GitHub REST API 元数据快照](https://api.github.com/repos/wang2122/sprix-sage-router)
- [Agent2Agent 协议](https://a2a-protocol.org/latest/)
