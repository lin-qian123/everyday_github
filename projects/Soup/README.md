<!-- markdownlint-disable MD013 MD034 -->

# Soup：用单份 YAML 组织 LLM 微调、评测与交付

## 项目概览

- 上游仓库：https://github.com/MakazhanAlpamys/Soup
- GitHub API 快照（2026-09-01）：4,188 stars、639 forks、62 个开放 issue
- 当前 release：`v0.73.3`
- 主要技术：Python、Transformers、PEFT、TRL、LoRA/QLoRA、可选 Unsloth / MLX
- 许可证：Apache-2.0

## 定位

Soup 是面向消费级硬件的 LLM fine-tuning CLI。它用一份 YAML 描述模型、数据、训练、LoRA、量化、评测和输出，并把环境检查、数据工具、训练、测试和 serving 接口放进同一命令体系。

## 用法

轻量安装只包含 CLI 与配置工具，实际训练需额外依赖：

```bash
pip install soup-cli
pip install "soup-cli[train]"
soup init --template chat
soup train --config soup.yaml
```

典型配置包含基座模型、训练数据、格式、验证集切分、epoch、学习率、batch、LoRA 和 4-bit 量化。开始训练前应先运行 `soup doctor` 并在小数据上做 smoke test。

## 原理

Soup 将配置 schema 作为字段真源，根据硬件与 extras 选择 PyTorch/Transformers、PEFT/TRL、Unsloth、MLX 或 serving 组件。LoRA/QLoRA 通过训练少量适配参数和低比特基座降低显存；layer streaming 等路径试图进一步降低显存峰值。

这类优化改变的是训练和内存路径，不保证任务质量。数据质量、切分、防泄漏、基座许可、量化误差和评测设计仍决定最终模型是否可用。

## 价值

- 用可版本化 YAML 降低微调实验的配置分散问题。
- 把 data inspect、doctor、训练、评测和导出串成同一 CLI。
- 为 CUDA、Apple Silicon、CPU 与多种可选 backend 提供统一入口。
- 适合教学、小规模领域适配和复现实验模板。

## 风险边界

- 上游标题强调 4 GB 显卡上的 8B layer streaming，但 README 的一般要求又建议 7B QLoRA 使用 8 GB+ VRAM；不能把单个演示外推为所有模型/配置都能稳定训练。
- 微调会继承并可能放大基座模型偏差、训练数据泄露和版权/隐私问题。
- 自动 batch、量化和多 backend 会带来数值与版本差异，成功结束不等于质量提升。
- 模型权重、数据集和输出 adapter 各自可能有不同许可与使用限制。
- 本页未运行训练，也未复现显存、吞吐或上游 benchmark。

## 补充建议

1. 固定基座 revision、数据哈希、schema、依赖锁和随机种子。
2. 先用小样本、短步数和同硬件 smoke test 实测显存与 checkpoint 恢复。
3. 将训练集、验证集、最终测试集和人工红队样例严格隔离，检查近重复泄漏。
4. 与未微调基座、简单 prompt/RAG 基线比较，不只报告训练 loss。
5. 在发布 adapter 前整理模型卡、数据来源、许可、失败模式和不可用场景。

## 参考资料

- 仓库与 README：https://github.com/MakazhanAlpamys/Soup
- 官方站点：https://trysoup.dev
- 模型与可选依赖：https://github.com/MakazhanAlpamys/Soup/blob/main/docs/models.md
- 配置说明：https://github.com/MakazhanAlpamys/Soup/tree/main/docs
- 上游演示视频：https://youtu.be/T1LCErE943E
