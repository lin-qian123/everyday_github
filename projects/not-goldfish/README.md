# not-goldfish

## 定位

`not-goldfish` 是 Rust 实现的 agent 记忆与上下文卫生层，以 SQLite WAL/FTS5 维护检索、缓存与本地 Web UI。

截至 2026-07-23，GitHub API 显示其创建于 2026-07-21，约 2 stars；属早期开发者信号。

## 用法

按仓库说明连接 Claude Code、Codex、Gemini CLI 或 Kimi，并将记忆库放在可备份、受访问控制的位置。

## 原理

以 SQLite 作为状态真源，叠加混合搜索和知识图谱，试图在跨会话压缩时保留可恢复的上下文线索。

## 价值

- 面向多宿主 agent 的本地记忆互操作值得跟踪。
- WAL/FTS5 使存储、检索与备份更接近常规工程实践。

## 风险边界

- 记忆库可能积累代码、提示和敏感信息。
- “无损”压缩应以回放评测而不是宣传语验证。

## 补充建议

先测量检索命中、错误召回和上下文泄露，再接入生产任务。

## 参考资料

- GitHub：<https://github.com/vmelooo/not-goldfish>
