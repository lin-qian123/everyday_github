<!-- markdownlint-disable MD013 MD034 -->

# ZeroClaw：Rust 单二进制个人 Agent Runtime

> 上游仓库：https://github.com/zeroclaw-labs/zeroclaw · 归类：Agent 框架与技能生态 · 本页基于 2026-09-15 的 README、架构/安全文档、Cargo manifest、release、LICENSE 与 GitHub REST API 静态整理；未安装、启动服务或连接任何 channel/provider。

## 定位

ZeroClaw 是用 Rust 构建的自托管个人 agent runtime。它将多 provider、30 多种消息/语音/webhook channel、shell/browser/HTTP/MCP/hardware tools、SQLite memory、SOP、gateway/dashboard 和 ACP 放进一个可作为系统服务运行的框架，强调单机可控与跨平台部署。

2026-09-15 的 GitHub 官方 Rust Trending 抓取显示约 `+22 stars today`；REST API 快照为 `32,809 stars / 4,942 forks / 807 open issues`。API 识别为 Apache-2.0，但 README、Cargo manifest 和根许可证文件声明 `MIT OR Apache-2.0` 双许可；当前 release 与 workspace version 均为 `v0.8.5`（2026-09-05）。

## 用法

上游提供预编译安装脚本和源码/容器等路径。审计时应先锁定 release、核对资产哈希并阅读脚本，不直接把 `master` 管道交给 shell：

```sh
# 上游快速路径；生产使用前应先固定 v0.8.5 并审查脚本
curl -fsSL https://raw.githubusercontent.com/zeroclaw-labs/zeroclaw/master/install.sh | sh

zeroclaw quickstart
zeroclaw agent -a <alias>
zeroclaw service install
zeroclaw service start
```

最小 V3 配置需要 provider、agent、risk profile 等关联项。接真实 Telegram、Discord、email、webhook、hardware 或 cron 前，应先在 CLI、合成 workspace 和 supervised profile 中验证。

## 原理

- **Agent runtime**：channel 消息进入统一 loop，由 agent 选择 provider、memory 与 tools，再把结果返回 gateway / channel。
- **可插拔 provider/channel/tool**：Anthropic、OpenAI、Ollama 等 provider 与 Discord、Telegram、Matrix、email、voice、webhook 等 adapter 分层实现。
- **风险 profile**：ReadOnly / Supervised / Full 控制动作审批，shell policy、workspace 边界、domain allowlist 和 OTP 等组成策略层。
- **OS sandbox**：在 native runtime 上按平台尝试 Landlock、Bubblewrap、Firejail、Seatbelt、Docker 等 backend；策略决定是否运行，sandbox 才限制实际进程。
- **SOP 与服务化**：MQTT、webhook、cron 或 peripheral 事件可触发带审批和恢复的标准流程，gateway/dashboard 提供管理界面。
- **工具回执**：可为成功 tool result 生成会话内 HMAC evidence，但文档明确它不是持久审计日志。

## 价值

- 单一 runtime 同时覆盖 CLI、消息 channel、automation 和 hardware，可减少多套 bot glue code。
- provider、agent、risk profile 分离，便于不同 agent 使用不同模型、权限与 sandbox 组合。
- 上游文档公开列出 sandbox 自动检测、network caveat、YOLO mode 和失败边界，便于做真实威胁模型。
- Rust workspace 将 config、runtime、tools、channels、memory、gateway、hardware 等拆成 crate，方便局部审计与扩展。

## 风险边界

- “self-hosted / you own the data”不等于无网络外发：云模型、channel、HTTP/browser、MCP、remote dashboard 和 optional integrations 都可能传输内容。
- `sandbox_backend = auto` 在可用 backend 缺失时可能落到 `none`；macOS Seatbelt 也可能因工具兼容问题被换成 Docker。必须读取启动日志确认实际 backend。
- sandboxed tools 默认仍有完整 outbound network；Landlock 只限制文件系统，domain allowlist 和 private-host 策略需要另配。
- YOLO mode 会关闭审批、workspace 边界、shell policy、allow/denylist、OTP、sandbox 和 gateway pairing。公开 channel 连到 YOLO agent 等价于把高权限 shell 暴露给能触达端口的人。
- 30 多 channel、长期服务、cron/SOP、browser/shell 和硬件访问扩大 prompt injection、身份冒用、重复执行和凭据泄露面。
- 807 个 open issues 与快速版本演进要求固定版本、迁移、备份和回滚演练；stars 和 release 不能替代稳定性评估。
- 本页没有复现性能、内存占用、sandbox 强度、provider 兼容、回执、SOP 恢复或 dashboard 安全。

## 补充建议

1. 固定 `v0.8.5`，以无真实凭据、无网络或 allowlist 网络、ReadOnly/Supervised profile 和副本 workspace 启动。
2. 在每个平台记录实际 sandbox backend，分别测试路径穿越、symlink、环境变量、outbound network、监听端口和 child process。
3. 对每个 channel 使用独立测试身份与最小 scope，验证 pairing、actor identity、重放、速率限制、prompt injection 和消息删除。
4. 保持 YOLO 只在可丢弃 VM / dev box 使用；生产审计另开持久日志，不能只依赖会话内 tool receipt。
5. 用故障注入验证 cron/SOP 的幂等、网络中断、provider fallback、service restart 与重复 webhook。

## 参考资料

- 上游 README：https://github.com/zeroclaw-labs/zeroclaw
- 架构说明：https://github.com/zeroclaw-labs/zeroclaw/blob/master/docs/book/src/architecture/overview.md
- 安全概览：https://github.com/zeroclaw-labs/zeroclaw/blob/master/docs/book/src/security/overview.md
- Sandbox 文档：https://github.com/zeroclaw-labs/zeroclaw/blob/master/docs/book/src/security/sandboxing.md
- YOLO mode：https://github.com/zeroclaw-labs/zeroclaw/blob/master/docs/book/src/getting-started/yolo.md
- Cargo manifest：https://github.com/zeroclaw-labs/zeroclaw/blob/master/Cargo.toml
- `v0.8.5` release：https://github.com/zeroclaw-labs/zeroclaw/releases/tag/v0.8.5
- GitHub REST API：https://api.github.com/repos/zeroclaw-labs/zeroclaw
- LICENSE：https://github.com/zeroclaw-labs/zeroclaw/blob/master/LICENSE-APACHE
