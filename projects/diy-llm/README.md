<!-- markdownlint-disable MD013 -->

# diy-llm：从分词、训练系统到对齐评估的中文实践课程

- 主上游：[datawhalechina/diy-llm](https://github.com/datawhalechina/diy-llm)；repository ID `1102772718`。
- 采样日期：2026-10-26（Asia/Shanghai）；分类：AI 学习与教育资源。
- API 累计快照：1,810 stars / 186 forks / 7 open issues（含 PR 口径）；与榜单日增分开。
- 默认分支 `main`，本页静态依据固定在 `95a3b81d4b2686d33afc2d533b0f91d295ec9b78`。发行 API 首项 [V0.2](https://github.com/datawhalechina/diy-llm/releases/tag/V0.2)，UTC 2026-08-17T11:46:46Z，正式发行。
- 核验层级：读取上游文档、许可、元数据及所列部分实现；未安装运行上游、调用模型或复现实验。

## 定位

diy-llm 是 Datawhale 面向有 Python、PyTorch、数学与机器学习基础的读者整理的 LLM 中文课程，覆盖分词、架构、MoE、GPU / 分布式、扩展定律、数据、推理、对齐和评估。它是讲义与代码实践集合，不是官方 Stanford 学分课程，也不保证完整实现每个章节的工业级系统。

## 用法

先读固定版本 README 与 docs/zh 目录，再按所选作业创建环境。入门获取方式如下，本轮未执行上游代码：

```bash
git clone https://github.com/datawhalechina/diy-llm.git
cd diy-llm
```

不要对整个仓库套用单一依赖环境：作业 2 manifest 要求 Python ≥3.12；作业 5 为 ≥3.11 且 <3.13，并固定 vLLM 0.7.2、flash-attn 2.7.4.post1。后者 README 还使用作者机器上的模型绝对路径，须先改成本机可核对的权重。Release V0.2 提供课程更新与 PDF 入口，主线仍可能继续变化。

## 原理

课程把模型全流程拆成六类作业：从 tokenizer、Transformer 与优化器出发，继而做性能 / 分布式优化、scaling、数据清洗、SFT / GRPO 与多维评估。实现和结果让读者对照理论、资源与误差；理解这种对应关系比只复用 notebook 输出更重要。作业 5 README 明确当前用 GSM8K 替代 MATH，评测名称和数据身份应一并记录。

## 价值

适合中文学习者用较小实验把分词、训练、系统优化及评估串起来，也方便逐层定位“算法没实现、配置没对齐、资源不足、指标不可比”等问题。CPU / MPS 可做部分逻辑调试，不能据此承诺所有 CUDA、Triton、vLLM 与分布式作业都能在 Mac 等价完成。

## 风险边界

- **作业 1 缺少 data.bin 时，train.py 会生成随机 token 模拟数据。** 此时 loss 曲线与 checkpoint 只能说明训练路径运转，不能作为学到自然语言能力的证据。
- 根 README / V0.2 说明涉及 CS336 2026 更新，作业 5 文档和 manifest 仍标 Spring 2025；材料年份、实现和 tests 要逐项对齐，不能将课程整体标成同一年份的完整复现。
- 作业 5 建议至少 80 GB 显存，完整实验更推荐 2×80 GB；这是上游建议而非本轮测量。全量 sweep、模型下载与 W&B 记录均可能增加计算、存储和外发成本。
- GSM8K / MATH 替换、奖励评分器、训练集过滤和验证集选择会改变结果；历史结果文件及作者仪表盘不是本轮复现。根目录“已完成”状态也不能替代逐作业运行验收。
- 根 README 声明 CC BY-NC-SA 4.0，API 未返回 SPDX；目录树未见根 LICENSE，作业 4 自带 MIT LICENSE。正文、派生代码、数据、权重与课程原件需按来源分别核许可，不能整体视为 MIT 或可商用。

## 补充建议

先以真实、已获授权的小语料完成一次 tokenizer 到训练 / 验证的闭环，明确禁用或标识随机数据回退。每个作业独立记录 Python / CUDA / 依赖锁、模型与数据哈希、GPU 小时、随机种子和评分脚本；只在独立测试集报告结果。对照官方题目与本库实现写清差异，再决定是否运行完整对齐实验。

## 参考资料

- [README.md](https://github.com/datawhalechina/diy-llm/blob/95a3b81d4b2686d33afc2d533b0f91d295ec9b78/README.md)。
- [coursework/assignment1-basics/README.md](https://github.com/datawhalechina/diy-llm/blob/95a3b81d4b2686d33afc2d533b0f91d295ec9b78/coursework/assignment1-basics/README.md)。
- [coursework/assignment1-basics/train.py](https://github.com/datawhalechina/diy-llm/blob/95a3b81d4b2686d33afc2d533b0f91d295ec9b78/coursework/assignment1-basics/train.py)。
- [coursework/assignment2-systems/pyproject.toml](https://github.com/datawhalechina/diy-llm/blob/95a3b81d4b2686d33afc2d533b0f91d295ec9b78/coursework/assignment2-systems/pyproject.toml)。
- [coursework/assignment5-alignment/README.md](https://github.com/datawhalechina/diy-llm/blob/95a3b81d4b2686d33afc2d533b0f91d295ec9b78/coursework/assignment5-alignment/README.md)。
- [coursework/assignment5-alignment/pyproject.toml](https://github.com/datawhalechina/diy-llm/blob/95a3b81d4b2686d33afc2d533b0f91d295ec9b78/coursework/assignment5-alignment/pyproject.toml)。
- [coursework/assignment4-data/LICENSE](https://github.com/datawhalechina/diy-llm/blob/95a3b81d4b2686d33afc2d533b0f91d295ec9b78/coursework/assignment4-data/LICENSE)。
- [仓库 API](https://api.github.com/repos/datawhalechina/diy-llm)、[发行 API](https://api.github.com/repos/datawhalechina/diy-llm/releases?per_page=1)；动态元数据仅代表本轮采样。
- 事实来源为以上一手材料；价值、风险评估和建议为本库工程判断，未当作上游实测结果。
