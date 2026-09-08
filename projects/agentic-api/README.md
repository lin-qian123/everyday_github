<!-- markdownlint-disable MD013 MD034 -->

# agentic-api（vllm-project/agentic-api）

> 记录日期：2026-09-09（Asia/Shanghai）。本页依据上游 README、ROADMAP、release、LICENSE 与 GitHub REST API 做静态整理；本轮未编译 Rust 项目、未启动 vLLM、未接入 Codex / Claude Code，也未运行 Open Responses compatibility suite、性能或安全测试。

## 定位

`agentic-api` 是放在 vLLM 前方的 Rust stateful agentic API 层。它将 Responses API 会话状态、continuation、HTTP/SSE/WebSocket transport 与 server-side tool loop 从客户端移到 gateway，并为 Codex-shaped traffic、Claude Code、SQLite persistence 和 vLLM open-model serving 提供统一入口。

2026-09-09 的 GitHub 官方 Rust Trending 抓取显示约 `+22 stars today`；REST API 快照为 `232 stars / 62 forks / 67 open issues`，Apache-2.0；最新 release 为 `v0.5.0`（2026-08-25）。项目 roadmap 仍将 production storage、observability 与 cached-prefix continuation 列为后续 hardening，不应仅凭协议兼容就按成熟生产网关使用。

## 用法

上游给出的最小源码路径是先准备 vLLM，再启动 gateway：

```bash
cargo build -p agentic-server --bins
vllm serve Qwen/Qwen3-30B-A3B-FP8 \
  --tool-call-parser qwen3_coder --enable-auto-tool-choice \
  --reasoning-parser qwen3 --port 5050
cargo run -p agentic-server -- --llm-api-base http://127.0.0.1:5050
```

默认 gateway 使用 `localhost:9000`，数据库位于 `~/.agentic-api/agentic_api.db`。需要内置 web search 时还要配置 You.com endpoint / key。首次试用应限定 localhost、使用独立 `AGENTIC_API_HOME` 和假工具，不应直接暴露到共享网络。

## 原理

- **Responses API state**：以 response ID 与 `previous_response_id` 恢复多轮状态，避免客户端反复发送完整 transcript。
- **显式 tool ownership**：gateway-owned 工具在服务端执行，client-owned 原样返回给客户端，provider-owned 传给上游；未知形状默认不执行。
- **多 transport**：同时实现普通 HTTP、SSE streaming 与 WebSocket，适配不同 agent 客户端。
- **持久化与配置**：默认 SQLite 保存 response state；配置从 `~/.agentic-api/config.toml`、环境变量和 CLI 参数合并。
- **模型 / 编排分层**：vLLM core 负责推理，agentic-api 负责 state、continuation、tool execution 和更高层 API 语义。
- **兼容测试**：上游说明有 Open Responses 与 cassette 测试，但本页未运行，不能据此推出所有 provider/model/tool 组合等价。

## 价值

- 让客户端用一次 stateful API 调用委托多轮 tool loop，减少每个应用重复实现编排。
- 为 Codex / Claude Code 使用自托管 open models 提供较明确的协议与配置入口。
- tool ownership 把“谁执行工具”提升为一等语义，便于做 deny-by-default 和审计。
- Rust gateway 与 vLLM 推理层分离，允许独立演进状态、transport 和生产控制面。

## 风险边界

- Server-side tool execution 会把网络、MCP、文件检索等权限集中到 gateway；所有权标签只有在身份、参数校验、allowlist 和日志均正确时才有效。
- SQLite 会保存对话与工具状态；默认 home、Unix group-readable 配置、备份和删除策略都需要按敏感数据等级设计。
- 若 gateway 绑定非本地接口却未配置 OIDC / bearer auth，任意客户端可能调用模型、读取状态或触发工具。
- OpenAI-compatible 是 wire/API 目标，不证明 open model 的 reasoning、tool calling、safety、图像或 reasoning-effort 语义与某个闭源模型等价。
- Web search 依赖 You.com 外部服务，带来额外 key、数据出口、内容授权和 prompt-injection surface。
- Roadmap 明确 production hardening 尚未完成；67 个 open issues 与快速变化的接口要求版本固定和回滚。

## 补充建议

- 先以 mock vLLM 和无副作用工具做 contract suite，覆盖未知 tool shape、重复 continuation、断流、重试、取消与跨 transport 一致性。
- 为每个 gateway-owned tool 建独立身份、scope、timeout、egress allowlist、幂等与审计；client/provider-owned 工具也做 schema 验证。
- 将数据库、配置、模型缓存和日志放入独立加密卷，定义 retention、compaction、删除与 backup 恢复测试。
- 用固定模型、chat template、parser 和提示集同时测 tool-call 正确率、延迟、吞吐、成本和错误动作，不只测 HTTP 兼容。

## 参考资料

- GitHub 仓库：https://github.com/vllm-project/agentic-api
- GitHub REST API：https://api.github.com/repos/vllm-project/agentic-api
- README：https://github.com/vllm-project/agentic-api/blob/main/README.md
- ROADMAP：https://github.com/vllm-project/agentic-api/blob/main/ROADMAP.md
- `v0.5.0` release：https://github.com/vllm-project/agentic-api/releases/tag/v0.5.0
- LICENSE：https://github.com/vllm-project/agentic-api/blob/main/LICENSE
- vLLM：https://github.com/vllm-project/vllm
