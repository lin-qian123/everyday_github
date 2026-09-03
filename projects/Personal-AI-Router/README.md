<!-- markdownlint-disable MD013 MD034 -->

# NVIDIA PAIR：在家庭局域网多设备间路由本地推理请求

## 项目概览

- 上游仓库：https://github.com/NVIDIA/Personal-AI-Router
- GitHub API 快照（2026-09-04）：66 stars、6 forks、0 个开放 issue
- 当前 release：`v0.1.1`
- 主要技术：Go services、Electron desktop、Ollama / LM Studio、OpenAI-compatible / Ollama-compatible proxy、mTLS、LAN discovery
- 许可证：Apache-2.0；推理引擎和模型另有各自条款

## 定位

NVIDIA Personal AI Router（PAIR）在同一局域网的 Windows、Linux 与 macOS 节点间分发相互独立的本地推理请求。它发现节点和模型，管理 Ollama / LM Studio，并向应用与 agents 暴露兼容 proxy endpoint。

PAIR 不是多 GPU 内存池、模型并行或单请求分片系统：每个请求只送到一个拥有目标模型且引擎可用的节点。它在本轮依据 NVIDIA 2026-09-03 官方发布说明收录，不是 GitHub Trending 日增星项目。

## 用法

官方推荐从 release 安装签名桌面包，启动后安装/发现 Ollama 或 LM Studio、下载模型，再让本机应用调用 loopback endpoint。第二台机器通过六位 PIN 配对后加入 cluster。

```bash
curl http://127.0.0.1:11434/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{"model":"qwen4:12b","messages":[{"role":"user","content":"What does a router do?"}]}'
```

真实部署前应先阅读 architecture 与 security 文档，并在可信、隔离的 LAN 用非敏感 prompt 测试。

## 原理

每台节点运行相同服务，可同时接收本地请求和为 peer 提供推理。Proxy 根据模型 inventory 先做资格过滤，再按人工 pin、scheduler 优先级和稳定 node ID 形成 failover 列表。Scheduler 结合 pending work 与分段平滑的 GPU utilization 排序。

本地 client 通过 loopback plaintext HTTP；cluster inference 与多数控制流量使用配对证书的 mTLS。六位 PIN 只用于初始信任 bootstrap，部分 discovery、host/GPU telemetry 仍是局域网明文且未认证。

## 价值

- 复用家庭/工作室中多台已有设备，让并发 agents 把独立请求分散到可用节点。
- 兼容 Ollama、LM Studio 与常见 API 形状，减少上层 harness 改造。
- 支持混合操作系统和不同模型 inventory，不要求所有节点完全相同。
- 架构与 security 文档明确列出 mTLS、loopback、PIN 和 telemetry 边界，便于审计。

## 风险边界

- PAIR 不合并 VRAM、不切分模型或单次请求；只有复制到多节点的同一模型才有负载均衡空间。
- 六位 PIN 熵低，只是可信网络上的配对便利；被攻陷的已配对节点仍在信任边界内。
- 未认证 telemetry 可让同子网主体读取 hostname、硬件 inventory 和 utilization；共享 Wi-Fi 不宜直接使用。
- “local-first”不证明完全离线：模型目录、engine、更新系统、上层应用和配置仍可能访问外网。
- 本地 proxy、Electron IPC、worker、日志、cluster key 和模型管理继承当前 OS 用户权限；mTLS 不覆盖全部本地表面。
- 上游博客的五 subagent 8:48 对单机 18:00 是特定三设备演示，不应外推为通用加速比。
- 本页只做静态核验，未安装、配对节点或重放性能演示。

## 补充建议

1. 在独立 VLAN/可信 LAN 用两台测试机验证配对、member removal、证书轮换、节点掉线和 failover。
2. 抓包确认哪些 discovery/telemetry 是明文，按资产敏感度配置防火墙与网络隔离。
3. 用固定模型、相同 prompt、并发梯度和异构节点报告吞吐、TTFT、失败率、能耗与调度偏斜。
4. 检查 Ollama/LM Studio 的监听地址、模型许可证、更新源和日志，不把 PAIR 的 Apache-2.0 覆盖到它们。
5. 对外部 agent 保留工具权限、凭据和后果性动作 gate；推理路由不提供 agent sandbox。

## 参考资料

- 仓库与 README：https://github.com/NVIDIA/Personal-AI-Router
- Releases：https://github.com/NVIDIA/Personal-AI-Router/releases
- NVIDIA 官方发布说明：https://developer.nvidia.com/blog/nvidia-pair-virtual-inference-router-expands-available-compute-on-your-local-network/
- 架构文档：https://github.com/NVIDIA/Personal-AI-Router/blob/main/docs/architecture.mdx
- Security policy：https://github.com/NVIDIA/Personal-AI-Router/blob/main/SECURITY.md
- Getting started：https://github.com/NVIDIA/Personal-AI-Router/blob/main/docs/getting-started.mdx
