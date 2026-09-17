<!-- markdownlint-disable MD013 MD034 -->

# Octop：面向个人、家庭与小团队的自托管多 Agent 助手

> 上游仓库：https://github.com/TencentCloud/Octop · 归类：记忆层与个人 AI 基础设施 · 本页基于 2026-09-18 的 README、SECURITY、配置文档、`pyproject.toml`、release、LICENSE 与 REST API 静态整理；未部署服务或验证多租户隔离。

## 定位

Octop 把 Web Dashboard、CLI、飞书 / 钉钉 / QQ / Discord / 企业微信渠道、定时任务和多 Agent 专家库放进一个自托管控制面。它面向个人、家庭和小团队，并支持持久记忆、RAG、浏览器、远程桌面、ACP 与第三方 connector。

2026-09-18 的 GitHub 官方综合 / Python Trending 抓取显示约 `+386 stars today`；REST API 快照为 `3,408 stars / 352 forks / 233 open issues`，MIT，`v1.0.0` 于 9 月 14 日发布，`pyproject.toml` 要求 Python `>=3.12`。

## 用法

上游提供 release、PyPI、Docker 与源码路径；最小本机流程为：

```sh
pip install octop
octop init
octop run
```

默认打开 `http://127.0.0.1:8088`。生产路径需先设置强管理员口令、固定版本、规划数据卷和备份，再决定是否启用 channel、browser、remote desktop、shell、connector 或 ACP。

## 原理

- FastAPI / uvicorn 提供 API 与单进程控制面，React Dashboard、CLI、IM channel 和 scheduler 共享 SQLite WAL 或 PostgreSQL。
- `harness-agent` 负责模型、tools、skills 与 checkpoint；`harness-memory` 管理可迁移记忆；`harness-browser` 提供 CDP 浏览器能力。
- expert library 让不同用户切换角色，plugin / connector / MCP / OAuth 扩展外部数据与动作范围。
- ACP 可以把任务交给 OpenCode 或 Claude Code；终端、浏览器与远程桌面又把控制面扩展到主机和 GUI。
- 数据默认位于 `~/.octop/`，但模型 provider、IM、OAuth、COS/S3 与外部 MCP 会形成新的出站路径。

## 价值

- 用一个可审阅控制面统一多人、多个 channel、记忆、知识库与定时任务，减少零散 bot 的身份和状态漂移。
- SQLite / PostgreSQL 与可插拔存储适合从单机试验逐步迁移到团队部署。
- tool approval、shell guard、PII redaction 和 security policy 为高权限功能提供了可配置入口。
- MIT 代码、SECURITY 与配置文档公开，便于组织做二次 hardening 和定制。

## 风险边界

- “self-hosted”只描述控制面位置；云模型、IM、OAuth connector、MCP、S3 和浏览器任务仍可能发送对话、文件、凭据或结果。
- 多用户共享控制面、家庭成员、专家记忆和外部 channel 会产生横向越权风险；JWT 存在不等于 row-level 与工具级隔离已被独立证明。
- shell、browser、remote desktop、cron 与 ACP 都能造成主机或外部系统副作用，审批规则必须覆盖实际 tool 参数和回读结果。
- SECURITY 明确把 host/network、JWT、管理员凭据、tool guard、API key 和 IM 凭据保护交给 operator；直接绑定 `0.0.0.0` 不能视为安全部署。
- 本页未安装 `v1.0.0`，没有验证 migration、备份恢复、prompt injection、插件供应链、并发或 channel 身份映射。

## 补充建议

1. 先在隔离主机上只绑定 loopback，使用本地模型、合成文档和两个测试账号验证用户、workspace、memory 与 connector 边界。
2. 默认关闭 shell、remote desktop、browser、cron 与第三方 plugin，逐项启用并为高影响动作加入人工批准和 post-readback。
3. 画出每个 provider / channel / connector 的数据流，分离 JWT、模型 key、IM 凭据与 OAuth token，并测试轮换和撤销。
4. 对 SQLite/PostgreSQL、文件、memory、plugin 与升级分别做备份恢复和跨版本 migration 演练。

## 参考资料

- 上游 README：https://github.com/TencentCloud/Octop
- 中文 README：https://github.com/TencentCloud/Octop/blob/main/README_CN.md
- `v1.0.0` release：https://github.com/TencentCloud/Octop/releases/tag/v1.0.0
- Security Policy：https://github.com/TencentCloud/Octop/blob/main/SECURITY.md
- 配置文档：https://github.com/TencentCloud/Octop/blob/main/docs/configuration.md
- GitHub REST API：https://api.github.com/repos/TencentCloud/Octop
- LICENSE：https://github.com/TencentCloud/Octop/blob/main/LICENSE
