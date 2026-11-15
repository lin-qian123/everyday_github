<!-- markdownlint-disable MD013 -->

# ai-infra-book（bojieli/ai-infra-book）

- GitHub：<https://github.com/bojieli/ai-infra-book>
- 核查：2026-11-16（Asia/Shanghai）07 时段；7,819 stars / 629 forks / 9 open issues（含 PR）；仓库 ID `1342935078`。
- 热度：官方 Python daily +151；首次建档。书稿自述仍是初稿。
- 版本：固定 main `3bdcb4fcab73010eeaccf31cc10a8242a895d82e`；最新自动构建 [build-20261001-161920](https://github.com/bojieli/ai-infra-book/releases/tag/build-20261001-161920)，UTC 10-01，发行正文关联同一提交。不是今天新发书。
- 许可：原创正文、配图与配套代码 Apache-2.0；第三方资料另核。证据为目录与文档静态抽样，未通读全书、复算或重跑实验。

## 定位

李博杰的《深入理解 AI Infra：量化分析与系统设计》开源书稿，从计算、容量、带宽、通信和依赖约束推导系统选择，覆盖模型架构、算子、加速器、网络、推理、训练、资源调度及端边云。配套的静态计算、实跑记录、来源快照和正文相互链接，适合有 Python、线性代数和系统基础的读者。[固定 README](https://github.com/bojieli/ai-infra-book/blob/3bdcb4fcab73010eeaccf31cc10a8242a895d82e/README.md)

## 用法

阅读可从前 1—3 章建立负载概念，再按推理、系统网络或芯片方向选读。网页 / PDF 是阅读入口，`manuscripts/` Markdown 是正文权威来源；社区译本应核对其来源版本。最新下载链接会滚动，引用时记录构建 tag 与提交。

静态计算要求 Python 3.10+ 标准库，无需 GPU 或权重。以下是按项目命令改用本仓库约定的 `python` 的待执行示例：

```bash
python calculations/calc.py models
python calculations/calc.py forward --model qwen3-8b --tokens 8192 --format md
```

先确认当前 Python 版本并固定 checkout。上游 `.lfsconfig` 默认跳过大型 LFS 内容；约 20 GB 是 README 的仓库自述，不是本轮下载测量。复现实跑时仅按实验说明取所需对象，不能把 LFS 指针视为原始数据。[计算说明](https://github.com/bojieli/ai-infra-book/blob/3bdcb4fcab73010eeaccf31cc10a8242a895d82e/calculations/README.md)、[LFS 配置](https://github.com/bojieli/ai-infra-book/blob/3bdcb4fcab73010eeaccf31cc10a8242a895d82e/.lfsconfig)

## 原理

把模型配置、张量形状和场景参数转换为权重、KV / 递归状态、矩阵工作与数据载荷的账本；矩阵 FMA 按 2 FLOPs 计，普通算术和特殊函数分列。以同一工作和接口的输入估算 `max(F/P, V/B)` 资源下界，再与实际执行的额外开销对照。

计算说明特别区分：逻辑算子独立读取 / 物化假设、融合与 tile 重读、真实 HBM 流量，以及硬件峰值的精度 / 累加 / 稀疏条件。MoE 激活 FLOPs 与批内专家并集的权重载荷分开，不按一个模型标签推算全部成本。[计算口径](https://github.com/bojieli/ai-infra-book/blob/3bdcb4fcab73010eeaccf31cc10a8242a895d82e/calculations/README.md)

## 价值

它提供可追问、可替换输入的估算路线，有助于理解“为何增加卡数未必同比加速”“低比特权重为何仍不能代表全部内存”。来源锁与缺项记录比单一漂亮的 tokens/s 更适合形成自己的复核清单；具体结论仍需回到引用原件和目标机器。

## 风险边界

- **静态资源账不等于实测。** 独立算子载荷不是整模型 HBM 下界；峰值 Roofline 也不是延迟承诺。缓存、融合、路由、通信与工作区需逐项验证。
- `experiments/inventory.json` 的历史 93 项 delivered / 17 项有缺口，不代表当前正文全部题目已完成；实验说明列出编号错位、重写题目和失败证据。不要把路径存在、历史状态或单元测试通过写成全书验收。[实验总说明](https://github.com/bojieli/ai-infra-book/blob/3bdcb4fcab73010eeaccf31cc10a8242a895d82e/experiments/README.md)
- 实跑记录自述包括 M2 Max 与共享 RTX PRO 6000 Blackwell；共享负载条件不能改写成独占整卡成绩，本轮未独立确认其数字。
- `generate --steps G` 数的是追加 KV 的模型调用，排除 prefill；与 API 返回 G 个 token 的常用计数存在差别。引用需说明口径。
- 原创内容许可与论文、字体、模板、第三方代码分开；社区译本的来源与公式应对照中文原稿。[许可](https://github.com/bojieli/ai-infra-book/blob/3bdcb4fcab73010eeaccf31cc10a8242a895d82e/LICENSE)

## 补充建议

选一个小模型、一个场景和一台已有机器，先手算权重 / 状态 / 矩阵量，再对照 CLI，最后做独立测量。引用图表时保留单位、精度、假设、固定输入与来源，不把模拟或估算点改称实验。全书适合按章节渐进核验；本页没有替书稿做科学正确性背书。

## 参考资料

- [仓库 API](https://api.github.com/repos/bojieli/ai-infra-book)、[固定 README](https://github.com/bojieli/ai-infra-book/blob/3bdcb4fcab73010eeaccf31cc10a8242a895d82e/README.md)。
- [在线阅读](https://bojieli.github.io/ai-infra-book/)、[固定构建发行](https://github.com/bojieli/ai-infra-book/releases/tag/build-20261001-161920)。
- [计算与假设](https://github.com/bojieli/ai-infra-book/blob/3bdcb4fcab73010eeaccf31cc10a8242a895d82e/calculations/README.md)、[实验状态](https://github.com/bojieli/ai-infra-book/blob/3bdcb4fcab73010eeaccf31cc10a8242a895d82e/experiments/README.md)、[LFS 配置](https://github.com/bojieli/ai-infra-book/blob/3bdcb4fcab73010eeaccf31cc10a8242a895d82e/.lfsconfig)、[许可](https://github.com/bojieli/ai-infra-book/blob/3bdcb4fcab73010eeaccf31cc10a8242a895d82e/LICENSE)。
