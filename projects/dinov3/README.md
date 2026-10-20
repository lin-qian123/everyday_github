<!-- markdownlint-disable MD013 -->

# DINOv3

> 更新：2026-10-21（Asia/Shanghai）。分类：模型、训练与推理基础设施。上游 `facebookresearch/dinov3`；快照 `6876159a11b4`（main）。本文为官方资料与源码静态研究；热度、发行时间及社媒限制见[当日日报](../../daily/2026-10-21/ai-hotspots.md)。

## 定位

Meta FAIR 的自监督视觉特征模型与 PyTorch 参考实现，包含 ViT / ConvNeXt backbone，以及分类、分割、深度等下游示例或任务头。它主要提供表征，不是通用聊天模型。[README.md](https://github.com/facebookresearch/dinov3/blob/6876159a11b4df116f30f667f8c9888617df0751/README.md)

## 用法

按上游申请并接受模型权重访问条件，或核所选官方分发路径；示例可用 PyTorch Hub 或 Transformers 加载。训练 / 评估环境文档要求 PyTorch `>=2.7.1`，并说明仅在指定依赖及 Linux 环境测试。[README.md](https://github.com/facebookresearch/dinov3/blob/6876159a11b4df116f30f667f8c9888617df0751/README.md)

先运行小 backbone 的 patch PCA / matching 示例，再根据任务加载适当 head；训练配方与推理加载不是同一成本层次。源码 main 的 FINO 通告指向另一个分支，不能当成默认主线所有 recipe 都已包含。[README.md](https://github.com/facebookresearch/dinov3/blob/6876159a11b4df116f30f667f8c9888617df0751/README.md)

## 原理

训练代码显式构建 student、冻结的 teacher 及可选 Gram 参考模型，包含 DINO / iBOT heads 与 Gram loss 配置；下游使用全局或稠密 patch 表征做分类、匹配与任务头学习。README 将预训练、Gram anchoring、高分辨率适配分列。[dinov3/train/ssl_meta_arch.py](https://github.com/facebookresearch/dinov3/blob/6876159a11b4df116f30f667f8c9888617df0751/dinov3/train/ssl_meta_arch.py) [README.md](https://github.com/facebookresearch/dinov3/blob/6876159a11b4df116f30f667f8c9888617df0751/README.md)

## 价值

工程判断：适合评估冻结 backbone 是否能减少自有视觉任务的标注和训练需求，或作为稠密匹配基线。少量标注、无标签预训练与真正零样本任务不同，必须说明 downstream head 使用了什么监督。

## 风险边界

- 代码与权重采用自定义 **DINOv3 License**，不是 MIT / Apache，也不能简单写成仅限非商用。协议包含分发附带条款、研究发表致谢及特定用途限制，实际应用需逐项核正文。[LICENSE.md](https://github.com/facebookresearch/dinov3/blob/6876159a11b4df116f30f667f8c9888617df0751/LICENSE.md)
- 官方训练规模和跨域结果不能直接移植到当前设备或小数据集；图像预处理、backbone、任务头与数据划分均影响结果。训练 / 评估的 Linux 说明也不证明所有 macOS 路径不可用。[README.md](https://github.com/facebookresearch/dinov3/blob/6876159a11b4df116f30f667f8c9888617df0751/README.md)
- 权重申请成功、可下载或能生成可视化，不代表特定科学图像、医疗、遥感等下游任务已验证。涉及独立词表或数据的组件还需查看逐项来源。[README.md](https://github.com/facebookresearch/dinov3/blob/6876159a11b4df116f30f667f8c9888617df0751/README.md)

## 补充建议

固定 backbone / head / 权重来源，用自有授权样本比对最近邻、线性 probe 与完整微调，保留分域指标、标注量和计算预算。新分支研究单独锁 ref。本轮只读源码与许可，没有申请权重、训练或复现图像任务。

## 参考资料

- [README.md](https://github.com/facebookresearch/dinov3/blob/6876159a11b4df116f30f667f8c9888617df0751/README.md)
- [LICENSE.md](https://github.com/facebookresearch/dinov3/blob/6876159a11b4df116f30f667f8c9888617df0751/LICENSE.md)
- [pyproject.toml](https://github.com/facebookresearch/dinov3/blob/6876159a11b4df116f30f667f8c9888617df0751/pyproject.toml)
- [dinov3/train/ssl_meta_arch.py](https://github.com/facebookresearch/dinov3/blob/6876159a11b4df116f30f667f8c9888617df0751/dinov3/train/ssl_meta_arch.py)
- [仓库 API](https://api.github.com/repos/facebookresearch/dinov3)
