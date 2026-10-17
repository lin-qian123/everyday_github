<!-- markdownlint-disable MD013 -->

# Bonsai Demo（PrismML-Eng/Bonsai-demo）中文解读

> 上游仓库：<https://github.com/PrismML-Eng/Bonsai-demo> · 归类：模型、训练与推理基础设施 · 证据快照：2026-10-18（Asia/Shanghai）。认证 API：3,393 stars / 382 forks / 21 open issues；无 GitHub Release / tag；演示代码 Apache-2.0，已读 27B GGUF 模型卡标 Apache-2.0。本页为上游材料及所列源码的静态整理，未安装运行、复测 benchmark 或完成全面安全审计。

## 定位

Bonsai-demo 是 Bonsai 本地模型的安装与运行入口，当前默认 Bonsai 2 27B，另有 2B / 4B / 9B、GGUF / MLX 路径，支持聊天、视觉与工具调用。它不是单一格式或单一二进制：权重 packing、模型代际、后端与驱动版本共同决定能否运行。

## 用法

先读 BACKEND-SUPPORT 和对应模型卡，记录硬件与内存预算。README 路线为 clone 后执行 `./setup.sh`，再 `./scripts/start_llama_server.sh`；默认会下载约 7.8GB 的 27B PQ2_0 权重及视觉 projector，并安装 Open WebUI / code interpreter 等额外组件。最小试验可先设置 `BONSAI_MODEL=4B`、`BONSAI_OPENWEBUI=0`、`BONSAI_CODE_INTERPRETER=0`。本轮没有下载模型或启动服务。

## 原理

Bonsai 2 用低比特 / ternary 权重表示，并包含 Hadamard 等模型图变换；PTQ1_0、PQ2_0、Q2_0 是不同 packing。当前支持相应集成的 upstream llama.cpp 可运行 Q2_0，而 PQ2_0 / PTQ1_0 仍需 PrismML fork；演示默认取 fork。MLX 路径另有固定依赖和模型格式，不能只换文件扩展名。

## 价值

降低权重体积可扩大本机实验范围，公开的后端矩阵和社区测量模板有助于复现。作者称 27B 保留 98.2% 基准平均表现、特定硬件有较快生成；这些指标需结合任务、采样、prefill、长上下文、视觉和工具正确率评估，不能概括为保留等比例的全部智能。

## 风险边界

- 权重大小不是总 RAM / VRAM：KV cache、视觉塔、上下文、临时缓冲和后端转换均占资源。PTQ1_0 在部分 SYCL 路径扩展为更大布局，小文件不保证更低 GPU 内存。
- 支持表明确是源码状态，部分设备 / 驱动仍需验证；指定 Intel Windows Vulkan 驱动范围有 fallback，SYCL 不由 setup 自动选择。下载模型不能修复旧引擎。
- server 脚本默认绑定 127.0.0.1；改成公网 / 局域网地址后不能假定已有认证。MCP 按聊天 opt-in，启用后会调用远端服务；code interpreter 和工具会增加执行能力与数据出口。
- setup 会联网取权重、二进制和依赖，本地推理不是离线安装保证。已读 27B GGUF 模型卡许可不应外推全部尺寸、视觉组件和依赖。

## 补充建议

先用最小模型和固定 prompt，在相同硬件分别记录冷启动、prefill、tokens/s、峰值内存、正确率与失败日志；固定模型 hash、后端 release 和有效启动参数。逐一加入视觉 / MCP，验证工具回合和出站记录，再测试长上下文及代码解释器。

## 参考资料

- 上游仓库：<https://github.com/PrismML-Eng/Bonsai-demo>
- GitHub REST API：<https://api.github.com/repos/PrismML-Eng/Bonsai-demo>
- README / 默认下载与模型选择：<https://github.com/PrismML-Eng/Bonsai-demo/blob/main/README.md>
- 后端与发布基线：<https://github.com/PrismML-Eng/Bonsai-demo/blob/main/BACKEND-SUPPORT.md>
- Packing 定义：<https://github.com/PrismML-Eng/Bonsai-demo/blob/main/MODEL-FORMATS.md>
- 安装脚本：<https://github.com/PrismML-Eng/Bonsai-demo/blob/main/setup.sh>
- server 监听默认值：<https://github.com/PrismML-Eng/Bonsai-demo/blob/main/scripts/start_llama_server.sh>
- 工具调用与 MCP opt-in：<https://github.com/PrismML-Eng/Bonsai-demo/blob/main/TOOLS.md>
- 27B GGUF 模型卡：<https://huggingface.co/prism-ml/Ternary-Bonsai-2-27B-gguf>
- 演示代码许可：<https://github.com/PrismML-Eng/Bonsai-demo/blob/main/LICENSE>
