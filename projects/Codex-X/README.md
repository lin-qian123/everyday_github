# Codex-X

<!-- markdownlint-disable MD013 MD012 -->

## 定位

`Codex-X` 是一个面向 OpenAI Codex 桌面端 / Codex CLI 的跨平台桌面管理器。它用 Tauri、React、TypeScript、Rust 构建，提供 Provider 切换、TOML/Auth 可视化管理、会话 Provider Sync、Skills/MCP 管理等功能。

需要特别注意的是，项目 README 也强调“提示词注入”和所谓 unrestricted 模板。这使它既是 Codex 本地配置可视化工具，也是一个需要谨慎看待的安全边界研究样本。

## 用法

项目面向桌面用户，核心操作包括：

- 管理 `~/.codex/config.toml`。
- 管理 `~/.codex/auth.json`。
- 切换官方 OpenAI 与第三方 OpenAI-compatible Provider。
- 查看本地 SQLite / rollout JSONL 会话信息。
- 管理 Codex skills 与 MCP 配置。
- 同步或修复历史 thread 的 Provider 元数据。

从仓库结构看，项目包含 `apps/desktop`、`codex-instruct.py`、文档、脚本和示例，适合有 Codex 本地配置经验的用户评估。

## 原理

Codex-X 把 Codex 本地配置目录中的文本文件和状态文件包装成桌面 UI：

- Rust/Tauri 负责本地文件访问和桌面壳。
- React/TypeScript 负责配置界面、Provider 表单和会话展示。
- SQLite / JSONL 读取用于理解历史会话和 Provider 元数据。
- Skills/MCP 管理页读取当前可用能力，并提供启用、禁用、导入等操作。

它本质上是“Codex 本地状态控制面”，把原本需要手动编辑的文件变成可视化操作。

## 价值

- 对 Codex 重度用户：降低配置 provider、auth、TOML、MCP 和 skills 的操作门槛。
- 对 agent 桌面生态：说明本地 agent 配置正在从 CLI 文本文件走向 GUI 控制面。
- 对安全研究：提供了观察本地配置、提示词、Provider 和会话元数据如何被第三方工具修改的具体样本。
- 对工具开发：Tauri + 本地配置目录 + agent state 的组合值得参考。

## 风险边界

- 不建议在主力账号、生产密钥或敏感代码环境中直接试用未经审计的配置管理器。
- Provider 切换和 Auth 编辑可能导致密钥泄漏、配置损坏或会话元数据混乱。
- README 中展示的 unrestricted / prompt injection 方向存在明确安全争议，应按研究和隔离测试处理。
- 第三方 Provider 的合规、计费和日志策略需要单独核查。

## 补充建议

- 若只是管理 Codex 配置，优先在测试账号和临时 `CODEX_HOME` 下试用。
- 对团队环境，应禁止自动写入未知提示词模板，保留配置 diff 和回滚路径。
- 后续观察重点是：项目能否把安全模式、只读预览、密钥脱敏、配置备份做扎实。
- 可与 `agentsview`、`ax`、`herdr` 等本地 agent 管理工具对比。

## 参考资料

- GitHub 仓库：<https://github.com/yynxxxxx/Codex-X>
- OpenAI Codex：<https://github.com/openai/codex>
