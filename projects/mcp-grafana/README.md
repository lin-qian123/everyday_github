<!-- markdownlint-disable MD013 -->

# Grafana MCP：让 Agent 查询监控并受控管理资源

- 主上游：[grafana/mcp-grafana](https://github.com/grafana/mcp-grafana)；repository ID `907869862`。
- 采样日期：2026-10-28（Asia/Shanghai）；分类：Agent 框架与技能生态。
- API 累计快照：3,616 stars / 478 forks / 87 open issues（含 PR 口径），与榜单日增分开。
- 默认分支 `main`；主线依据固定在 `e41b5962411b17e311a33006982815701c336bb9`。发行 API 首项 [v2.1.1](https://github.com/grafana/mcp-grafana/releases/tag/v2.1.1)，UTC 2026-10-20T17:35:20Z，正式发行标记。
- 核验层级：一手文档、元数据和所列部分实现的静态阅读；未安装运行、调用模型、复现基准或验证真实用户效果。

## 定位

Grafana MCP 将 dashboard、数据源、Prometheus / Loki 查询以及部分告警 / incident 操作提供给 Agent。它是可观察性系统的工具接口，模型能查到日志不代表能正确诊断故障，也不代表已经获准修改生产资源。

## 用法

先按固定发行安装 binary / Docker 或上游支持的入口，使用测试 Grafana 和最小权限 service account。配置 `GRAFANA_URL` 与 `GRAFANA_SERVICE_ACCOUNT_TOKEN`，或用 token 文件变量；从 stdio、只读与少量工具类别开始：

```bash
mcp-grafana --disable-write   --enabled-tools=search,dashboard,prometheus,loki   --usage-stats=disabled
```

默认 stdio 不开监听端口；HTTP / SSE 文档默认 `localhost:8000`，streamable-http 默认 `/mcp`。上面仅为当前主线文档配置示例，本轮未启动或接入监控。发行首项 v2.1.1 与 main 功能应分开核对。

## 原理

MCP 请求被映射到 Grafana API 与配置的数据源，类别 / 工具开关决定注册范围，Grafana 与数据源凭据决定后端权限。HTTP 调用者认证与访问 Grafana 的 service account token 是两套身份；streamable-http 可传逐请求身份，SSE 不把对应逐请求 headers 传给工具调用。

## 价值

适合把告警、指标、日志、trace 与面板串成可追溯调查过程，减少人工复制查询。应保存时间范围、查询文本、数据源和观测结果，独立验证模型的因果解释；工具输出是线索，不能自动证明根因。

## 风险边界

- 写工具默认并非整体关闭。`--disable-write` 移除相应操作，也移除 raw SQL / InfluxDB 查询；`--enable-query` 可重新开放这些查询，而 SQL 本身可能写入，仍需数据源只读账号。
- 当前代码只在配置 caller token 时实施 HTTP / SSE 调用者认证；非 loopback 且无 token 会记录 error 后继续启动，不能把日志提示当作强制拒绝。远程部署须单独配置认证、TLS 与网络限制。
- Grafana URL override 默认关闭；开启后若无目标 allowlist，可请求可达的 HTTP(S) 地址。allowlist 不替代调用者认证或“凭据与目标”的绑定。
- README 声明匿名使用统计**默认开启**，按 server process 上报工具计数 / 配置概况，称不含参数、查询和凭据；可用 `--usage-stats=disabled` 关闭。本文核到文档与 main 接线，未抓包验证所有数据路径。
- 只读日志也可能含秘密并进入模型上下文，宽范围查询还会消耗后端资源；Loki 成本 guardrail 默认 off，需另行启用与验收。
- Apache-2.0 覆盖本仓库，Grafana Cloud、插件和数据源权限 / 费用另计。

## 补充建议

先用脱敏故障样本检验正确时间窗、时区、截断和查询开销，再检查服务账号的真实拒绝行为。写操作采用独立身份、变更预览与审批；保留查询证据，避免 Agent 直接处理生产 token 或完整敏感日志。

## 参考资料

- [README.md](https://github.com/grafana/mcp-grafana/blob/e41b5962411b17e311a33006982815701c336bb9/README.md)。
- [docs/sources/configure/authentication.md](https://github.com/grafana/mcp-grafana/blob/e41b5962411b17e311a33006982815701c336bb9/docs/sources/configure/authentication.md)。
- [docs/sources/configure/transports-and-addresses.md](https://github.com/grafana/mcp-grafana/blob/e41b5962411b17e311a33006982815701c336bb9/docs/sources/configure/transports-and-addresses.md)。
- [LICENSE](https://github.com/grafana/mcp-grafana/blob/e41b5962411b17e311a33006982815701c336bb9/LICENSE)。
- [cmd/mcp-grafana/main.go](https://github.com/grafana/mcp-grafana/blob/e41b5962411b17e311a33006982815701c336bb9/cmd/mcp-grafana/main.go)。
- [caller_auth.go](https://github.com/grafana/mcp-grafana/blob/e41b5962411b17e311a33006982815701c336bb9/caller_auth.go)。
- [仓库 API](https://api.github.com/repos/grafana/mcp-grafana)、[发行 API](https://api.github.com/repos/grafana/mcp-grafana/releases?per_page=1)；动态字段只代表本轮采样。
- 事实依据为以上一手材料；价值、风险推论与补充建议为本库工程分析。
