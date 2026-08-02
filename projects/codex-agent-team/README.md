# codex-agent-team

## 定位

`codex-agent-team` 是面向 Codex 的第三方 skill 和确定性校验脚本，用来基于任务权限、风险和证据选择单 agent、临时团队或持续团队；它不是独立多 agent runtime。截至 2026-08-03 的 GitHub API 快照：项目创建于 2026-08-02，约 14 stars、0 forks，Apache-2.0。

## 用法

README 给出 Windows PowerShell 安装脚本，也允许在其他系统将 `skill/agent-team/` 放入 Codex skills 目录。可先使用 `preview` 只生成拓扑建议；只有用户明确授权后才要求临时团队完成任务。开发者可运行 Python unittest、结构校验与同步验证。

## 原理

skill 将五个常被混合的决策拆开：协作拓扑、唤醒机制、收敛方式、验证方式与人工闸门。可选证据循环会冻结验收命令和资产、使用干净 linked worktree，并让确定性检查优先于“多叫几个 agent”。

## 价值

- 将“是否并行”从默认偏好改为可解释、最小权限的决策。
- 对发布、部署、删除、付费和权限等后果性操作保留人类关口。

## 风险边界

- skill 不能提供操作系统沙箱，也不会自动令 agent 的代码、安全性或验收结论可信。
- 安装脚本会写入用户级 skill 目录；应在审阅来源、版本和文件 hash 后执行。
- 多 agent 协作提高并行度也增加上下文分叉、冲突和成本；无清晰验收标准时不应以团队数量代替验证。

## 补充建议

默认从单 agent + 明确验收命令开始；仅当任务可拆分、权限边界明确且存在独立残余风险时再启用团队。将预览结果、授权文本和最终证据随任务保存。

## 参考资料

- GitHub：<https://github.com/youngfor-shoot/codex-agent-team>
- 项目安全说明：<https://github.com/youngfor-shoot/codex-agent-team/blob/main/SECURITY.md>
- GitHub API 快照：<https://api.github.com/repos/youngfor-shoot/codex-agent-team>
