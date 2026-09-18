<!-- markdownlint-disable MD013 MD034 -->

# Buzz：让人类、Agent、工作流与 Git 共享事件日志的协作空间

> 上游仓库：https://github.com/block/buzz · 归类：Agent 框架与技能生态 · 本页基于 2026-09-19 的 README、架构 / 安全文档、release、LICENSE 与 REST API 静态整理；未部署 relay、连接 Agent 或验证多租户安全。

## 定位

Block 开源的 Buzz 是一个可自托管协作空间：人类和 Agent 使用相同的 community、channel、身份、公钥签名、搜索与审计日志，消息、反应、workflow、review approval 和 Git event 都写成 Nostr event。它试图把聊天、Agent 编排、Git forge、工作流和项目记忆放到一个 relay 中，而不是继续用多个孤立面板拼接。

2026-09-19 的 GitHub 官方 Rust Trending 抓取显示约 `+124 stars today`；REST API 快照为 `33,626 stars / 4,409 forks / 3,615 open issues`，Apache-2.0。最新 GitHub release 为 `desktop-v0.5.23`（9 月 5 日）。

## 用法

桌面 release 提供 macOS、Linux 与 Windows 包；上游明确 Windows 包当前未签名。自托管开发路径需要 Docker 与 Hermit，或 Rust 1.88+、Node 24+、pnpm 10+ 与 `just`：

```sh
git clone https://github.com/block/buzz.git
cd buzz
. ./bin/activate-hermit
just setup
just build
just dev
```

生产单节点部署使用 `deploy/compose/` 中的 Postgres、Redis、MinIO 与可选 Caddy / TLS。Agent 通过 `BUZZ_PRIVATE_KEY`、`buzz-cli` 或 `buzz-acp` 接入。

## 原理

- `buzz-relay` 是唯一协调中心，处理 NIP-01 事件、NIP-42 / NIP-98 认证、channel、DM、media、workflow、Git REST 与 audit。
- Postgres 保存事件、频道、token、workflow、audit 与全文索引；Redis 做 pub/sub；S3 / MinIO 保存 media。
- 每个事件由人或 Agent 的 keypair 签名；channel membership、scope 与 community context 决定可见性，host URL 是 multi-community 的权威边界。
- `buzz-acp` 通过 WebSocket 订阅 relay，再用 ACP / JSON-RPC 启动 Goose、Codex、Claude Code 等子进程；每 channel 最多一个 prompt in flight。
- YAML workflow 可由消息、reaction、schedule 或 webhook 触发，支持人工 approval infrastructure；Git 事件和 hosting 走同一 relay。
- hash-chain audit 能检测历史条目被篡改，但 event submission 的 audit / workflow trigger 是异步任务，失败不会回滚主事件。

## 价值

- 人类和 Agent 共用身份、频道和审计模型，避免“后台 cron bot”脱离团队上下文与责任边界。
- 将对话、patch、CI、approval 与 release decision 放进同一事件流，有利于形成可检索的项目 provenance。
- 自托管 relay、开放协议和 Apache-2.0 便于组织控制协作数据和扩展自己的 Agent surface。
- 架构文档对已实现、正在接线和仅有愿景的部分做了显式区分，便于技术尽调。

## 风险边界

- 架构文档明确当前没有实际 rate limiting 实现；配置中虽有 tier，不能据此声称 relay 已防刷或资源滥用。
- `send_dm`、`set_channel_topic` 等 workflow action 仍会返回 `NotImplemented`；README 也将移动端、approval glue 等列为在建。
- hash-chain audit 只能暴露链内篡改，不能保证事件内容真实、私钥安全、所有副作用都被记录，且 ephemeral / AUTH 事件不进入审计。
- Agent 可操作 repos、patch、workflow、channel 与外部工具；独立 keypair 不等于最小权限正确，更不等于执行进程被 sandbox。
- multi-community 可共享 Postgres、Redis 与对象存储；host-derived tenant context、搜索重授权和每条存储路径都需要对抗测试。
- Windows release 未签名；3,615 个 open issues 与“Not finished”声明说明项目仍在快速演进。本页未验证部署、认证、租户隔离、Git policy 或 crash recovery。

## 补充建议

1. 从单 community、测试 keypair 与只读 Agent 开始；先验证 channel / DM / search / media / Git 的权限矩阵，再考虑 multi-tenant。
2. 在入口前增加反向代理限流、连接 / payload / workflow quota 与资源告警，不依赖尚未实现的内部 rate limiter。
3. 对 Agent key、Git credential、webhook secret 和 approval token 建立短期轮换；高影响 workflow 必须有不可绕过的人审闸门。
4. 分别测试 audit task 失败、Redis / Postgres / S3 中断、Agent crash、跨 community 查询和恶意 Nostr event，并记录恢复语义。

## 参考资料

- 上游 README：https://github.com/block/buzz
- `desktop-v0.5.23` release：https://github.com/block/buzz/releases/tag/desktop-v0.5.23
- 架构说明：https://github.com/block/buzz/blob/main/ARCHITECTURE.md
- 安全政策：https://github.com/block/buzz/blob/main/SECURITY.md
- GitHub REST API：https://api.github.com/repos/block/buzz
- LICENSE：https://github.com/block/buzz/blob/main/LICENSE
