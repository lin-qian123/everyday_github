# vLLM（vllm-project/vllm）

- GitHub: https://github.com/vllm-project/vllm
- 记录日期: 2026-04-27 (Asia/Shanghai)

## 这是什么

`vLLM` 是高吞吐 LLM 推理与服务框架，重点解决“模型服务化后的并发效率”问题。它在生产环境常用于降低延迟与提升吞吐，是推理层常见核心组件。

## 热度信号

1. OSSInsight AI Trending Top 50（2026-04-27 抓取）排名第 14，约 `56,694 stars`，近 28 天增长 `+541`。
2. 在企业推理栈里，vLLM 与模型路由/网关组合出现频率很高。

## 怎么用（最短路径）

### 1) 安装并启动 OpenAI 兼容服务

```bash
pip install vllm
python -m vllm.entrypoints.openai.api_server --model Qwen/Qwen3-8B
```

### 2) 使用 OpenAI 兼容调用

- 让现有应用通过兼容接口直接接入 vLLM 服务。

### 3) 做压测再上线

1. 准备真实请求分布。
2. 对比不同并发下延迟、吞吐、显存。
3. 再决定批处理和并行参数。

## 核心原理

1. 高效注意力与 KV Cache 管理，减少资源浪费。
2. 动态批处理提升吞吐。
3. 统一服务接口降低接入成本。

## 适用场景

1. 自建 LLM API 服务。
2. 高并发问答/Agent 后端。
3. 需要成本优化的企业推理集群。

## 价值与风险

价值：
- 在相同硬件上提升可服务请求量。
- 兼容接口便于迁移既有应用。

风险：
- 参数调优复杂，不同模型差异明显。
- 峰值并发下若无限流，尾延迟可能恶化。

## 我认为有价值的补充材料

1. 建立“模型-配置”基准表，不同模型独立调参。
2. 在网关层做超时/重试/熔断，避免雪崩。
3. 把监控重点放在 `P95/P99` 与显存抖动，而不是平均值。

## 参考来源

- https://github.com/vllm-project/vllm
- https://ossinsight.io/trending/ai
