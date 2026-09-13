<!-- markdownlint-disable MD013 -->

# GPT-Load（tbphp/gpt-load）中文解读

> 证据快照：2026-09-14（Asia/Shanghai）。GitHub REST API 显示 6,722 stars、724 forks、15 open issues，最新 release 为 `v2.0.0-rc.17`（2026-09-13），MIT。2.0 是完整重写，官方明确说明不能打开、导入或原地迁移 1.x 数据；当前 `2` 镜像在 GA 前跟随 Beta/RC。本文未部署网关、导入账号、发起模型请求或验证上游协议兼容性。

## 定位

GPT-Load 是面向多 provider、多凭据和多客户端协议的自托管 AI 网关。应用只连接一个地址和 AccessKey，管理员在服务端集中配置 OpenAI、Anthropic、Gemini 等 API、订阅账号、模型分组、调度、重试、会话亲和、日志、用量和成本估算。

它解决接入与运维聚合，不提供模型本身，也不能把订阅账号、兼容中转或协议转换自动变成合规、等价、稳定的生产服务。

## 用法

官方推荐 Docker Compose：

```bash
git clone --depth 1 https://github.com/tbphp/gpt-load.git
cd gpt-load
cp .env.example .env
docker compose up -d
curl --fail http://127.0.0.1:3001/health
docker compose exec gpt-load sh -c 'cat /app/data/auth.key'
```

首次登录后添加渠道、创建 Group、再创建最小权限 AccessKey。2.0 应使用独立数据库、`DATA_DIR`、端口和 volume，与 1.x 并行验证并保留回滚窗口。

## 原理

- 单个 Go 服务内嵌管理 UI，以 SQLite、MySQL 或 PostgreSQL 保存配置和运行状态。
- 渠道层封装 API key、OAuth/订阅账号与兼容端点；Group 绑定模型、权重、重试、冷却、黑名单和会话亲和。
- AccessKey 控制客户端可访问的 Group 和协议；入口覆盖 OpenAI Chat/Responses/Images/Embeddings/Rerank、Anthropic Messages 与 Gemini 路径。
- 网关根据能力声明做协议透传或有限转换，并归一化流式响应、错误、用量与成本估算。
- 渠道凭据由 `encryption.key` 加密；数据库、`auth.key` 与加密密钥共同构成可恢复状态。

## 价值

- 将模型端点、凭据健康、failover 与用量观察集中起来，减少每个客户端重复配置。
- 保留多类原生协议，而不是强迫所有 provider 都降到单一 Chat Completions 形状。
- 默认监听 `127.0.0.1`，单二进制/Compose 和内嵌 UI 降低个人或小团队的试用门槛。
- release、容器、校验和、第三方 notices 与多数据库支持提供了较完整的运维入口。

## 风险边界

- 网关集中保存 API key、OAuth token、请求日志和使用数据，一旦管理密钥、数据库、镜像或主机失陷，blast radius 会覆盖多个 provider。
- 当前不支持主加密密钥轮换；`encryption.key` 丢失后既有凭据不可恢复，复制错误又可能造成长期泄露。
- 2.0 RC 与 1.x 数据不兼容，`2` 标签在 GA 前会移动；不能对现有实例做无备份原地升级。
- 官方说明 2.0 按单应用实例设计，不支持直接横向扩容；这不是高可用控制面。
- 成本来自上游 usage 和本地定价估算，不是财务对账；协议可返回不代表状态、tool calling、cache、错误或计费语义等价。
- 订阅账号/OAuth 适配可能受 provider 条款与协议变化影响；只能接入有权使用的账号，并限制日志和凭据可见范围。

## 补充建议

1. 固定 RC 的镜像 digest 和仓库 tag，在隔离环境用低额度测试 key 验证每个协议、错误、stream 与 failover。
2. 管理面只暴露在受控网络/TLS 反代后，分离 admin key 与客户端 AccessKey，并显式配置协议和 Group allowlist。
3. 将数据库、`auth.key`、`encryption.key` 加密备份到独立位置，定期做恢复演练；不要把密钥写入仓库、截图或 issue。
4. 用 provider 账单对比本地用量，记录 rate limit、cache、stateful Responses 和重试是否造成重复费用。

## 参考资料

- GitHub：<https://github.com/tbphp/gpt-load>
- GitHub REST API：<https://api.github.com/repos/tbphp/gpt-load>
- 中文 README：<https://github.com/tbphp/gpt-load/blob/main/README_CN.md>
- Releases：<https://github.com/tbphp/gpt-load/releases>
- 官方文档：<https://www.gpt-load.com>
- 安全策略：<https://github.com/tbphp/gpt-load/blob/main/SECURITY.md>
- 第三方声明：<https://github.com/tbphp/gpt-load/blob/main/THIRD_PARTY_NOTICES.md>
- LICENSE：<https://github.com/tbphp/gpt-load/blob/main/LICENSE>
