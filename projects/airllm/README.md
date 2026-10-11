<!-- markdownlint-disable MD013 -->

# AirLLM（lyogavin/airllm）中文解读

> 上游仓库：<https://github.com/lyogavin/airllm> · 归类：模型、训练与推理基础设施 · 本页基于 2026-10-12 的 README、Release、示例、许可证与 GitHub REST API 静态整理；未下载超大模型、运行推理 / 训练或复测作者显存、速度和质量数据。

## 定位

AirLLM 通过逐层拆分、按需把权重从磁盘 / 主存流入 GPU，使显存较小的单卡也能执行超大模型推理；新版本还把冻结权重逐层流式载入、只把 adapter 留在 GPU，以支持低显存训练。它解决的是“模型权重同时驻留显存”的容量问题，不等于把模型总存储、主存、I/O 或计算成本消除。

## 用法

```bash
pip install airllm
```

Python 中用 `AutoModel.from_pretrained()` 指向 Hugging Face 仓库或本地 checkpoint，再按普通生成接口传入 token。首次使用会把模型拆成逐层文件；可设置 `layer_shards_saving_path`、`compression`、`prefetching` 与 `delete_original`。处理 gated 或带自定义代码的模型前，应先固定 revision、阅读模型卡并为 cache 预留足够磁盘。

## 原理

- 将 checkpoint 拆成 layer shards，推理时只把当前层送入 GPU，计算完成后再换入下一层。
- 通过 prefetch 重叠 I/O 与计算；4 / 8 bit block-wise 压缩主要缩小权重读取量。
- 针对 MoE 模型按路由加载被选中的 experts，以降低一次驻留量。
- 训练路径流式读取冻结权重，把可训练 adapter 与必要状态留在 GPU。

## 价值

- 让显存预算不足但磁盘 / 主存充足的研究者验证大模型接口和兼容性。
- 保留接近 Transformers 的调用方式，便于在现有脚本中做受控替换。
- 把显存、磁盘、吞吐、量化和模型许可之间的取舍暴露得较清楚。

## 风险边界

- README 的“70B / 125B / 2.8T 在少量显存运行”是作者环境数据；低显存不代表低延迟、高吞吐或低总成本，磁盘容量、主存、PCIe / 文件系统 I/O 仍可能成为瓶颈。
- `delete_original=True` 会删除原始 checkpoint；应先验证拆分文件完整、保留模型 revision 与可恢复副本。
- 仓库 Apache-2.0 不自动覆盖下载的模型、tokenizer、数据集或远端自定义代码；每个制品要单独核对许可与执行风险。
- 本页未复测压缩后的精度损失、不同 backend / GPU 的稳定性，也未证明 README 中未来模型名称和依赖组合可长期复现。

## 补充建议

- 从小模型、固定 prompt 与固定 commit 开始，分别记录 TTFT、tokens/s、峰值 GPU / CPU 内存、磁盘占用和生成质量。
- 在副本 cache 中先跑拆分与删除流程；校验 shard 数量、hash 和中断恢复，再考虑大 checkpoint。
- 固定 `transformers`、PyTorch、CUDA / MLX、模型 revision 与远端代码 revision，不使用浮动 `main` 做正式对比。

## 参考资料

- GitHub 仓库：<https://github.com/lyogavin/airllm>
- GitHub REST API：<https://api.github.com/repos/lyogavin/airllm>
- `v4.0.0` Release：<https://github.com/lyogavin/airllm/releases/tag/v4.0.0>
- 示例目录：<https://github.com/lyogavin/airllm/tree/main/examples>
- 训练代码：<https://github.com/lyogavin/airllm/tree/main/training>
- LICENSE：<https://github.com/lyogavin/airllm/blob/main/LICENSE>
