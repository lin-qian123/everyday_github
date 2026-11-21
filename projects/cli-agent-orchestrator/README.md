<!-- markdownlint-disable MD013 -->

# cli-agent-orchestrator

## 定位

AWS Labs 的 CLI Agent Orchestrator（CAO）以本地控制面协调多种已有编码 CLI，让 supervisor 分派工作、获取结果和接续会话。每个 worker 仍是带原生认证与能力的真实 CLI 进程；tmux 会话的分离不提供操作系统隔离。

- 上游：[awslabs/cli-agent-orchestrator](https://github.com/awslabs/cli-agent-orchestrator)，仓库 ID `1028432181`。
- 2026-11-22（Asia/Shanghai）07 时段：官方 Python daily **+14**；API stars / forks / open issues（含 PR）为 **1,618 / 342 / 179**。[API](https://api.github.com/repos/awslabs/cli-agent-orchestrator)
- 最新核到非预发行版 [v2.5.3](https://github.com/awslabs/cli-agent-orchestrator/releases/tag/v2.5.3)，UTC 2026-10-08；主干快照 `682cefa1f9c49673cf207e746062022aba6cb386` 的包版本写 `2.5.4`，不据此认定新 release 已发布。
- 分类：`Agent 框架与技能生态`。本轮仅核资料和少量实现，未安装、启动 server、登录 provider、创建 worker 或调用模型。

## 用法

主干要求 Python 3.11+、tmux 3.3+、uv，以及至少一个已经认证的 provider CLI。包元数据标注 POSIX，原生 Windows 的安装成功不能说明运行支持。[固定 README](https://github.com/awslabs/cli-agent-orchestrator/blob/682cefa1f9c49673cf207e746062022aba6cb386/README.md)、[包元数据](https://github.com/awslabs/cli-agent-orchestrator/blob/682cefa1f9c49673cf207e746062022aba6cb386/pyproject.toml)

固定本页主干的安装与默认 Kiro provider 接口示例，以下未执行：

```bash
uv tool install git+https://github.com/awslabs/cli-agent-orchestrator.git@682cefa1f9c49673cf207e746062022aba6cb386
cao --help
cao install code_supervisor
cao-server
```

在另一终端进入可恢复的目标项目，运行 `cao launch --agents code_supervisor`；用 launch 终端、tmux 或本机 `http://localhost:9889` 观察，结束时 `cao shutdown --session {session-name}`。上述默认是 Kiro；切换 Codex 等 provider 必须按其专门指南配置 profile、权限与认证。稳定版可选 PyPI `2.5.3`，不要混用主干新接口。v2.5.3 说明还指出 v2.5.1 / v2.5.2 曾打 tag 却未发布 PyPI，tag 与包版本要分别确认。

## 原理

`cao-server` 管理 session、terminal、inbox、workflow 等状态；默认 tmux backend 启动 provider 进程，适配器负责启动参数、状态检测与输出提取，SQLite 保存控制面数据。Agent 通过 `cao-mcp-server` 等入口使用 `assign`、`handoff`、`send_message` 协作。终端状态是适配器识别结果，仍需检查实际产物。[架构](https://github.com/awslabs/cli-agent-orchestrator/blob/682cefa1f9c49673cf207e746062022aba6cb386/CODEBASE.md)

`role` 给出权限预设，`allowedTools` 可显式覆盖，`delegateTools` 限制能授予子任务的工具；supervisor 默认委派上限为 `*`。工具声明、委派检查、provider 原生执行限制、主机隔离属于不同层次。[工具限制](https://github.com/awslabs/cli-agent-orchestrator/blob/682cefa1f9c49673cf207e746062022aba6cb386/docs/tool-restrictions.md)

## 价值

- 复用已有 CLI、认证与交互方式，适合把开发、审阅等职责组织成可观察任务。
- 将跨 provider 的分派、结果回传和会话管理放到统一控制面，便于演练失败、接续与人工接管。
- 对多仓库工作有组织价值，但本轮没有并行效率、成本或任务成功率的独立测量。

## 风险边界

- **默认权限不低。** 未指定 role / allowlist 时用 developer 权限，包含文件写入和 shell。固定工具文档与 SECURITY 的角色表已有细节漂移，不能只看一张旧表；以安装版本的解析结果和实际拒绝路径为准。
- **白名单强度因 provider 而异。** SECURITY 把部分 provider 列为原生强制，把 Codex / Kimi / Qwen 等列为提示词软约束，Hermes / Cursor 另有限制。profile 写 reviewer 不自动形成只读隔离；开放完整 shell 时也可能写文件或联网。[安全政策相关表](https://github.com/awslabs/cli-agent-orchestrator/blob/682cefa1f9c49673cf207e746062022aba6cb386/SECURITY.md)
- **Codex 默认绕过审批与 sandbox。** 固定指南和 `_build_codex_command()` 均显示默认 `--yolo`；只有适用的 `codexProfile` 路径改用 `--profile`，而 `allowedTools: ["*"]` 会再次强制 yolo。不要依赖被绕过的 Codex sandbox 配置来限制默认 worker。profile 文件、CLI 版本与非交互审批行为都须实机核验。[指南](https://github.com/awslabs/cli-agent-orchestrator/blob/682cefa1f9c49673cf207e746062022aba6cb386/docs/codex-cli.md)、[实现抽读](https://github.com/awslabs/cli-agent-orchestrator/blob/682cefa1f9c49673cf207e746062022aba6cb386/src/cli_agent_orchestrator/providers/codex.py)
- **本机端口仍是控制面。** 默认 loopback、认证关闭；可达该端口的本机进程 / 账户可能访问终端和输出。`auth.*` / `network.*` 配置字段目前部分仅为 schema，认证应核实际环境变量。local token 匹配后授予全部 scopes，且会被 agent pane 继承；它不提供只读 token 或对已持有它的 worker 的隔离。[配置与认证](https://github.com/awslabs/cli-agent-orchestrator/blob/682cefa1f9c49673cf207e746062022aba6cb386/docs/configuration.md)
- **数据与维护。** provider 模型仍可能接收源码；终端、日志、workflow 输出及可选 memory 需要保留和清理政策。当前主干不能视作稳定包的同义词，更新后应复测适配器与权限。
- **许可。** 根代码 Apache-2.0；各 CLI、模型订阅和第三方 profile / skills 的条款分别适用。[LICENSE](https://github.com/awslabs/cli-agent-orchestrator/blob/682cefa1f9c49673cf207e746062022aba6cb386/LICENSE)

## 补充建议

先用可丢弃项目和两项可验证任务测试分派、输出、超时与停止；固定 provider CLI 版本，并检查实际进程参数、`Enforcement:`、委派上限和真实拒绝。对敏感任务使用外部权限隔离并限制控制面可达范围，再评估并发带来的耗时和费用。本轮没有替用户调整任何 CAO、Codex 或主机配置。

## 参考资料

- [固定 README](https://github.com/awslabs/cli-agent-orchestrator/blob/682cefa1f9c49673cf207e746062022aba6cb386/README.md)、[架构](https://github.com/awslabs/cli-agent-orchestrator/blob/682cefa1f9c49673cf207e746062022aba6cb386/CODEBASE.md)、[v2.5.3](https://github.com/awslabs/cli-agent-orchestrator/releases/tag/v2.5.3)。
- [工具限制](https://github.com/awslabs/cli-agent-orchestrator/blob/682cefa1f9c49673cf207e746062022aba6cb386/docs/tool-restrictions.md)、[Codex 接入](https://github.com/awslabs/cli-agent-orchestrator/blob/682cefa1f9c49673cf207e746062022aba6cb386/docs/codex-cli.md)、[配置](https://github.com/awslabs/cli-agent-orchestrator/blob/682cefa1f9c49673cf207e746062022aba6cb386/docs/configuration.md)、[SECURITY](https://github.com/awslabs/cli-agent-orchestrator/blob/682cefa1f9c49673cf207e746062022aba6cb386/SECURITY.md)。
