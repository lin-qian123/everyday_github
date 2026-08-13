<!-- markdownlint-disable MD013 -->

# Switchyard

> NVIDIA NeMo 的预览期 LLM 流量代理与 Rust 库：在 OpenAI Chat/Responses、Anthropic Messages 等接口之间转换，并按策略路由到多个模型或 provider。

- 上游仓库：[NVIDIA-NeMo/Switchyard](https://github.com/NVIDIA-NeMo/Switchyard)
- 许可证：Apache-2.0
- 本轮快照：2026-08-14，GitHub REST API 约 `1.2k` stars、`107` forks；GitHub Trending 页面抓取时显示约 `408` stars/day。以上计数会随时间变化。
- 分类：模型、训练与推理基础设施

## 定位

Switchyard 是位于 LLM client 与多种模型后端之间的路由层。它以 Rust proxy 和可嵌入库两种方式，提供 OpenAI/Anthropic 协议转换、多后端选择、信号驱动路由、A/B benchmark 与 Prometheus 指标；上游示例将 Claude Code、Codex 和 OpenClaw 接到 OpenRouter、vLLM、NVIDIA NIM、Ollama 或兼容端点。项目明确处于 pre-alpha，API 和算法可能发生大幅变化。

## 用法

先在隔离环境安装、核验配置，再指向本地或已批准的 provider。上游的 standalone server 路径为：

```bash
cargo install --locked switchyard-server
switchyard-server --config routes.toml --dry-run
switchyard-server --config routes.toml --host 127.0.0.1 --port 4000
curl http://localhost:4000/health
```

若使用已发布的 CLI，README 给出了 `uv tool install --python 3.10 "nemo-switchyard[cli]"`，随后以 `switchyard launch codex --model <route>` 启动客户端的方式。密钥不应写入 `routes.toml` 或提交到仓库；先使用无敏感测试提示词验证协议、工具调用和流式响应，再接入真实工作流。

## 原理

1. 客户端按其原生 OpenAI 或 Anthropic 格式发送请求；
2. 代理执行协议转换，并依照随机、分类器、信号阶段路由或自定义算法选择目标；
3. 请求被发往 vLLM、NIM、Ollama、OpenRouter 或其他兼容后端，结果再转回客户端格式；
4. Prometheus 指标记录请求、错误、延迟、token 与路由开销，供比较模型与策略。

它解决的是接口与选择层的可替换性，不会自动使不同模型的工具语义、数据政策、速率限制或安全行为一致。

## 价值

- 可让既有 agent 保持原生 API 使用习惯，同时试验自托管或多 provider 后端。
- 将成本、延迟、错误和路由决策放入同一观测面，便于做明确条件下的 A/B 比较。
- Rust server 与库模式分别适合独立网关和嵌入既有 runtime，减少一次性绑定单一模型服务。

## 风险边界

- 路由代理会接触提示词、工具参数、响应及 provider 凭据；必须限制监听地址、加密传输、日志脱敏与密钥存储，且逐一审阅每个上游的数据政策。
- 协议兼容不保证所有消息格式、流式事件、函数调用或安全策略等价；升级模型或 provider 后需回归测试关键 agent 路径。
- 自动选择“较便宜/较快”模型可能降低输出质量、泄露数据到不合适端点或突破预算；高风险任务应固定允许的模型和人工确认门。
- 上游标注 pre-alpha，不应直接作为生产控制面；需明确版本锁定、回滚、超时、熔断与故障降级策略。

## 补充建议

- 先仅绑定 `127.0.0.1`，为每条 route 设 allowlist、成本上限、超时、失败回退与无敏感 health-check。
- 用固定的提示词、工具调用和长流式响应集测量质量、TTFT、总延迟、错误率和实际账单，避免只比较单次演示。
- 将路由决策与原始请求分开留存；对 logs 建立脱敏、保留期和访问审批，生产发布前完成威胁建模。

## 参考资料

- [项目 README：Quick Start、协议与路由说明](https://github.com/NVIDIA-NeMo/Switchyard#readme)
- [Getting Started 文档](https://github.com/NVIDIA-NeMo/Switchyard/blob/main/docs/getting_started.md)
- [GitHub 仓库元数据](https://api.github.com/repos/NVIDIA-NeMo/Switchyard)
- [GitHub Trending 观察入口](https://github.com/trending)
