<!-- markdownlint-disable MD013 -->

# sparkDash（MiaAI-Lab/sparkDash）中文解读

> 上游仓库：<https://github.com/MiaAI-Lab/sparkDash> · 归类：模型、训练与推理基础设施 · 本页基于 2026-10-12 的 README、Remote Access、Release、许可证与 GitHub REST API 静态整理；未连接 DGX Spark / GPU host、挂载 SSH key、运行 benchmark 或触发电源 / 更新动作。

## 定位

sparkDash 是面向 NVIDIA DGX Spark 及 Linux / Windows / macOS 计算节点的实时监控和轻量管理面。它聚合 GPU、CPU、统一内存 / VRAM、网络、存储、RoCE、LLM endpoint、ComfyUI、Hermes 与 fleet 能耗 / token 数据，并能从 UI 发起 benchmark、更新、取消任务和电源动作。

## 用法

项目以 Docker 为主要部署方式，默认只绑定 `127.0.0.1:5555`。远端节点通过 SSH、`nvidia-smi`、sysfs / proc 或 PowerShell 收集；外部访问应使用 SSH tunnel、带认证的反向代理或 Tailscale Serve。若明确绑定 `0.0.0.0`，上游要求配置 `SPARKDASH_TOKEN`，否则对远程 mutation 和 WebSocket fail closed。

## 原理

- 本机或 SSH collector 周期采集硬件、网络、存储与服务指标，经 WebSocket 推送 React dashboard。
- LLM probes 识别 llama.cpp、vLLM、SGLang、Ollama 等 endpoint，并读取它们公开的 counters / Prometheus metrics。
- decode、prefill、quality 与 tool-eval benchmark 从 Dashboard 发起并保存历史结果。
- 健康规则依据温度、内存、Xid / OOM、链路速率和 RoCE counters 生成可解释 finding。

## 价值

- 用一个界面观察小型 AI compute fleet、多个 LLM 服务和本地生成工作流。
- 将 TTFT、prefill / decode、queue、cache、能耗与硬件状态放在同一时间线上，便于定位明显瓶颈。
- 上游文档明确说明无认证 API、loopback、token 与 authenticated front door 的边界，便于安全部署。

## 风险边界

- Dashboard 包含 credential、benchmark、update、cancel 与 power controls；它不是只读监控面，误暴露可能直接影响主机和任务。
- Docker 需要较高主机可见性，SSH private key 会挂入容器；容器、密钥、host mounts 和 collector 命令必须作为高权限组件审计。
- AES-256-GCM 存储声明和默认 loopback 是机制，不证明 secrets key 管理、token rotation、WebSocket、反向代理或所有 API path 均无缺陷。
- health finding、quality score、tok/s 与能耗估计只覆盖实现的采样和规则，不能替代完整 observability、模型质量验收或硬件可靠性诊断。

## 补充建议

- 先在单台非生产节点以只读 SSH 账户试用，禁用更新 / power action，核对采样开销与指标语义。
- 使用专用 SSH key、最小 sudo、独立 secrets key、短期 token 与 authenticated proxy；不要把裸端口暴露到 LAN / Internet。
- 对 benchmark 固定模型 hash、runtime、并发、prompt set、温度和 cache 状态，并与独立命令行采样交叉验证。

## 参考资料

- GitHub 仓库：<https://github.com/MiaAI-Lab/sparkDash>
- GitHub REST API：<https://api.github.com/repos/MiaAI-Lab/sparkDash>
- `v2.32.0` Release：<https://github.com/MiaAI-Lab/sparkDash/releases/tag/v2.32.0>
- Remote access：<https://github.com/MiaAI-Lab/sparkDash/blob/main/docs/REMOTE-ACCESS.md>
- Program / architecture notes：<https://github.com/MiaAI-Lab/sparkDash/blob/main/docs/PROGRAM.md>
- CHANGELOG：<https://github.com/MiaAI-Lab/sparkDash/blob/main/CHANGELOG.md>
- LICENSE：<https://github.com/MiaAI-Lab/sparkDash/blob/main/LICENSE>
