<!-- markdownlint-disable MD013 MD034 -->

# New API：统一多模型协议、路由、配额与计费的自托管网关

> 上游仓库：https://github.com/QuantumNous/new-api · 归类：模型、训练与推理基础设施 · 本页基于 2026-09-22 的 README、认证文档、release、许可证与 REST API 静态整理；未部署服务、配置上游 key、做协议互比或开展公网运营。

## 定位

New API 是面向应用、Agent 与团队的 AI gateway：把 OpenAI Chat / Responses、Anthropic Messages、Gemini 等接口和多家模型渠道汇聚到同一控制面，提供模型映射、权重 / 优先级、重试、配额、订阅、计费、访问控制与日志。它管理授权访问，不会替用户取得上游转售权或满足监管义务。

2026-09-22 的 GitHub 官方 Go Trending 抓取显示约 `+103 stars today`；REST API 快照为 `48,610 stars / 11,664 forks / 1,338 open issues`，AGPL-3.0，最新 release 为 `v1.0.0-rc.40`（9 月 21 日）。RC 与高 issue 数意味着升级前仍需按目标协议回归。

## 用法

本地 SQLite smoke 可只绑定 loopback：

```sh
mkdir -p data
docker run --name new-api -d --restart unless-stopped \
  -p 127.0.0.1:3000:3000 \
  -e TZ=Asia/Shanghai \
  -v "$(pwd)/data:/data" \
  calciumion/new-api:v1.0.0-rc.40
```

创建管理员后，添加获授权的上游渠道、模型与 group，设置价格 / 配额，再签发 New API 自己的 client key。生产部署需替换数据库 / Redis 示例密码，固定 `SESSION_SECRET` / `CRYPTO_SECRET`，配置 HTTPS cookie 和 exact trusted origins。

## 原理

- Go / Gin backend 接收多种兼容接口，经 middleware 做身份、权限、配额和审计，再由 relay adapter 选择上游。
- RelayKit 在 OpenAI、Responses、Anthropic 与 Gemini 文本协议之间转换 request、response 与 stream。
- channel priority、weight、model mapping、retry 与 affinity 决定路由；实际能力仍受模型和上游 channel 限制。
- 用户、group、API key restriction、OAuth / OIDC、passkey、2FA 与 session 共同构成控制面身份层。
- SQLite / MySQL / PostgreSQL 保存核心状态，Redis 可共享 cache 与 rate limit，ClickHouse 可作为独立日志库；task plugin 扩展异步图片 / 视频接口。

## 价值

- 客户端可稳定指向一个内部 base URL，把 provider 切换、模型映射和凭据管理集中化。
- 使用量、cache、价格表达式、配额与订阅放在同一账本，有利于团队成本归因。
- 同时保留原生 Anthropic / Gemini 与 OpenAI-compatible 接口，减少强行把所有字段压成最低公分母。
- 认证、session、proxy、插件与多节点约束有专门文档，提供生产审计入口。

## 风险边界

- 协议“兼容”不是语义等价：tool call、reasoning、多模态、cache、usage 与 error 在转换路径上可能丢失或改变。
- 网关集中保存上游 key、client key、prompt、usage 和计费记录，是高价值攻击目标；日志也可能含敏感内容。
- 权重 / 重试可能重复产生付费请求或副作用；内存 rate limit 与分离 Redis 会造成节点间配额不一致。
- 部署公共生成式 AI 或 API 转售涉及上游条款、授权、实名、内容安全、日志、税务与当地监管；AGPL 也有网络使用义务。
- `v1.0.0-rc.40`、迁移和 provider API 都会变化；本页未验证每种模型的 stream / tool / realtime 互操作。

## 补充建议

1. 先用测试 key 和固定模型建立 contract suite，逐项比较原生与网关的字段、流事件、usage、错误和取消行为。
2. provider key 分组最小授权，禁止在日志记录 secret / 完整敏感 prompt，并定期轮换与演练撤销。
3. 生产固定 release / image digest，升级前备份数据库并在 staging 执行迁移、回滚、并发和限流测试。
4. 公网服务前由法律 / 合规人员核验上游授权、AGPL 与当地生成式 AI、隐私、计费和税务要求。

## 参考资料

- 上游 README：https://github.com/QuantumNous/new-api
- 官方文档：https://docs.newapi.ai/en/docs
- Authentication：https://github.com/QuantumNous/new-api/blob/main/docs/authentication.md
- RelayKit：https://github.com/QuantumNous/new-api/tree/main/relaykit
- `v1.0.0-rc.40` release：https://github.com/QuantumNous/new-api/releases/tag/v1.0.0-rc.40
- GitHub REST API：https://api.github.com/repos/QuantumNous/new-api
- LICENSE：https://github.com/QuantumNous/new-api/blob/main/LICENSE
