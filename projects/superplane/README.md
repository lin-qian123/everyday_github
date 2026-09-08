<!-- markdownlint-disable MD013 MD034 -->

# superplane（superplanehq/superplane）

> 记录日期：2026-09-09（Asia/Shanghai）。本页依据上游 README、官网、文档、release、LICENSE 与 GitHub REST API 做静态整理；本轮未部署 SuperPlane、未连接 Git/CI/云/事故系统，也未验证其自动选单、PR 质量、成本或营销指标。

## 定位

`superplane` 将自己定位为面向 one-shot routine engineering 的开源 AI software factory：持续分析 backlog，把高置信任务交给 coding agents，协调 source control、CI、review、approval 与 feedback，并将结果交付为可审阅 PR。仓库同时保留通用 workflow / Canvas、integration 和 runner 基础设施。

2026-09-09 的 GitHub 官方 Go Trending 抓取显示约 `+244 stars today`；REST API 快照为 `6,308 stars / 629 forks / 609 open issues`，Apache-2.0；最新 GitHub release 为 `v0.30.0`（2026-07-27）。README 明确标注 beta，不能把首页的 one-shot 与比例数字写成独立复现结果。

## 用法

产品试用入口在官网和文档；贡献者路径从源码仓库开始：

```bash
git clone https://github.com/superplanehq/superplane.git
cd superplane
```

上游要求继续阅读仓库 `AGENTS.md`、`CONTRIBUTING.md` 和 Docker-based contributor setup。本页不补写 README 未提供的一键生产部署命令。评估时应先接测试组织、临时仓库、mock CI 与无生产凭据的 integration。

## 原理

- **Factory**：保存 work orders、automation lines 与团队政策。
- **Work order**：从 backlog intake 到结果记录一项委派任务，关联 PR、note、branch 等 artifact。
- **Line / Automation**：按顺序执行 agent、工具、事件等待或人工 approval；Canvas 负责组合 integration。
- **Run**：持久记录输入、输出、retry、cost 和 execution state，允许失败后续接。
- **自动选单**：上游声称持续判断哪些 backlog issue 具有高置信自动化条件，把歧义和需要判断的工作留给人。
- **广泛连接器**：覆盖 GitHub/GitLab/Bitbucket、CI、云、observability、incident、工单与消息系统。

## 价值

- 将零散的 coding-agent 会话提升为可观察、可重试、可审批的工程流水线。
- Work order / run / artifact 模型为“为何运行、运行了什么、失败在哪”提供较完整的运营记录。
- 把 CI、review 和 approval 放入流程，可在 agent 输出与合并之间增加确定性检查。
- 开源 engine 与多模型 / on-prem 选择有利于按数据、成本和供应商约束做部署取舍。

## 风险边界

- 官网展示的“30% backlog”“90%+ ready for approval”“4x faster”等是上游营销指标，本页没有样本定义、对照组或原始数据，不能当通用产能结论。
- Beta、快速演进和 609 个 open issues 表明生产 adoption 需要版本固定、迁移、备份和升级演练。
- Source control、CI、cloud、incident、ticket 与 messaging connector 构成高权限组合；一个被污染的 issue/prompt 可能跨系统触发动作。
- “高置信任务”需要可解释的 qualification、误选率和拒绝策略；语言模型或启发式分数不能替代 owner 对影响范围的判断。
- Retry / resume 若没有幂等键、外部状态 readback 与 compensating action，可能重复创建 branch、PR、部署、通知或工单。
- PR 可审阅和 CI 通过不证明需求正确、安全、性能或运维后果可接受，合并与发布仍需外部保护规则。

## 补充建议

- 从文档、依赖升级、确定性 lint 修复等低后果 backlog 建 golden set，记录 qualification precision、一次通过率、人工返工、成本和 cycle time。
- 每个 integration 使用专用 service account、最小 scope、短期 token 和环境 allowlist；生产 deploy、合并、删除、事故状态变更必须有人审批。
- 对 retry、runner crash、网络分区、重复 webhook、过期 branch 与 CI 假阳性做 failure injection，验证幂等和恢复。
- 将官网比例数字视为待复现假设；采用前用自己的仓库与人类 baseline 重新定义并测量。

## 参考资料

- GitHub 仓库：https://github.com/superplanehq/superplane
- GitHub REST API：https://api.github.com/repos/superplanehq/superplane
- 官方网站：https://superplane.com/
- 文档：https://docs.superplane.com/
- `v0.30.0` release：https://github.com/superplanehq/superplane/releases/tag/v0.30.0
- 官方 X 账号：https://x.com/superplanehq
- LICENSE：https://github.com/superplanehq/superplane/blob/main/LICENSE
