# dao-code

## 1. 项目定位

`dao-code` 是一个 TypeScript 终端 coding agent，围绕 DeepSeek V4 的长上下文、低价格和 prefix cache 做工程优化。它强调中文可用性、低成本长任务、Claude Code 配置兼容、Skills / MCP / Hooks 支持，以及跨会话记忆和自我纠偏。

它适合关注中国大陆可访问性、DeepSeek 生态、成本敏感型 coding agent 和长上下文缓存工程的开发者。

## 2. 基本用法

官方 README 将命令名定义为 `dao`，项目主页指向 npm 包 `dao-code`。典型使用路径是安装 CLI、配置 DeepSeek 兼容模型通道，然后在终端中让 agent 读取代码、修改文件、运行命令并通过 approval gate 执行敏感操作。

项目还提供 `/cost`、`/audit cache`、`/restore`、`/rewind`、`/dod` 等命令，用于观察成本、检查缓存、恢复 checkpoint 和定义完成标准。

## 3. 核心原理

`dao-code` 的核心思路是把 agent 运行成本和长任务稳定性纳入 harness 设计：

- 使用 byte-stable system prefix，让 DeepSeek prefix cache 命中率持续提高。
- 将记忆、反思和自我纠偏设计为复用主上下文缓存的 forks。
- 用 session log、shadow-git checkpoint、todo 持久化和 crash recovery 支撑长任务。
- 使用 challenger / refocuser / reply-challenger 处理卡住、漂移和重复问题。
- 兼容 Skills、MCP、Hooks 和 Claude Code 风格配置，降低迁移成本。

## 4. 工程价值

`dao-code` 的价值在于把“模型便宜”进一步工程化为“agent 长任务可承受”。如果 prefix cache、forked reflection 和自验证记忆能稳定工作，低成本模型就可以承担更多反复阅读、修改、测试、复盘的开发循环。

对本仓库的长期跟踪而言，它与 `MiMo-Code`、`qwen-code`、`codex`、`claude-code` 构成新的终端 agent 对照组：模型厂商和社区项目都在把 long-context、memory、checkpoint、subagent 和成本观测做进 CLI。

## 5. 风险边界

- 项目强绑定 DeepSeek V4 的价格、上下文和缓存特性，迁移到其他模型时优势可能下降。
- README 中的成本和 benchmark 结论需要结合官方价格、任务集和日志复核，不能直接外推到所有代码库。
- 终端 agent 具备命令执行和文件修改能力，必须控制 approval、密钥读取、网络访问和 Git 操作。
- 自我纠偏和记忆验证能降低漂移，但不能替代测试、代码审查和人工验收。

## 6. 补充建议

- 先用只读分析和小型 bugfix 验证 `/cost` 与缓存命中率，再交给长任务。
- 对团队项目，把可执行命令、MCP server、skills 和 hooks 列入明确白名单。
- 将 Dao Code 的记忆文件与项目正式文档分开管理，避免 agent 私有记忆污染公开 README。
- 后续重点观察其 DeepSeek V4 适配是否能在真实复杂仓库中持续保持高缓存命中和低漂移。

## 7. 参考资料

- GitHub 仓库：https://github.com/tigicion/dao-code
- npm 包：https://www.npmjs.com/package/dao-code
- GitHub API 元数据：仓库创建于 `2026-06-08`，抓取时约 `964 stars / 21 forks`
