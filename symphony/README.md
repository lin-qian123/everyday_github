# Symphony

## 项目定位
- 项目地址：<https://github.com/openai/symphony>
- 一句话：把项目管理看板（如 Linear）变成 AI 编码代理的“任务控制平面”，把每个任务自动拆成隔离运行的实现流程。
- 适合人群：已经有较完善测试与 CI 的工程团队，希望从“盯着 AI 写代码”升级为“管理任务结果”。

## 为什么值得关注（2026-05）
- 在 GitHub 趋势与 AI 编码工作流讨论中热度高，核心点不是“再造一个代理”，而是“编排多个代理持续完成看板任务”。
- 官方同时提供：
  - `SPEC.md`（语言无关规范）
  - `elixir/`（实验参考实现）
- 这让团队可先按规范实现自己的版本，再按安全要求收紧权限模型。

## 快速用法

## 1. 以规范驱动自建（推荐生产）
1. 阅读规范：<https://github.com/openai/symphony/blob/main/SPEC.md>
2. 明确最小闭环：任务轮询 -> 工作区隔离 -> 代理执行 -> 产出回传（PR/CI/评审）
3. 将你们团队策略写进仓库（如 `WORKFLOW.md`），版本化审批与回滚策略
4. 从单仓库、单队列开始，再扩展并发

## 2. 运行参考实现（适合评估）
1. 按说明准备环境：<https://github.com/openai/symphony/blob/main/elixir/README.md>
2. 配置任务源（Linear）和代理运行参数
3. 在测试仓库演练“完整任务生命周期”（领取、执行、提交、终止）

## 工作原理（核心机制）
1. **持续轮询任务系统**：定期读取可执行 issue。
2. **按任务创建隔离工作区**：每个 issue 独立目录/上下文，降低串扰。
3. **启动代理会话执行任务**：代理在隔离区内完成编码、测试、提交。
4. **策略化控制与观测**：通过仓库内工作流文件定义提示词、权限、并发、退出条件。
5. **状态回写与清理**：任务进入 Done/Closed/Cancelled 等终态后停止会话并回收工作区。

## 价值与边界
- 价值：
  - 把“人工盯执行”变成“系统化运营任务”
  - 提升多任务并发能力
  - 降低上下文切换成本
- 边界：
  - 官方明确属于工程预览，默认高信任前提
  - 对测试覆盖、CI 稳定性、权限隔离要求高
  - 若仓库缺少自动化护栏，容易放大错误提交风险

## 落地建议
- 先做三层护栏：
  - `代码层`：lint/test/typecheck 必过
  - `流程层`：PR 模板 + 必要评审 + 分支保护
  - `权限层`：最小权限 token、敏感命令白名单
- 指标先行：
  - 任务 lead time
  - 单任务返工率
  - 自动提交通过率
- 先在低风险仓库试运行 1~2 周，再推广主仓。

## 补充资料
- OpenAI 说明文：<https://openai.com/index/open-source-codex-orchestration-symphony/>
- 仓库 README：<https://github.com/openai/symphony#readme>
- 规范文档：<https://github.com/openai/symphony/blob/main/SPEC.md>
- 参考实现：<https://github.com/openai/symphony/blob/main/elixir/README.md>
