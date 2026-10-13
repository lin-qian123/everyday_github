<!-- markdownlint-disable MD013 -->

# SGLang-Omni（sgl-project/sglang-omni）中文解读

> 上游仓库：<https://github.com/sgl-project/sglang-omni> · 归类：模型、训练与推理基础设施 · 本页基于 2026-10-14 的 README、router / topology / TTS 文档、Release、许可证与 GitHub REST API 静态整理；未占用 GPU、启动模型或复测吞吐、延迟和音频质量。

## 定位

SGLang-Omni 是面向 omni、ASR、TTS、音乐与全双工语音模型的多阶段 serving runtime。它管理预处理、encoder、autoregressive engine、talker、decoder、vocoder 与 aggregator 的拓扑、生命周期和传输，并复用 SGLang 处理适合自回归调度的阶段。

## 用法

上游推荐按模型 cookbook 安装 `sglang-omni==0.1.8`，再以对应 launcher 启动 Qwen3-Omni、Qwen3-ASR、MOSS、Fish Audio、Higgs Audio 等模型。API 覆盖 OpenAI-compatible chat、speech、transcription、batch、streaming 与 uploaded voices；NVIDIA CUDA 为完整支持，Apple Silicon 和 Intel XPU 仍标为实验路径。

## 原理

- 将一次生成拆成异构 stage，每个 stage 使用适合自身计算模式的 scheduler。
- control plane 协调请求；relay data plane 通过 shared memory、NCCL、NIXL 或 Mooncake 移动 tensor。
- process topology 可把 stage / replica 放到不同 GPU，也可使用 MPS 与可选权重共享。
- Rust router 提供多 worker 入口、admission、backpressure、health、readiness 与 realtime session relay。

## 价值

- 不把音频 / omni serving 简化成单一 text LLM server，显式表达 vocoder、talker 和流式阶段资源差异。
- 模型 cookbook、process topology、router 与 benchmark 命令较完整，便于按模型建立可复算部署基线。
- 同一接口覆盖 TTS、ASR、音频翻译与多模态输入输出，适合作为多模型 serving 对照平台。

## 风险边界

- Rust router 文档明确说明不实现客户端认证或 TLS termination，只能放在可信网络或经认证的 TLS proxy 后。
- “day-0 support”只证明存在适配路径，不证明模型质量、并发稳定性、版权、声纹授权或生产 SLA。
- 不同模型、codec、vocoder 与 CUDA / XPU / MPS backend 的许可、显存、质量和失败模式不同，不能由统一 API 推断一致性。
- voice cloning、uploaded voices 与长音频转录会处理生物特征和敏感内容；需明确同意、保留期、访问控制和滥用检测。

## 补充建议

- 每种模型固定 revision、GPU、precision、topology、chunk / codec 设置，分别记录首 token / 首音频延迟、实时率、吞吐、显存和失败率。
- 在反向代理处落实 mTLS / OIDC、请求大小、并发、超时、费用与审计；默认拒绝公网直接访问 router。
- 对 voice cloning 建立说话人授权、可撤销、标记与水印策略，并保留人工听评和 ASR / speaker similarity 的分开结果。

## 参考资料

- GitHub 仓库：<https://github.com/sgl-project/sglang-omni>
- GitHub REST API：<https://api.github.com/repos/sgl-project/sglang-omni>
- `v0.1.8` Release：<https://github.com/sgl-project/sglang-omni/releases/tag/v0.1.8>
- 文档：<https://sgl-project.github.io/sglang-omni/>
- Process topology：<https://github.com/sgl-project/sglang-omni/blob/main/docs/basic_usage/process_topology.md>
- Router security：<https://github.com/sgl-project/sglang-omni/blob/main/docs/basic_usage/omni_router.md#security-and-deployment>
- LICENSE：<https://github.com/sgl-project/sglang-omni/blob/main/LICENSE>
