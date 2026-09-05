<!-- markdownlint-disable MD013 -->

# context-mode（mksglu/context-mode）

> 记录日期：2026-09-06（Asia/Shanghai）。本页依据上游 README、BENCHMARK、源码目录、release、LICENSE 与 GitHub REST API 做静态整理；本轮未安装 npm 包、未接入任何 agent，也未复现 token 节省或会话恢复。

## 定位

`context-mode` 是面向 coding agents 的 MCP server、hooks 与本地索引组合，目标是把大体积工具输出留在 SQLite/索引侧，通过脚本计算、批量执行和检索只把相关片段送回模型上下文。它还记录文件编辑、Git 操作、任务、错误和用户决策，用于 compaction 后恢复会话线索。

2026-09-06 的 GitHub 官方 TypeScript Trending 抓取显示约 `+36 stars today`；REST API 快照为 `20,402 stars / 1,486 forks / 210 open issues`，最新 release 为 `v1.0.169`。API 许可证字段为 `NOASSERTION`，仓库 LICENSE 与 README 标示 Elastic License 2.0（ELv2），不是 MIT/Apache 类宽松许可证。

## 用法

上游为 Claude Code 提供 plugin 路径，也提供仅注册 MCP server 的试用方式：

```bash
claude mcp add context-mode -- npx -y context-mode
```

仅 MCP 方式不会自动安装 hooks 或注入路由规则；完整模式会按宿主配置 SessionStart、PreToolUse、PostToolUse、PreCompact 等 hooks。正式评估前应先运行项目提供的 doctor，审查它将修改的用户级配置、hook 命令与数据目录。

## 原理

- **工具输出隔离**：让 `ctx_execute`、`ctx_batch_execute`、`ctx_fetch_and_index` 等工具在外部处理大文本，只返回计算结果或命中片段。
- **事件索引**：把编辑、Git、任务、错误和决策写入 SQLite，并用 FTS5/BM25 做按需检索。
- **会话生命周期**：上游称不使用 `--continue` 时会删除上一会话数据；实际删除范围、失败行为和备份残留仍须实测。
- **路由约束**：支持 hook 的宿主可自动引导模型优先走 context-mode；仅 MCP 接入则依赖模型主动选择。
- **跨宿主适配**：仓库包含 Claude Code、Codex、Gemini CLI、VS Code Copilot、OpenClaw 等多类配置与插件目录。
- **本地 bundle**：npm/CLI、server bundle、hooks、skills、tests 与 web 页面共同构成分发形态。

## 价值

- 大量日志、网页、issue 和文件分析可先在代码侧聚合，减少原始内容直接占满上下文。
- FTS5 检索提供比整段 compaction 摘要更可定位的会话恢复入口。
- Doctor、stats、purge、insight 等工具让配置、节省量和本地状态有可检查表面。
- 跨宿主复用同一 MCP/索引思路，便于比较不同 coding-agent 客户端的接入效果。

## 风险边界

- 项目所说的 “sandboxed tool output” 是输出处理/存储路径，不是 OS、容器或网络安全沙箱；被调用命令仍拥有宿主授予的权限。
- README 的 `98% reduction`、`100x` 等为上游场景声明；节省 token 不等于任务正确率、成本或延迟必然更好。
- 自动 hooks 会改变模型的工具路由和用户级配置；版本升级、宿主 API 变化或 hook 顺序冲突可能导致漏拦截或功能退化。
- SQLite 索引会集中保存文件名、命令、错误、决策和可能的敏感输出；需要明确目录、权限、加密、保留、purge 与备份边界。
- BM25 命中会遗漏未索引或措辞不同的关键信息；检索片段也可能脱离上下文，不能替代原始证据和测试日志。
- ELv2 限制将该软件的大部分功能作为 hosted/managed service 提供，团队服务化前须按实际部署审查条款。

## 补充建议

- 在无敏感数据的长会话 fixture 中做 A/B：固定模型、任务、上下文上限和工具输出，比较成功率、token、延迟、漏证据与返工。
- 记录安装前后所有 MCP、hooks、AGENTS/CLAUDE 配置和用户目录 diff，并验证卸载与升级回滚。
- 用 canary secrets、超大日志、二进制、注入文本和并发会话测试索引边界，不把 secrets 写入真实 fixture。
- 分别验证 fresh session、continue、compaction、crash、purge、备份恢复和多项目隔离。
- 使用 ELv2 代码提供内部或外部服务前，让法务按服务暴露的“substantial set of features”审查。

## 参考资料

- [GitHub 仓库](https://github.com/mksglu/context-mode)
- [GitHub REST API](https://api.github.com/repos/mksglu/context-mode)
- [v1.0.169 Release](https://github.com/mksglu/context-mode/releases/tag/v1.0.169)
- [README](https://github.com/mksglu/context-mode/blob/main/README.md)
- [BENCHMARK](https://github.com/mksglu/context-mode/blob/main/BENCHMARK.md)
- [Elastic License 2.0](https://github.com/mksglu/context-mode/blob/main/LICENSE)
- [上游 YouTube Demo](https://www.youtube.com/watch?v=QUHrntlfPo4)
