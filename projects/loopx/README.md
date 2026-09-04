<!-- markdownlint-disable MD013 -->

# loopx（huangruiteng/loopx）

> 记录日期：2026-09-05（Asia/Shanghai）。本页依据上游 README、文档、release 与 GitHub API 做静态整理；未在本机安装、连接 agent 或运行长时程任务。

## 定位

`LoopX` 是运行在 Codex、Claude Code、Cursor 等 agent harness 之上的本地优先长时程控制平面。它不替换模型或 harness，而是把 objective、gate、todo、scope、evidence、quota、handoff 与恢复状态放到一个持久层，让跨天任务能按有界 turn 继续。

2026-09-05 的 GitHub 官方 Python Trending 快照显示约 `+82 stars today`；REST API 快照为 `5,606 stars / 501 forks / 60 open issues`，许可证为 Apache-2.0。最新 release 是 `dsh-loopx-plugin-v0.1.1-beta.4`（2026-09-03），名称本身也表明其中至少包含 beta 组件。

## 用法

上游给出的 PyPI 路径为：

```bash
python -m pip install --upgrade loopx
loopx workflow-skills --install
loopx doctor
```

然后在目标项目中建立或接入 goal；首次评估应在无敏感数据的副本仓库中执行，并检查 `.loopx/`、`.codex/goals/`、`.local/` 是否按上游建议忽略。`loopx dashboard` 提供浏览器 / PWA 工作区；原生 Tauri shell 是实验路径，不应与控制状态本身混为一谈。

## 原理

- **持久 state kernel**：以 objective、todo、gate、evidence、quota 和调度状态作为可恢复事实源。
- **有界 continuation**：每次只让外部 agent 执行一个受范围限制的工作片段，再写回证据和下一步。
- **能力 / provider / extension 分层**：能力定义稳定结果契约，provider 访问外部系统，extension 管安装、启用、升级、禁用和回滚生命周期。
- **人类闸门**：当发布、危险权限、私密数据或最终所有权需要判断时，状态机应停在明确 gate。
- **跨 harness 交接**：不同 agent 是对等执行者，通过 claim、lease、capability 和 handoff 继续同一目标。
- **可视化投影**：Dashboard / Kanban 是状态投影，LoopX state 才是上游定义的权威来源。

## 价值

- 把“聊天记住了什么”提升为可检查的目标、范围、证据和接续状态。
- 适合多日工程、研究、benchmark、PR / issue 循环和定时 monitor，而不把整个任务塞进一次会话。
- quota、gate、receipt 和 handoff 让人更容易看清 agent 为什么继续、何时应停、证据是否过期。
- provider-neutral 设计减少对单一模型或单一 coding-agent 宿主的绑定。

## 风险边界

- LoopX 不是 OS sandbox，也不是自主生产控制器；真正的文件、网络、凭据和发布权限仍由底层 harness / 系统决定。
- 上游的 `200+ hours` 表示 elapsed wall-clock project lifetime，不是连续模型执行、无人值守生产或独立复现实验。
- 状态、gate 和 receipt 只有在 provider 正确写回、证据可读且验证器可靠时才有意义。
- 调度循环可能持续消耗额度或重复无价值工作；必须配置 quota、停止条件、幂等与异常升级。
- 本地优先不等于数据永不外发；模型 provider、搜索、Git、遥测和扩展仍可能联网。
- beta plugin、多个宿主适配器和长期状态迁移增加升级/回滚复杂度。

## 补充建议

- 用一个可丢弃仓库设计“成功、需人工、证据过期、provider 失败、预算耗尽、冲突 claim”六类测试。
- 每个 goal 固定 owner、scope、可接受证据、stop condition、预算和危险动作清单。
- 抽样比对 Dashboard、状态文件、Git 历史与真实外部系统，确认投影没有漂移。
- 将用户报告、上游 showcase、可重复 demo 和本地实测分开标注证据等级。
- 升级前导出状态并演练 rollback；不要让实验性桌面 shell 成为唯一恢复入口。

## 参考资料

- [GitHub 仓库](https://github.com/huangruiteng/loopx)
- [GitHub REST API](https://api.github.com/repos/huangruiteng/loopx)
- [官方文档](https://huangruiteng.github.io/loopx/docs/)
- [Getting Started](https://huangruiteng.github.io/loopx/docs/guides/getting-started/)
- [Releases](https://github.com/huangruiteng/loopx/releases)
- [公开/私有边界说明](https://github.com/huangruiteng/loopx/blob/main/docs/public-private-boundary.md)
