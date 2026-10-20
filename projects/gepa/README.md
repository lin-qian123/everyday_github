<!-- markdownlint-disable MD013 -->

# GEPA

> 更新：2026-10-21（Asia/Shanghai）。分类：Agent 框架与技能生态。上游 `gepa-ai/gepa`；快照 `8f287de942f4`（main）。本文为官方资料与源码静态研究；热度、发行时间及社媒限制见[当日日报](../../daily/2026-10-21/ai-hotspots.md)。

## 定位

Genetic-Pareto 文本参数优化框架，可优化 prompt、代码、Agent 结构与配置；提供通用优化器、DSPy 接入和多种 adapter。README 中性能 / 成本案例属于各自任务及作者或引用方结果，本页不认作普遍收益。[README.md](https://github.com/gepa-ai/gepa/blob/8f287de942f41a6d1e0e7e5b2d576247c4bedee9/README.md)

## 用法

基础安装入口 `pip install gepa`；main 安装与发行包应分开固定。提示词路径使用 seed candidate、trainset / valset、task model、reflection model 与调用预算；`optimize_anything` 另外接受自定义 evaluator。[README.md](https://github.com/gepa-ai/gepa/blob/8f287de942f41a6d1e0e7e5b2d576247c4bedee9/README.md) [pyproject.toml](https://github.com/gepa-ai/gepa/blob/8f287de942f41a6d1e0e7e5b2d576247c4bedee9/pyproject.toml)

先实现确定的评分与诊断，再设较小预算；evaluator 可返回 `(score, info)`，info 被用于反思。当前 main 的 API / skill 指南可能领先 GitHub Release `v0.1.4`，不能混用片段。[.claude/skills/gepa-optimize-anything/references/writing_evaluators.md](https://github.com/gepa-ai/gepa/blob/8f287de942f41a6d1e0e7e5b2d576247c4bedee9/.claude/skills/gepa-optimize-anything/references/writing_evaluators.md)

## 原理

候选先在小批任务上执行，保留得分及诊断；反思模型读取失败原因并提出变异，在不同任务子集上保留有优势的 Pareto 候选，也支持合并候选长处。adapter 把用户系统的 evaluate 与反思数据转换接到搜索过程。[README.md](https://github.com/gepa-ai/gepa/blob/8f287de942f41a6d1e0e7e5b2d576247c4bedee9/README.md) [src/gepa/core/adapter.py](https://github.com/gepa-ai/gepa/blob/8f287de942f41a6d1e0e7e5b2d576247c4bedee9/src/gepa/core/adapter.py)

## 价值

工程判断：相比纯手改 prompt，可保存候选、数据、反馈与预算，适合已能客观验收的流程。它把优化目标显式化，也会暴露“评分高但实际任务失败”的指标漏洞。

## 风险边界

- 反思反馈可能包含答案、源代码、错误栈与执行日志，需审查进入 provider 的内容及保存位置。代码候选的运行权限由 evaluator / 宿主提供，搜索算法本身不是隔离层。[src/gepa/core/adapter.py](https://github.com/gepa-ai/gepa/blob/8f287de942f41a6d1e0e7e5b2d576247c4bedee9/src/gepa/core/adapter.py) [.claude/skills/gepa-optimize-anything/references/writing_evaluators.md](https://github.com/gepa-ai/gepa/blob/8f287de942f41a6d1e0e7e5b2d576247c4bedee9/.claude/skills/gepa-optimize-anything/references/writing_evaluators.md)
- train / validation / held-out test 必须分开；反复选择会过拟合验证集。官方 evaluator 指南也提醒单次随机采样的噪声会造成选择膨胀，必要时在 evaluator 内重复测量。[.claude/skills/gepa-optimize-anything/references/writing_evaluators.md](https://github.com/gepa-ai/gepa/blob/8f287de942f41a6d1e0e7e5b2d576247c4bedee9/.claude/skills/gepa-optimize-anything/references/writing_evaluators.md)
- metric 调用上限不等于总 token / 时间 / 费用硬上限；反思、重试和候选执行需另计。MIT 许可不保证模型或数据可同条件使用。[README.md](https://github.com/gepa-ai/gepa/blob/8f287de942f41a6d1e0e7e5b2d576247c4bedee9/README.md) [LICENSE](https://github.com/gepa-ai/gepa/blob/8f287de942f41a6d1e0e7e5b2d576247c4bedee9/LICENSE)

## 补充建议

用一组冻结、可人工复核的任务做 baseline，保留独立测试集、随机种子、模型与所有候选；报告均值、失败例、总费用和耗时。未独立复现 README 的 90 倍成本、RL 比较或其他案例指标，本轮未调用任何模型。

## 参考资料

- [README.md](https://github.com/gepa-ai/gepa/blob/8f287de942f41a6d1e0e7e5b2d576247c4bedee9/README.md)
- [src/gepa/core/adapter.py](https://github.com/gepa-ai/gepa/blob/8f287de942f41a6d1e0e7e5b2d576247c4bedee9/src/gepa/core/adapter.py)
- [LICENSE](https://github.com/gepa-ai/gepa/blob/8f287de942f41a6d1e0e7e5b2d576247c4bedee9/LICENSE)
- [pyproject.toml](https://github.com/gepa-ai/gepa/blob/8f287de942f41a6d1e0e7e5b2d576247c4bedee9/pyproject.toml)
- [.claude/skills/gepa-optimize-anything/references/writing_evaluators.md](https://github.com/gepa-ai/gepa/blob/8f287de942f41a6d1e0e7e5b2d576247c4bedee9/.claude/skills/gepa-optimize-anything/references/writing_evaluators.md)
- [仓库 API](https://api.github.com/repos/gepa-ai/gepa)
- [v0.1.4 Release](https://github.com/gepa-ai/gepa/releases/tag/v0.1.4)
