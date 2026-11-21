<!-- markdownlint-disable MD013 -->

# torchtitan

## 定位

TorchTitan 是 PyTorch 原生的大模型训练平台，用可读的 Python recipe 组合预训练、监督微调和 TitanRL 强化学习，面向研究与分布式训练工程。它提供训练代码和并行机制，不提供已经验收的模型效果或现成算力。

- 上游：[pytorch/torchtitan](https://github.com/pytorch/torchtitan)，仓库 ID `730932260`。
- 2026-11-22（Asia/Shanghai）07 时段：官方 Python daily **+8**；API stars / forks / open issues（含 PR）为 **5,938 / 1,095 / 509**。[API](https://api.github.com/repos/pytorch/torchtitan)
- 最新核到非预发行版 [v0.4.0](https://github.com/pytorch/torchtitan/releases/tag/v0.4.0)，UTC 2026-10-28 发布；本页主干快照固定为 `b62add8a227de83a855ba63b27f6ceb4252949f4`，两者分开使用。
- 分类：`模型、训练与推理基础设施`。本轮首次建档，仅抽读文档、配置与启动脚本，未安装依赖、申请 GPU 或运行训练。

## 用法

先选择稳定版或主干，再固定 PyTorch、TorchAO、CUDA / ROCm、硬件和 recipe。当前主干要求 Python 3.11+，README 建议近期 PyTorch nightly；不能把主干安装说明直接套到 v0.4.0。

主干最小示例，以下未执行；`cu132` 需换成目标硬件匹配的构建：

```bash
git clone https://github.com/pytorch/torchtitan
cd torchtitan
git checkout b62add8a227de83a855ba63b27f6ceb4252949f4
python -m pip install --pre torch --index-url https://download.pytorch.org/whl/nightly/cu132
python -m pip install -r requirements.txt
NGPU=1 ./run_train.sh
```

固定脚本默认 `NGPU=8`，因此单卡调试必须显式设 `NGPU=1`；默认 recipe 是 `llama3_debugmodel`，配置为 10 步并使用测试 tokenizer。这是小模型链路检查，不是正式模型收敛或性能证明。[启动脚本](https://github.com/pytorch/torchtitan/blob/b62add8a227de83a855ba63b27f6ceb4252949f4/run_train.sh)、[调试 recipe](https://github.com/pytorch/torchtitan/blob/b62add8a227de83a855ba63b27f6ceb4252949f4/torchtitan_recipes/tests/models/llama3.py)

正式任务通过 `MODULE=模块 CONFIG=函数 ./run_train.sh` 选择返回完整配置的 Python 函数；改变行为优先修改 recipe。`NGPU` 要与并行布局相符，模型配置也须按序列长度和 expert parallelism 等重新构造；`--output-dir`、`--resume-step` 属于保留的运行选项。[配置指南](https://github.com/pytorch/torchtitan/blob/b62add8a227de83a855ba63b27f6ceb4252949f4/torchtitan/config/README.md)

## 原理

模型在 DeviceMesh / DTensor 上声明分片，组合 FSDP2、张量、流水线、上下文和专家并行；recipe 决定模型、优化器、数据与并行布局。TitanRL 复用训练和生成的模型定义，并为 trainer / vLLM generator 的 logprob 一致性提供专门模式。[固定 README](https://github.com/pytorch/torchtitan/blob/b62add8a227de83a855ba63b27f6ceb4252949f4/README.md)

批次组成改变时，GEMM、attention 与 collective 的求和顺序可能改变舍入，MoE 路由还可能放大差异。batch-invariant 模式同时要求 trainer / generator 开启相应调试选项，替换部分算子、固定 attention 切分及 NCCL 归约配置；它是有适用条件的数值路径，不能推广成任意后端、模型和拓扑的逐位一致。[机制与限制](https://github.com/pytorch/torchtitan/blob/b62add8a227de83a855ba63b27f6ceb4252949f4/torchtitan/rl/BITWISE_PARITY.md)

## 价值

- 适合阅读和修改分布式训练机制，把消融条件放在可追踪的 recipe 中，减少隐含命令行状态。
- 提供预训练、SFT、RL 与 checkpoint 的共同结构，便于研究训练 / 生成差异和恢复行为。
- 上游明确区分 CI debug 配置与经过训练、收敛或性能工作流的 verified recipes；“列出模型”不表示其所有功能组合均验证。

## 风险边界

- **复现条件。** 固定数值文档要求两端 BF16 计算、匹配的 tensor parallel degree；batch-invariant 模式不支持 sequence parallelism。零 logprob 差异只说明相应比较一致，不证明奖励、训练目标或任务能力正确。
- **性能分母。** 上游 Qwen3-8B / Search-R1、8×H100、TP2 / TP2、30 步报告中，开启后 generator ITL 中位数 `9.6 → 22.8 ms`，trainer 前反向 `370 → 127 tok/s`，但整步 `136.4 → 133.6 s`。作者解释检索、调度与同步掩盖计算变慢；不能写成确定性普遍“免费”，也不能把这组近似持平数据当作加速实验。本轮未复跑。
- **导出不等于恢复点。** 最终 model-only 保存位于 `exports/`，不能恢复完整训练；自动恢复只考虑完整的 `step-N`。已有有效 checkpoint 时可能优先恢复它，忽略另设的初始权重路径。[checkpoint 文档](https://github.com/pytorch/torchtitan/blob/b62add8a227de83a855ba63b27f6ceb4252949f4/torchtitan/components/checkpointer/README.md)
- **版本与硬件。** v0.4.0 移除若干旧路径，MXFP8 要求相应 TorchAO nightly，NVFP4 等还有限定硬件与依赖；主干新增功能不自动属于稳定版。[发行说明](https://github.com/pytorch/torchtitan/releases/tag/v0.4.0)
- **数据与指标。** 权重、数据、tokenizer 各有许可和下载要求；开启 W&B 等外部 logger 需核数据出口。W&B 的 `_step` 是日志调用序号，训练横轴应核 `trainer/step`。[指标说明](https://github.com/pytorch/torchtitan/blob/b62add8a227de83a855ba63b27f6ceb4252949f4/torchtitan/observability/METRICS.md)
- **许可。** 根代码为 BSD-3-Clause；模型权重和数据不随代码许可一并授权。[LICENSE](https://github.com/pytorch/torchtitan/blob/b62add8a227de83a855ba63b27f6ceb4252949f4/LICENSE)

## 补充建议

先完成单卡 10 步、有限 loss、完整 checkpoint / 恢复的检查，再扩展并行维度。保存 SHA、依赖、recipe、硬件拓扑、数据顺序和失败样本；性能分别记录编译、数据加载、计算、通信和整步时间。复现 RL 一致性时，同时保留 logprob 差异、任务指标与吞吐，不只截取一个零值或最佳速率。

## 参考资料

- [固定 README](https://github.com/pytorch/torchtitan/blob/b62add8a227de83a855ba63b27f6ceb4252949f4/README.md)、[包元数据](https://github.com/pytorch/torchtitan/blob/b62add8a227de83a855ba63b27f6ceb4252949f4/pyproject.toml)、[配置指南](https://github.com/pytorch/torchtitan/blob/b62add8a227de83a855ba63b27f6ceb4252949f4/torchtitan/config/README.md)。
- [数值一致性与限定性能样本](https://github.com/pytorch/torchtitan/blob/b62add8a227de83a855ba63b27f6ceb4252949f4/torchtitan/rl/BITWISE_PARITY.md)、[checkpoint](https://github.com/pytorch/torchtitan/blob/b62add8a227de83a855ba63b27f6ceb4252949f4/torchtitan/components/checkpointer/README.md)、[v0.4.0](https://github.com/pytorch/torchtitan/releases/tag/v0.4.0)。README 所链论文留作后续深读，本轮未阅读全文或独立复现。
