# memsearch

## 项目定位
`memsearch` 是一套面向 AI coding agent 的持久化记忆层，目标不是再造一个聊天应用，而是让 `Claude Code`、`Codex CLI`、`OpenClaw`、`OpenCode` 等不同 agent 共享一套可检索、可编辑、可迁移的长期记忆。

- GitHub：https://github.com/zilliztech/memsearch
- 文档：https://zilliztech.github.io/memsearch/
- 适用人群：希望给编码 agent 增加跨会话记忆、跨工具上下文复用和可审计记忆文件的个人开发者、AI 工具链团队、agent 平台团队。

## 用法

官方 README 已经把接入拆成“按 agent 安装插件”的路线：

1. 克隆仓库或按对应平台文档安装插件。
2. 为当前使用的 agent 启用 `memsearch`。
3. 正常继续对话或执行任务，让插件自动捕获会话摘要与记忆。
4. 通过 `/memory-recall` 或自然语言问题触发历史检索。

从仓库主页公开的安装示例看，它已经覆盖多条主流链路：

- `Claude Code`：通过 plugin marketplace 安装。
- `Codex CLI`：运行 `bash memsearch/plugins/codex/scripts/install.sh`。
- `OpenClaw`：通过插件安装并打开 conversation access / prompt injection。
- `OpenCode`：在配置文件里声明插件。

它的默认工作方式是“先把记忆写成 Markdown，再用向量索引和搜索层增强检索”，而不是只把数据锁进某个数据库里。

## 原理

`memsearch` 的设计有几个很清晰的工程判断：

- Markdown 是事实源：记忆最终落在 `.md` 文件里，便于人类阅读、手工修正和版本控制。
- Milvus 是派生索引：向量库不是唯一真相，而是可重建的检索加速层。
- 混合检索：官方明确写了 dense vector、BM25 sparse 和 RRF reranking 的组合。
- 分层召回：公开说明采用 `search -> expand -> transcript` 的 3 层 recall。
- 实时同步：通过文件监听和内容哈希跳过未变化内容，降低重复索引成本。

这让它和“单纯往会话里塞摘要”的记忆插件不一样。它更像一个独立的记忆子系统，agent 只是上层入口。

## 价值

- 对重度使用多个 coding agent 的用户，最大的价值是跨工具共享上下文，而不是每个 agent 各自重复学习。
- 对工程团队，Markdown 记忆文件更容易纳入现有仓库、审计、备份和差异检查流程。
- 对平台团队，它提供了从个人使用到团队部署的升级空间，既能本地零配置，也能接托管向量服务。

## 风险边界

- 记忆层能提升连续协作体验，但不能自动保证“记住的东西就是对的”，错误记忆仍需要治理。
- 引入长期记忆后，敏感信息边界、过期信息清理、记忆污染和召回误触发都会变成真实工程问题。
- 它依赖额外插件、索引与嵌入配置，轻量场景下未必值得立刻接入完整栈。

## 补充建议

- 真正值得先验证的是：你的 agent 是否真的需要跨会话、跨工具共享上下文，而不是先被“长期记忆”叙事吸引。
- 如果准备长期使用，优先审查 `.memsearch/memory/` 的落盘内容、忽略规则、备份策略和敏感信息处理。
- 从趋势看，`memsearch` 代表的是“把 agent 记忆做成独立基础设施”的路线，这条线和近期高热的 memory 项目一起，说明 agent 生态正在从推理能力卷到状态治理能力。

## 参考资料

- 仓库主页：https://github.com/zilliztech/memsearch
- 官方文档：https://zilliztech.github.io/memsearch/
- GitHub 仓库 README（Codex/Claude/OpenClaw/OpenCode 安装段落）
- GitHub Trending：https://github.com/trending
