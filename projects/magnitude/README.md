<!-- markdownlint-disable MD013 MD034 -->

# Magnitude：为本机硬件选择并托管 Agent 本地模型的推理服务

## 项目概览

- 上游仓库：https://github.com/magnitudedev/magnitude
- GitHub API 快照（2026-09-04）：1,921 stars、142 forks、13 个开放 issue
- 当前 release：`@magnitudedev/cli@0.0.11`
- 主要技术：TypeScript CLI、本地 inference server、GGUF、OpenAI-compatible 接入、硬件探测与模型目录
- 许可证：Apache-2.0

## 定位

Magnitude 面向已经使用 Pi、OpenCode、Hermes、OpenClaw、Codex、Claude Code、Cline 等 harness 的开发者：它探测本机芯片、内存和带宽，推荐可放入当前硬件的本地模型，并协助下载、调优、启动和改写宿主配置。

它解决的是本地模型选择与服务接入，不会自动让小模型达到云端大模型质量，也不是对宿主工具权限的安全隔离层。

## 用法

官方入口是全局安装 CLI，再让 agent 读取 onboarding 文档：

```bash
npm install -g @magnitudedev/cli
magnitude docs onboarding
```

交互式 `magnitude setup` 可浏览推荐模型。上游支持 macOS、Linux 和 WSL；模型与服务下载完成后可离线运行，也允许从 Hugging Face 下载兼容 GGUF 模型。

首次使用宜先打印计划和目标配置，记录将修改的 provider/base URL、模型 ID、后台服务与缓存目录，再在无敏感仓库验证。

## 原理

Magnitude 建立硬件 profile，将可用内存、带宽和芯片信息映射到模型与量化目录，给出拟合度和估计 tokens/s。选择模型后，CLI 下载权重、配置推理参数和并发策略，并让现有 agent 通过本地兼容端点调用。

服务会按请求加载模型，在空闲或内存紧张时卸载。所谓“best models”和速度均来自上游目录与估计逻辑，仍依赖具体模型 revision、量化、上下文长度、并发和硬件散热。

## 价值

- 把硬件探测、模型筛选、下载和 harness 接入整合成一条本地工作流。
- 避免用户只按参数量猜测模型能否装入内存。
- 兼容多种 agent harness，降低重复配置 provider 的成本。
- 本地推理可减少按 token 计费，并为离线场景提供入口。

## 风险边界

- “free/private/offline”是本地推理拓扑的上游主张；npm、模型下载、更新、外部工具和原 harness 仍可能联网。
- 自动改写 harness 配置可能影响默认 provider、模型名、上下文长度和已有工作流，必须保留备份与回滚。
- 估计 tok/s 不能替代固定 prompt、上下文、并发与功耗条件下的实测，也不代表任务质量。
- GGUF 权重、模型代码、数据来源和许可证需逐模型审查，不能由 Apache-2.0 的服务器许可证覆盖。
- 后台服务、本地端口和模型缓存仍需访问控制、磁盘配额与日志治理。
- 本页依据上游 README、release 与 API，未安装，也未跑本地性能或质量评测。

## 补充建议

1. 先固定一个模型 revision、量化和 20--50 条真实任务，在同一硬件测 TTFT、tok/s、内存、功耗和成功率。
2. 安装前后 diff agent 配置，确认 base URL、API key、上下文长度与回退模型均可恢复。
3. 用网络监测区分首次下载、更新检查、模型推理和 agent 外部工具的实际出口。
4. 给模型缓存设容量和清理策略，并验证模型卸载、OOM、崩溃重启与并发退化。
5. 将本地模型用于风险可控任务；后果性代码、密钥和外部动作仍保留人工 gate。

## 参考资料

- 仓库与 README：https://github.com/magnitudedev/magnitude
- Releases：https://github.com/magnitudedev/magnitude/releases
- 官方站点：https://magnitude.dev/
- 官方文档：https://docs.magnitude.dev/
- npm 包：https://www.npmjs.com/package/@magnitudedev/cli
