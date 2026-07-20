<!-- markdownlint-disable MD013 -->

# fastctx

## 定位

`fastctx` 是一个面向 AI coding agent 的本地 Rust 工具运行时，通过 MCP 暴露结构化的仓库读取、搜索、文件发现、批量替换和 Bash 执行能力。它的目标是减少 agent 在 shell 拼接、路径转义、输出截断和跨平台差异上浪费的上下文。

## 用法

```bash
npm install --global fastctx
fastctx
```

首次运行会打开控制终端，配置输出级别、Bash 终端、后台任务存储、并发和列表分页等选项。应用配置后，可被 ChatGPT App、Codex CLI 或其他 MCP client 通过 `fastctx serve` 调用。

## 原理

FastCtx 将常见仓库操作变成稳定 schema 的 MCP 工具：`read`、`grep`、`glob`、`replace`、`run`、`run_background`、`job_output`、`job_kill` 和 `job_list`。agent 不再临时构造复杂 shell，而是传入路径、模式、范围和执行参数，由常驻 Rust 进程处理编码、分页、目录遍历、后台任务和输出边界。

## 价值

- 直接击中 coding agent 的上下文效率问题：减少为了“读文件/搜代码”消耗的工具轮次。
- 对 Windows、macOS、Linux 混合环境有意义，因为工具层承担跨平台差异。
- 与 MCP 生态天然兼容，可作为 Codex / ChatGPT / Claude 等工具的本地 repo access 层。

## 风险边界

- 它提升的是工具访问效率，不会自动改善需求理解或架构判断。
- `run` 和后台任务能力需要明确权限策略，否则会扩大 agent 可执行面。
- 批量替换虽然结构化，但仍需 git diff 和测试验证，不能把机械替换等同于安全修改。
- 新项目的长期维护、升级回滚和兼容性仍需观察。

## 补充建议

- 适合在大型仓库、跨平台仓库或 shell 输出容易截断的环境中试用。
- 可先只开启只读读取/搜索，再逐步放开 `replace` 和命令执行能力。
- 与仓库级 `AGENTS.md` 的权限说明配套，清楚定义哪些命令允许 agent 自动运行。

## 参考资料

- GitHub：<https://github.com/yc-duan/fastctx>
- README：<https://github.com/yc-duan/fastctx#readme>
- MCP：<https://modelcontextprotocol.io/>
