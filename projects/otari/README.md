<!-- markdownlint-disable MD013 -->

# Otari

> 更新：2026-10-19（Asia/Shanghai）。分类：模型、训练与推理基础设施。上游 `mozilla-ai/otari`；本文基于官方榜单、认证 API 与文档 / 源码静态核验，未安装运行。源码快照 `64155c48ce0d`；Release 与主分支行为分别说明。热度见[当日官方榜单](https://github.com/trending/python?since=daily)。

## 定位

mozilla.ai 的自托管 LLM gateway，置于应用与模型 provider 之间，提供 OpenAI / Anthropic 兼容入口、virtual keys、工作区、预算、路由和 usage 记录；provider 调用通过 any-llm 适配。README 声称支持 40+ providers，不能据此保证所有 API 特性完全兼容。[来源 1](https://github.com/mozilla-ai/otari/blob/64155c48ce0d11a1e113827d7f472b7b76dbf526/README.md)

官方 Python Trending 约 +46 当日 stars；API 为 658 / 83 / 315（stars / forks / open issues）；采样最新稳定 Release 为 v0.28.0。核心 Apache-2.0。[来源 2](https://api.github.com/repos/mozilla-ai/otari)[来源 3](https://github.com/mozilla-ai/otari/releases/tag/v0.28.0)[来源 8](https://github.com/mozilla-ai/otari/blob/64155c48ce0d11a1e113827d7f472b7b76dbf526/LICENSE)

## 用法

新部署先选 standalone，在测试数据库里配置 master key、provider 与定价，再给应用发限模型 / 限预算的 API key；客户端 base URL 为 `http://localhost:8000/api/v1`。正式使用前配置持久 PostgreSQL、TLS、备份与必要 secret。[来源 1](https://github.com/mozilla-ai/otari/blob/64155c48ce0d11a1e113827d7f472b7b76dbf526/README.md)[来源 4](https://github.com/mozilla-ai/otari/blob/64155c48ce0d11a1e113827d7f472b7b76dbf526/docs/deployment.md)

**v0.27 → v0.28 升级要点**：Release 明示不再仅凭环境变量自动识别 provider key；必须在 config 中声明，例如 `openai: {api_key: ${OPENAI_API_KEY}}`，或在 dashboard 添加 provider；keyless provider 也要声明，否则可返回 `424 provider_not_configured`。[来源 3](https://github.com/mozilla-ai/otari/releases/tag/v0.28.0)

本轮未部署网关、接入 provider、调用模型或执行迁移。

## 原理

请求先认证并解析工作区 / provider 凭据、检查预算，再分派到模型，之后写 usage；路由可做 fallback、加权或学习式选择。应用应持 scoped key，master key 保留部署管理用途。[来源 1](https://github.com/mozilla-ai/otari/blob/64155c48ce0d11a1e113827d7f472b7b76dbf526/README.md)[来源 5](https://github.com/mozilla-ai/otari/blob/64155c48ce0d11a1e113827d7f472b7b76dbf526/docs/access-control.md)

standalone 的管理和推理同进程；hosted 是控制面职责；hybrid data plane 会与 otari.ai 交互。未设 OTARI_MODE 时，存在 OTARI_AI_TOKEN 会选 hybrid，否则默认 standalone。部署者与进程 mode 是两个维度。[来源 1](https://github.com/mozilla-ai/otari/blob/64155c48ce0d11a1e113827d7f472b7b76dbf526/README.md)[来源 6](https://github.com/mozilla-ai/otari/blob/64155c48ce0d11a1e113827d7f472b7b76dbf526/docs/modes.md)

## 价值

对多应用 / 多模型团队，统一凭据、撤销、归因和路由可降低每个客户端的集成成本。它也提供复盘一次 Agent 运行的时间与成本入口；是否省钱、兼容具体 SDK 和能否覆盖故障场景，仍需自己的负载测试。

## 风险边界

- 自托管 gateway 仍会把内容送到所配置的模型、MCP、搜索或执行服务；hybrid 更不能当作全链路离线。
- 默认 Compose 的 gateway `8000:8000` 没有限定 host 回环地址；PostgreSQL 与部分辅助服务另绑 127.0.0.1。发布前需核管理面、TLS、反向代理及凭据，不把 localhost 示例 URL 当作网络隔离。[来源 4](https://github.com/mozilla-ai/otari/blob/64155c48ce0d11a1e113827d7f472b7b76dbf526/docs/deployment.md)[来源 9](https://github.com/mozilla-ai/otari/blob/64155c48ce0d11a1e113827d7f472b7b76dbf526/docker-compose.yml)
- 主分支 traces 默认开启、保留 30 天；文档称不记录 prompt / output / tool content，但会保留 names、IDs、时间、token、结果与费用。该声明只覆盖 traces，不能外推所有日志和 provider 留存；hybrid 当前不存 traces。[来源 7](https://github.com/mozilla-ai/otari/blob/64155c48ce0d11a1e113827d7f472b7b76dbf526/docs/traces.md)
- dashboard session 和推理 API key 的授权不同；配置声明的 key 会在重启恢复，API 轮换不能替代修改配置。预算与 usage 需同 provider 账单核对。[来源 5](https://github.com/mozilla-ai/otari/blob/64155c48ce0d11a1e113827d7f472b7b76dbf526/docs/access-control.md)
- README 的临时 Docker 示例停止即删 SQLite；生产需固定镜像和预演迁移，主分支文档不保证与 v0.28.0 完全一致。[来源 1](https://github.com/mozilla-ai/otari/blob/64155c48ce0d11a1e113827d7f472b7b76dbf526/README.md)[来源 4](https://github.com/mozilla-ai/otari/blob/64155c48ce0d11a1e113827d7f472b7b76dbf526/docs/deployment.md)

## 补充建议

用本地 mock provider 验证缺配置、撤销、额度耗尽、错误定价、fallback 与流式中断；再接低额度真实 key。升级时先备份数据库、配置、Fernet key 和相关 pepper，核 v0.28 的 provider 声明变更；把 usage、trace、外部账单的差异保留下来。

## 参考资料

1. [README](https://github.com/mozilla-ai/otari/blob/64155c48ce0d11a1e113827d7f472b7b76dbf526/README.md)
2. [仓库 API](https://api.github.com/repos/mozilla-ai/otari)
3. [v0.28.0 Release](https://github.com/mozilla-ai/otari/releases/tag/v0.28.0)
4. [部署说明](https://github.com/mozilla-ai/otari/blob/64155c48ce0d11a1e113827d7f472b7b76dbf526/docs/deployment.md)
5. [访问控制与 key 生命周期](https://github.com/mozilla-ai/otari/blob/64155c48ce0d11a1e113827d7f472b7b76dbf526/docs/access-control.md)
6. [Runtime modes](https://github.com/mozilla-ai/otari/blob/64155c48ce0d11a1e113827d7f472b7b76dbf526/docs/modes.md)
7. [Trace 内容与默认值](https://github.com/mozilla-ai/otari/blob/64155c48ce0d11a1e113827d7f472b7b76dbf526/docs/traces.md)
8. [LICENSE](https://github.com/mozilla-ai/otari/blob/64155c48ce0d11a1e113827d7f472b7b76dbf526/LICENSE)
9. [Compose 网络与存储](https://github.com/mozilla-ai/otari/blob/64155c48ce0d11a1e113827d7f472b7b76dbf526/docker-compose.yml)
