<!-- markdownlint-disable MD013 -->

# Shepherd Model Gateway（SMG）

> 更新：2026-10-20（Asia/Shanghai）。分类：模型、训练与推理基础设施。上游 `smg-project/smg`；快照 `26e73a3b22f4`（main）。本文基于官方榜单、认证 API 与上游文件静态研究；热度、版本时间与跨平台证据见[当日日报](../../daily/2026-10-20/ai-hotspots.md)。

## 定位

用 Rust 实现的模型路由网关，在一个端点后管理自托管推理 worker 与云 provider，覆盖 OpenAI / Anthropic 风格接口、缓存感知调度、gRPC、聊天历史、MCP 和扩展。它不提供模型权重，也不会增加 GPU 的物理容量。[README.md](https://github.com/smg-project/smg/blob/26e73a3b22f4812dccd7d407c0f98c2ff67046ef/README.md)

## 用法

上游提供 Docker、Helm、Python 和 Cargo 路径；生产先固定并审查发行版本。已有本地推理服务时，README 的最小体验为：[README.md](https://github.com/smg-project/smg/blob/26e73a3b22f4812dccd7d407c0f98c2ff67046ef/README.md)

```bash
pip install smg
smg launch --worker-urls http://localhost:8000
```

客户端请求 gateway 的 30000 端口。多 worker 可选择 `--policy cache_aware`；测试前先明确监听地址、认证、上游 key、模型名和失败重试策略。本轮未安装网关、启动 worker 或调用模型。

## 原理

gateway 接收请求，按模型 / 负载 / 前缀缓存策略选择 worker；HTTP 与 gRPC 路径适配不同 engine，支持 prefill / decode 拆分等部署。认证数据面与控制面分别配置：数据面将共享 / tenant key 映射为调用者身份，控制面可使用角色 API key 与 JWT / OIDC。[README.md](https://github.com/smg-project/smg/blob/26e73a3b22f4812dccd7d407c0f98c2ff67046ef/README.md)[crates/auth/src/config.rs](https://github.com/smg-project/smg/blob/26e73a3b22f4812dccd7d407c0f98c2ff67046ef/crates/auth/src/config.rs)[model_gateway/src/middleware/auth.rs](https://github.com/smg-project/smg/blob/26e73a3b22f4812dccd7d407c0f98c2ff67046ef/model_gateway/src/middleware/auth.rs)

## 价值

适合统一异构推理后端、做缓存亲和与负载均衡，也提供研究网关认证、worker 生命周期和失败恢复的入口。对小型单 GPU 部署，应先比较增加网关后的运维成本；高吞吐宣传不能代替固定模型、硬件、输入长度与 SLO 的实测。

## 风险边界

- 当前主分支默认 `host` 为 `0.0.0.0`，共享 `api_key` 为 None；数据面认证中间件在没有配置任何 key 时放行请求。localhost 示例 URL 不表示只监听本机；需要显式配置网络边界和各类认证。[model_gateway/src/config/types.rs](https://github.com/smg-project/smg/blob/26e73a3b22f4812dccd7d407c0f98c2ff67046ef/model_gateway/src/config/types.rs)[model_gateway/src/middleware/auth.rs](https://github.com/smg-project/smg/blob/26e73a3b22f4812dccd7d407c0f98c2ff67046ef/model_gateway/src/middleware/auth.rs)
- 网关 key 与 provider key 不是同一凭据：启用认证并匹配网关 key 后，中间件移除对应认证 header；公开 GET proxy、未启用认证的转发路径另有处理。不能仅凭一个 key 开关推断全部端点与数据存储都隔离。[model_gateway/src/middleware/auth.rs](https://github.com/smg-project/smg/blob/26e73a3b22f4812dccd7d407c0f98c2ff67046ef/model_gateway/src/middleware/auth.rs)
- MCP 可执行外部工具，WASM 可扩展请求处理；聊天存储、trace、mesh 与 provider 连接引入额外数据面。文档列出的可用机制不等于已经为部署实例正确配置。[README.md](https://github.com/smg-project/smg/blob/26e73a3b22f4812dccd7d407c0f98c2ff67046ef/README.md)
- latest Release `v1.13.0` 与本文主分支源码分别记录，不把后续主分支修复当作已安装包保证；代码 Apache-2.0，模型 / engine / 云服务另有条款与费用。[LICENSE](https://github.com/smg-project/smg/blob/26e73a3b22f4812dccd7d407c0f98c2ff67046ef/LICENSE)

## 补充建议

先用两个 mock worker 验证未认证 / 错 key、tenant 分离、worker 故障、流式断开与重试重复；再测固定请求集的命中率、TTFT、吞吐、P95 延迟和峰值内存。数据面、管理面、MCP / 历史存储分别设验收条件，并保留配置、镜像 digest 与 worker 版本。

## 参考资料

- [README.md](https://github.com/smg-project/smg/blob/26e73a3b22f4812dccd7d407c0f98c2ff67046ef/README.md)
- [LICENSE](https://github.com/smg-project/smg/blob/26e73a3b22f4812dccd7d407c0f98c2ff67046ef/LICENSE)
- [crates/auth/src/config.rs](https://github.com/smg-project/smg/blob/26e73a3b22f4812dccd7d407c0f98c2ff67046ef/crates/auth/src/config.rs)
- [model_gateway/src/middleware/auth.rs](https://github.com/smg-project/smg/blob/26e73a3b22f4812dccd7d407c0f98c2ff67046ef/model_gateway/src/middleware/auth.rs)
- [model_gateway/src/config/types.rs](https://github.com/smg-project/smg/blob/26e73a3b22f4812dccd7d407c0f98c2ff67046ef/model_gateway/src/config/types.rs)
- [仓库 API](https://api.github.com/repos/smg-project/smg)
- [v1.13.0 Release](https://github.com/smg-project/smg/releases/tag/v1.13.0)
