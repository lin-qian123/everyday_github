<!-- markdownlint-disable MD013 -->

# rig

## 定位

Rig 是构建 LLM 应用的 Rust 库，也提供以 Bevy plugins 组合的终端编码 Agent。当前主干的模型、工具、会话和界面均按 crate / plugin 分层；不能把历史 SDK 示例直接当作当前 CLI 的配置说明。[固定 README](https://github.com/0xPlaygrounds/rig/blob/2fa895b7cf60990c4589b83b7f5fcac6edba33da/README.md)

- 上游：[0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig)，仓库 ID `810861466`。
- 2026-11-23（Asia/Shanghai）07 时段：官方 Rust daily **+8**；API stars / forks / open issues（含 PR）**9,225 / 1,030 / 67**。[API](https://api.github.com/repos/0xPlaygrounds/rig)
- 最新核到非预发行版 [v0.47.0](https://github.com/0xPlaygrounds/rig/releases/tag/v0.47.0)，UTC 2026-11-20；主干固定 `2fa895b7cf60990c4589b83b7f5fcac6edba33da`，workspace 版本同为 0.47.0。crates.io 版本 API 本轮返回 403，没有独立核到已发布包内容。
- 分类：`Agent 框架与技能生态`；CLI 是同一仓库能力，在本页说明。本轮没有构建、登录、调用模型或启动子 Agent。

## 用法

当前发行标签的 Agent 指南要求 **Rust 1.97.1+、Linux 或 macOS**，Windows 不支持。可参考以下固定发行版本的安装入口，命令未执行：

```bash
cargo install --locked --version 0.47.0 rig
rig --help
rig
```

首次 `rig` 会生成并编译插件组合，需数分钟和额外构建空间；之后按指南选择模型、通过 `/login` 或 provider 环境配置完成认证。SDK 应用则从 `cargo add rig@=0.47.0` 起步，按具体 provider / vector store 选择 feature；默认 facade 同时带 agent、宏、reqwest，以及原生平台的 CLI，纯库可研究 `default-features = false` 的最小依赖。[发行指南](https://github.com/0xPlaygrounds/rig/blob/v0.47.0/docs/agent.md)、[固定 README](https://github.com/0xPlaygrounds/rig/blob/2fa895b7cf60990c4589b83b7f5fcac6edba33da/README.md)、[Cargo 清单](https://github.com/0xPlaygrounds/rig/blob/2fa895b7cf60990c4589b83b7f5fcac6edba33da/Cargo.toml)

主配置为 `RIG_HOME/settings.toml`，默认 home 是 `~/.rig`。0.46 的 `plugins.toml` 和 `defaults.json` 在 0.47 不再读取；按启动提示及迁移说明转入新配置。先备份 home 和会话，再验证迁移与恢复。[迁移说明](https://github.com/0xPlaygrounds/rig/blob/2fa895b7cf60990c4589b83b7f5fcac6edba33da/MIGRATING.md)、[主干指南](https://github.com/0xPlaygrounds/rig/blob/2fa895b7cf60990c4589b83b7f5fcac6edba33da/docs/agent.md)

## 原理

库层统一 provider、消息、工具、流式输出和 embedding 等接口；向量库通过伴随 crate 接入。终端层由 launcher 根据插件选择生成 Cargo 项目，再启动 Bevy app；kernel 把 agent、turn 和 tool call 作为实体及 effect 组织。Rust 类型能约束数据接口，模型回答和外部工具效果仍需另外验证。[README](https://github.com/0xPlaygrounds/rig/blob/2fa895b7cf60990c4589b83b7f5fcac6edba33da/README.md)、[生成项目实现](https://github.com/0xPlaygrounds/rig/blob/2fa895b7cf60990c4589b83b7f5fcac6edba33da/crates/rig-cli/src/project.rs)

主干默认工具包含 `read / edit / write / shell`；可选的审批、secret redaction、预算、MCP、subagents 等是不同插件。审批基础设施只汇总其他 gate 请求的确认，本身不会自动为每条 shell 建立限制。[插件默认表](https://github.com/0xPlaygrounds/rig/blob/2fa895b7cf60990c4589b83b7f5fcac6edba33da/crates/rig-harness-protocol/src/config.rs)、[审批实现](https://github.com/0xPlaygrounds/rig/blob/2fa895b7cf60990c4589b83b7f5fcac6edba33da/plugins/rig-basics/src/approval.rs)

## 价值

- 适合 Rust 服务将模型访问、检索、工具调用与观测放入同一工程体系。
- 编码 Agent 可通过插件替换交互和策略，并保留具体构建组合，便于比较行为变化。
- Record / replay 和 typed hooks 有测试组织价值，但不保证真实 provider 行为、业务正确率或节省费用；本轮未复现基准。

## 风险边界

- **默认主机工具。** 写文件和 shell 默认开；Approval、Redact、Budget 等默认关。即使启用 ApprovalPlugin，也需有实际 gate 添加审批原因；提示词、Rust 内存安全或 `--tools` 列表不提供操作系统隔离。外部插件会被编译并在进程中运行。[默认配置](https://github.com/0xPlaygrounds/rig/blob/2fa895b7cf60990c4589b83b7f5fcac6edba33da/crates/rig-harness-protocol/src/config.rs)、[审批实现](https://github.com/0xPlaygrounds/rig/blob/2fa895b7cf60990c4589b83b7f5fcac6edba33da/plugins/rig-basics/src/approval.rs)
- **MCP 文档与默认表有出入。** 发行指南描述项目 MCP server 需批准；但本轮核到 v0.47.0 与固定主干的默认表均将 McpPlugin、McpApprovalPlugin 分别标 `off`，注释还说明信任项目 server。不能假定启用 MCP 自动启用审批；检查最终插件组合并验证拒绝 / 配置变化路径。[发行指南](https://github.com/0xPlaygrounds/rig/blob/v0.47.0/docs/agent.md)、[发行默认表](https://github.com/0xPlaygrounds/rig/blob/v0.47.0/crates/rig-harness-protocol/src/config.rs)、[主干默认表](https://github.com/0xPlaygrounds/rig/blob/2fa895b7cf60990c4589b83b7f5fcac6edba33da/crates/rig-harness-protocol/src/config.rs)
- **safe 是构建恢复。** `rig --safe` 只用默认 plugins 构建来排查插件失败，会忽略用户的 plugins 开关，模型与其他配置继续适用。它不等于受限 shell 或 sandbox；禁用敏感工具的自定义配置不会自动延续到 safe 构建。[指南](https://github.com/0xPlaygrounds/rig/blob/2fa895b7cf60990c4589b83b7f5fcac6edba33da/docs/agent.md)
- **预算与压缩各有损失。** 可选 BudgetPlugin 会停止后续调用 / 取消在途调用，但未计入的在途服务商费用可使账单超限，订阅模型可能没有美元定价。0.47 的 compaction 去掉 undo，旧消息保留在 transcript 不等于之后每次请求仍带完整旧上下文；摘要遗漏、计数估算与额外调用需要测试。[发行指南](https://github.com/0xPlaygrounds/rig/blob/v0.47.0/docs/agent.md)、[v0.47.0](https://github.com/0xPlaygrounds/rig/releases/tag/v0.47.0)
- **凭据和源码。** `RIG_HOME/auth/` 保存登录资料，session / spill / 可选 traffic 等可能含工具结果；默认 Redact 关闭。模型数据出口、日志权限与 retention 分别核验；本轮未做网络流量或秘密脱敏测试。[指南](https://github.com/0xPlaygrounds/rig/blob/2fa895b7cf60990c4589b83b7f5fcac6edba33da/docs/agent.md)、[默认表](https://github.com/0xPlaygrounds/rig/blob/2fa895b7cf60990c4589b83b7f5fcac6edba33da/crates/rig-harness-protocol/src/config.rs)
- **版本与许可。** pre-1.0 仍可能破坏 API，main 指南可超前于 release；根代码 MIT，模型、向量服务和插件许可分别处理。[LICENSE](https://github.com/0xPlaygrounds/rig/blob/2fa895b7cf60990c4589b83b7f5fcac6edba33da/LICENSE)、[MIGRATING](https://github.com/0xPlaygrounds/rig/blob/2fa895b7cf60990c4589b83b7f5fcac6edba33da/MIGRATING.md)

## 补充建议

先做一个固定版本、可丢弃工程的最小问答 / 工具任务，记录 provider、模型、插件清单和总耗时 / 费用；再核审批拒绝、日志和摘要恢复。已有 0.46 用户先迁移配置并比较最终启用表；将 SDK 编译测试、CLI 权限测试和真实模型质量分别验收。

## 参考资料

- [README](https://github.com/0xPlaygrounds/rig/blob/2fa895b7cf60990c4589b83b7f5fcac6edba33da/README.md)、[Cargo.toml](https://github.com/0xPlaygrounds/rig/blob/2fa895b7cf60990c4589b83b7f5fcac6edba33da/Cargo.toml)、[v0.47.0](https://github.com/0xPlaygrounds/rig/releases/tag/v0.47.0)。
- [发行 Agent 指南](https://github.com/0xPlaygrounds/rig/blob/v0.47.0/docs/agent.md)、[主干 Agent 指南](https://github.com/0xPlaygrounds/rig/blob/2fa895b7cf60990c4589b83b7f5fcac6edba33da/docs/agent.md)、[迁移记录](https://github.com/0xPlaygrounds/rig/blob/2fa895b7cf60990c4589b83b7f5fcac6edba33da/MIGRATING.md)。
- [默认插件表](https://github.com/0xPlaygrounds/rig/blob/2fa895b7cf60990c4589b83b7f5fcac6edba33da/crates/rig-harness-protocol/src/config.rs)、[项目生成](https://github.com/0xPlaygrounds/rig/blob/2fa895b7cf60990c4589b83b7f5fcac6edba33da/crates/rig-cli/src/project.rs)、[审批实现](https://github.com/0xPlaygrounds/rig/blob/2fa895b7cf60990c4589b83b7f5fcac6edba33da/plugins/rig-basics/src/approval.rs)、[本机工具说明](https://github.com/0xPlaygrounds/rig/blob/2fa895b7cf60990c4589b83b7f5fcac6edba33da/crates/rig-tools/README.md)。
