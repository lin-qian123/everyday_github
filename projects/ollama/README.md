# ollama（ollama/ollama）

- GitHub: https://github.com/ollama/ollama
- 记录日期: 2026-04-28 (Asia/Shanghai)

## 这是什么

`ollama` 是本地大模型运行与分发平台。它把“模型下载、推理运行、API 暴露”合并成一条可落地路径，常作为本地 AI 开发栈的推理底座。

## 热度信号

1. OSSInsight AI Trending Top 50（2026-04-28 抓取）排名第 2。
2. 仓库约 `147,487 stars`，近 28 天增长 `+754`。

## 怎么用（最短路径）

### 1) 启动服务

```bash
ollama serve
```

### 2) 拉取并运行模型

```bash
ollama pull qwen3
ollama run qwen3
```

### 3) 对外提供接口

- 默认本地 HTTP 接口可直接被 WebUI、Agent、RAG 服务调用。

## 核心原理

1. 模型制品化：把模型与运行参数组织成可复用制品。
2. 本地推理调度：处理加载、缓存、会话与资源分配。
3. 统一 API 层：让上层应用与模型实现解耦。

## 适用场景

1. 本地私有化助手。
2. 离线或弱网环境下的推理服务。
3. 企业内部 PoC 的低成本验证。

## 价值与风险

价值：
- 部署路径短，适合快速搭建本地 AI 基础设施。
- 数据可留在本地，隐私可控。

风险：
- 模型切换与性能调优有门槛。
- 本地资源不足时，吞吐与稳定性会明显下降。

## 我认为有价值的补充材料

1. 固定一套基准压测任务（延迟、吞吐、准确率）再切模型。
2. 给推理节点做显存/CPU 监控，避免“能跑但不稳定”。
3. 与 `open-webui`/`ragflow` 组合验证完整链路，而不只测单点推理。

## 参考来源

- https://github.com/ollama/ollama
- https://ossinsight.io/trending/ai
