# ai-memory

- 仓库：[akitaonrails/ai-memory](https://github.com/akitaonrails/ai-memory)
- 快照：2026-08-18 抓取；GitHub REST API 显示约 2.0k stars、192 forks、6 个开放 issue，MIT；创建于 2026-05-21，数值会变化。
- 分类：记忆层与个人 AI 基础设施

## 定位

`ai-memory` 是为 coding agent 准备的长期记忆与跨厂商交接工具。它把经清理的生命周期事件整理为 Git 版本化 Markdown wiki，并通过 MCP、hook 和可选的托管 workstream，让 Claude Code、Codex、OpenCode 等会话在同一仓库中接续上下文。

## 用法

优先从项目的 macOS/Linux 安装文档取得受支持的发布包；再在一个无敏感数据的测试仓库中配置客户端。例如，上游 README 提供 `install-mcp`、`install-hooks`、`bootstrap`、`status`、`finalize-session` 等子命令，并说明 Codex 没有真正的自动 session-end hook，需要在需要交接时显式执行 `ai-memory finalize-session`。

建议先只启用只读查询与一个测试客户端，创建两段可删除的模拟任务，检查写入内容、交接摘要和跨 worktree 的项目身份是否符合预期；确认后才接入真实仓库和其他 agent。

## 原理

上游将 hook 捕获的 prompt、工具生命周期和会话边界观察做有界、脱敏的采集，再在 session 结束或手动收尾时编译为 wiki 页面。检索结合 FTS5、实体匹配、图邻居和可选向量召回；项目以 workspace/project 标识隔离，wiki 本身可由 Git 保存版本。MCP 层负责把检索到的 handoff 或记忆提供给宿主 agent。

## 价值

- 将跨会话“重新解释架构、失败路径和待办”的成本变为可审阅的交接材料。
- Markdown/Git 便于人工查看、备份、差异审阅与迁移，不要求把全部上下文交给封闭记忆服务。
- 支持多个 coding harness 时，可把项目级知识与单次 agent 会话区分开来。

## 风险边界

- hook 捕获与“已清理”不等于绝对不会记录密钥、个人数据、客户代码或错误上下文；须先检查 capture exclusions、保留期限、权限和备份位置。
- 记忆召回是历史证据，不是当前代码事实；上游也要求把检索结果与当前 checkout、测试和运行结果交叉核验。
- 自动注入的 handoff 可能携带过期决定或提示注入内容；跨用户/跨项目部署还需要独立的身份认证、访问控制与审计。MIT 许可不替代组织的数据治理义务。

## 补充建议

1. 用专门的测试 wiki 和无秘密 fixture 验证捕获范围、检索命中率、删除/恢复和备份演练。
2. 为每个仓库显式配置 ignore path，并把 `.env`、凭据目录、生产导出、个人文件与大体积构建产物排除在采集外。
3. 将 handoff 当作候选上下文；对架构、权限、迁移和部署结论回到当前仓库和实际验证。

## 参考资料

- [项目 README 与架构文档入口](https://github.com/akitaonrails/ai-memory)
- [GitHub REST API 元数据快照](https://api.github.com/repos/akitaonrails/ai-memory)
- [GitHub Trending](https://github.com/trending)
