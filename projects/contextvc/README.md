# contextvc

<!-- markdownlint-disable MD013 -->

## 定位

`contextvc` 是一个 Git-native context control plane，命令名为 `ctx`。它把项目规则、决策、失败记忆、how-to、偏好和代码地图存进 `.context/`，再渲染成 Claude Code、Cursor、Codex、GitHub Copilot、Gemini、Cline 等工具原生读取的配置文件。

截至 2026-07-13，GitHub API 显示该仓库约 141 stars、4 forks，创建于 2026-07-05，许可证为 Apache-2.0。

## 用法

安装：

```bash
cargo install --locked --git https://github.com/HaochengLu/contextvc.git --tag v0.1.0
ctx --help
```

在仓库中初始化：

```bash
ctx init --install-hooks
ctx status
ctx check
```

它可生成或维护：

```text
.context/
AGENTS.md
CLAUDE.md
.cursor/rules/*.mdc
.github/copilot-instructions.md
GEMINI.md
.cline/memory-bank/contextvc.md
.mcp.json
```

## 原理

contextvc 把 agent 需要的长期上下文当成代码资产管理：可版本化、可 review、可 merge、可在 CI 中检查，并能在高风险操作前通过 hook 做拦截。它关注的不是“模型怎么记住”，而是“仓库如何治理给模型看的上下文”。

## 价值

- 解决多工具时代规则散落在 `AGENTS.md`、`CLAUDE.md`、Cursor rules、Copilot instructions 的同步问题。
- 适合团队把 agent memory 纳入 PR review，而不是让本地偏好静默漂移。
- Git-native 设计方便分支、回滚、冲突处理和 CI 验证。
- 与本仓库的三文件约束高度相关，可作为未来自动维护 `AGENTS.md` / tool-specific rules 的参考。

## 风险边界

- 它会生成多个 agent-facing 文件，使用前必须确认不会覆盖团队已有手写规则。
- 规则同步不能替代真实测试，也不能保证 agent 遵守所有约束。
- Rust CLI 与 hook 机制需要跨平台验证，尤其是 Windows 和 GUI agent 场景。
- 若 `.context/` 内容过多，可能增加 agent 上下文噪音。

## 补充建议

- 适合多 agent 工具并存、且规则经常漂移的工程团队试点。
- 建议先在小仓库中验证 `ctx check`、生成文件 diff 和 hook 行为。
- 重点观察它是否能处理上下文 stale detection 和语义 merge。

## 参考资料

- GitHub 仓库：<https://github.com/HaochengLu/contextvc>
- Rust 安装入口：<https://rustup.rs/>
- MCP 背景：<https://modelcontextprotocol.io/>
