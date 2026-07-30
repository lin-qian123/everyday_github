# LiteCoder

## 定位

`LiteCoder` 是 Python 实现的终端优先 coding agent：提供持久会话、token 上下文管理、项目 Markdown memory、任务/子 agent 协作、MCP、hook、权限确认与 JSONL trace，并可连接 Anthropic、OpenAI 及兼容接口。

截至 2026-07-31，GitHub API 快照显示仓库创建于 2026-07-30，约 8 stars、1 fork，MIT 许可证。功能来自项目 README，仍应视作早期实现而非经过独立安全审计的生产平台。

## 用法

要求 Python 3.11+ 和受支持 provider 的 API key。安装后复制示例配置，先只允许读取操作再逐步开放写入和外部副作用。

```bash
git clone https://github.com/ikooky/litecoder.git
cd litecoder
python -m pip install ".[providers,mcp]"
cp config.example.toml ~/.litecoder/config.toml
litecoder
```

可用 `litecoder run "..."` 执行单次任务，或以 `litecoder resume <session-id>` 恢复会话；使用前审阅 provider URL、模型名和密钥存储方式。

## 原理

它把 agent loop 周围的状态拆为 sessions 数据库、项目级 memory、任务状态、邮箱、审计日志与 traces。权限服务区分安全读取、工作区变更和外部操作；长会话由 token 预算及 compact 机制控制。

## 价值

- 为终端 agent 提供会话恢复、可读项目记忆和协作/隔离 worktree 的组合能力。
- 将 MCP、hook、权限与 trace 暴露为可配置的工程表面，便于在小团队中审计试用。

## 风险边界

- API key、第三方兼容端点、MCP server 和 hook 都是供应链及数据外发边界；红脱敏不等于密钥永不泄漏。
- 自动 compact 或持久 memory 可能丢失重要上下文或保留敏感资料；不可将其当成完整证据库。
- 多 agent 与 worktree 不会自动解决合并冲突、错误授权或错误测试结论。

## 补充建议

在隔离仓库、最小权限和测试 API key 下运行，验证 trace、拒绝路径、删除/导出及恢复语义。对外部 MCP 做 allowlist，并以 CI 和人工 code review 作为写入后的独立验收。

## 参考资料

- GitHub：<https://github.com/ikooky/litecoder>
- GitHub API 快照：<https://api.github.com/repos/ikooky/litecoder>
- 中文 README：<https://github.com/ikooky/litecoder/blob/master/README.zh-CN.md>
