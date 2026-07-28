# jaxotron

## 定位

`jaxotron` 是一个纯 JAX + Equinox 的极简 LLM 训练器，覆盖数据并行、FSDP、张量并行、梯度累积、muP、WandB 和 Orbax checkpoint，定位为可阅读的 3D 并行训练参考实现。

截至 2026-07-29，GitHub API 显示其创建于 2026-07-28，约 13 stars，采用 Apache-2.0；它是早期实验项目，不是已验证的大规模训练平台。

## 用法

先按硬件安装 JAX、Equinox、Optax、Orbax 等依赖，再运行仓库示例；README 表示示例会生成小型 dummy 二进制数据并按可见设备数配置 mesh。

```bash
pip install "jax[cuda12]" equinox optax orbax-checkpoint wandb numpy torch
python app.py
```

开始真实训练前，把 tokenized 数据、`dp * fsdp * tp` 与 global/micro batch 显式写入配置，并用一个节点的恢复测试验证 checkpoint。

## 原理

训练器以命名 mesh 划分数据、全分片和张量轴；mmap 读取扁平 token 文件，以 `jax.lax.scan` 实现梯度累积，并将模型/优化器状态交给 Orbax 异步保存。muP 选项用于把小模型上的超参探索迁移到更大宽度/深度，但其有效性取决于具体架构与训练设置。

## 价值

- 将常见分布式训练部件浓缩在较小代码面，适合学习和做受控实验。
- 明确展示 3D 并行轴与 batch 关系，便于在 GPU/TPU 环境建立最小可运行基线。

## 风险边界

- README 中的规模配置是说明性示例，未构成吞吐、收敛、数值稳定性或 fault tolerance 的独立 benchmark。
- JAX、CUDA/TPU runtime、驱动与 mesh 拓扑的版本组合很敏感；多节点必须另做通信与恢复演练。
- mmap 数据格式、tokenizer、许可证与训练数据治理均由使用者负责。

## 补充建议

从单设备 toy run、固定随机种子与 loss 对照开始；每增加一个并行轴就记录 tokens/s、显存和恢复一致性，并将 checkpoint restore 纳入 CI 或集群预飞检查。

## 参考资料

- GitHub：<https://github.com/rishiraj/jaxotron>
- GitHub API 快照：<https://api.github.com/repos/rishiraj/jaxotron>
