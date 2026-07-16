<!-- markdownlint-disable MD013 -->

# deja-vu

## 定位

`vshulcz/deja-vu` 是一个面向 coding agents 的本地 session memory layer。它索引 Claude Code、Codex、opencode、aider、Gemini CLI、Cursor、Antigravity、Grok Build 等工具已经写到本机的会话日志，并提供搜索、MCP recall、自动上下文注入、脱敏分享和同步。

## 用法

README 提供安装脚本、Go install、npm 和 Homebrew 方式。安装后可直接用 `deja "query"` 搜索历史会话，或执行 `deja install --all` / `deja install --auto` 接入多个 agent 的 MCP recall 和 session-start auto-recall。

## 原理

deja-vu 不要求额外模型或后台服务，而是读取本地 agent transcript，建立可搜索索引，并在索引时做 API key、JWT、私钥等敏感内容脱敏。MCP server 暴露 recall 能力，让后续 agent 会话能找回过去修过的问题、设计决策和调试过程。

## 价值

- 把“已经花 token 解决过的问题”转成可复用记忆，降低重复调试成本。
- 跨 harness 搜索是关键价值：同一个问题可能曾在 Codex 里解决，却在 Claude Code 中需要复用。
- 本地优先、零依赖和显式分享适合个人工程工作流。
- 对团队交接也有价值，可以输出脱敏 session digest。

## 风险边界

- 本地会话日志可能包含商业代码、路径、任务描述和用户意图，即使脱敏也要谨慎分享。
- 自动注入历史上下文可能带来 stale decision 或错误经验复用。
- 不同 agent 日志格式更新后，索引准确性需要继续验证。
- MCP recall 如果接入多个 agent，应明确哪些项目、哪些历史可以被读取。

## 补充建议

- 先只启用手动搜索，确认索引与脱敏质量后再启用 auto-recall。
- 对过期架构决策建立删除或标记机制，避免错误记忆长期污染上下文。
- 与 `paxm`、`personal-model` 区分：deja-vu 更偏从已有 session log 里找工程记忆。

## 参考资料

- GitHub: <https://github.com/vshulcz/deja-vu>
- Website: <https://vshulcz.github.io/deja-vu/>
