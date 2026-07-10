# Hy3

<!-- markdownlint-disable MD013 -->

## 定位

`Hy3` 是腾讯混元团队开源的 MoE 大模型仓库。README 描述其为 295B 总参数、21B 激活参数、256K 上下文的推理和 agent 模型，并提供 Hy3 与 Hy3-FP8 权重入口。项目重点强调 agent 能力、工具调用可靠性、长上下文、多轮意图跟踪和产品场景稳定性。

截至 2026-07-11，GitHub API 显示该仓库约 422 stars，创建于 2026-07-02，主要语言为 Python。它适合归入“模型、训练与推理基础设施”，是近期国产开放权重模型在 agentic engineering 方向继续竞争的信号。

## 用法

仓库建议先通过 vLLM 或 SGLang 部署，再调用 OpenAI-compatible API。README 给出的 vLLM 启动方式包括启用 MTP、tool-call parser、reasoning parser 和 auto tool choice：

```bash
vllm serve tencent/Hy3 \
  --tensor-parallel-size 8 \
  --speculative-config.method mtp \
  --speculative-config.num_speculative_tokens 2 \
  --tool-call-parser hy_v3 \
  --reasoning-parser hy_v3 \
  --enable-auto-tool-choice \
  --port 8000 \
  --served-model-name hy3
```

Python 调用走 OpenAI SDK 的 `base_url`，并可通过 `reasoning_effort` 控制回答模式。

## 原理

Hy3 采用 Mixture-of-Experts 架构，总参数 295B，激活参数 21B，192 个 experts，top-8 activated，支持 BF16 和 256K context。README 称该模型在 Hy3 Preview 后收集了 50+ 产品反馈，并扩展高质量 post-training 与 RL 训练。

项目特别强调工具调用稳定性、输出格式约束、tool-call error recovery、长对话指代和多轮约束继承。官方还给出内部专家盲测、幻觉率下降、多轮问题率下降等产品侧指标，但这些仍需要第三方复测。

## 价值

- 提供一个大上下文、agent 友好的开放权重模型选项。
- 支持 vLLM / SGLang 部署，便于接入现有推理服务栈。
- Hy3-FP8 权重降低了部分部署门槛。
- 对工具调用和输出格式的强调，贴近 coding agent、办公 agent、金融建模和前端生成等真实应用。

## 风险边界

- 295B 总参数模型部署成本很高，README 建议 8 GPU 且需要大显存设备。
- GitHub API 对许可证返回 `NOASSERTION`，虽然 README 标注 Apache 2.0，生产使用前仍应核对模型权重许可条款。
- 官方 benchmark、内部专家评分和幻觉率指标需要第三方复测。
- 工具调用稳定性依赖 parser、serving 后端和 agent scaffold，不应只看模型仓库结论。

## 补充建议

- 与 `GLM-5`、`Qwen`、`DeepSeek`、`local-llm`、`Rapid-MLX` 一起跟踪国产 agentic 模型生态。
- 若用于本地 agent，优先验证工具调用、长上下文检索、JSON 输出和多轮任务继承，而不是只跑通聊天 demo。
- 对成本敏感团队可先测试 Hy3-FP8、SGLang/vLLM serving 指标和实际吞吐。

## 参考资料

- GitHub 仓库：<https://github.com/Tencent-Hunyuan/Hy3>
- Hugging Face 权重：<https://huggingface.co/tencent/Hy3>
- ModelScope 权重：<https://modelscope.cn/models/Tencent-Hunyuan/Hy3>
- vLLM：<https://github.com/vllm-project/vllm>
- SGLang：<https://github.com/sgl-project/sglang>
