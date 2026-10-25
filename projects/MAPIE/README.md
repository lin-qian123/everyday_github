<!-- markdownlint-disable MD013 -->

# MAPIE：为机器学习预测增加区间、集合与风险控制

- 主上游：[scikit-learn-contrib/MAPIE](https://github.com/scikit-learn-contrib/MAPIE)；repository ID `352931865`。
- 采样日期：2026-10-26（Asia/Shanghai）；分类：模型、训练与推理基础设施。
- API 累计快照：1,640 stars / 171 forks / 25 open issues（含 PR 口径）；与榜单日增分开。
- 默认分支 `master`，本页静态依据固定在 `f1cc3d07460b2d7198f557d40d60cd563c51822b`。发行 API 首项 [v1.6.0](https://github.com/scikit-learn-contrib/MAPIE/releases/tag/v1.6.0)，UTC 2026-10-19T09:41:05Z，正式发行。
- 核验层级：读取上游文档、许可、元数据及所列部分实现；未安装运行上游、调用模型或复现实验。

## 定位

MAPIE 是 scikit-learn-contrib 生态中的 Python 不确定性量化与风险控制库，可为回归生成预测区间、为分类生成标签集合，并为某些精确率 / 召回率等目标选择阈值。它也有 LLM 分类 / judge 相关例子，不能因此推断能为任意自由生成文本提供“答案一定正确”的保证。

## 用法

可先在独立环境固定已发行版本，本轮未安装或运行：

```bash
python -m pip install mapie==1.6.0
```

典型流程是：训练基模型，保留独立 conformalization 数据，创建 SplitConformalRegressor / SplitConformalClassifier，调用 conformalize，再以 predict_interval / predict_set 获取区间或集合。v1 API 用 confidence_level；旧教程的 MapieRegressor、cv 与 alpha 不能直接照搬。

**依赖以 manifest 为准**：本轮主线及 v1.6.0 的 pyproject 均要求 Python ≥3.10、NumPy ≥1.24.1、scikit-learn ≥1.4、SciPy ≥1.10；README / quick start 仍写 Python 3.9、NumPy 1.23。选用条件覆盖等额外功能还要检查对应 optional dependencies。

## 原理

标准 conformal prediction 用留出数据上的 conformity score 估计误差分位，再围绕预测构造集合。在校准样本与未来样本可交换等前提下，标准方法给出总体平均的边际覆盖，而非每个输入都满足目标。条件覆盖方法另有分组 / 特征映射及有限维实现限制；风险控制则针对定义好的损失和置信水平寻找决策阈值，与单点预测精度是不同指标。

## 价值

当系统需要判断“何时拒答、转人工或报告范围”时，它能把模型置信输出转成可核对的覆盖率、区间宽度、集合大小和指定风险。适合带有留出标签的预测流程；其工程价值在于把不确定性和可用率一起报告，不是给原模型贴可靠性认证。

## 风险边界

- **90% 边际覆盖不等于对每个群体或每个个体有 90% 正确率。** 数据漂移、依赖结构、标签污染、校准集重复调参都会破坏适用前提；可交换性检验也不能证明所有未来数据都满足条件。
- 条件方法不是任意分布漂移的通用解法；当前文档说明主要实现有限维情形，部分更一般方法尚未优化。必须按实际算法核保证，不能把一个方法的理论套到整个包。
- LLM judge 的标签、评分函数与任务约化可能本身有偏；控制某个分类风险不等于消除幻觉、保证事实或完成领域安全验收。
- v1.6.0 发行列出 split / cross-conformal 分位数等修复；旧版和新版的数值可能不同，应固定版本复核已有报告，不能无说明合并曲线。本轮没有重算这些修复的统计效果。
- 代码为 BSD-3-Clause；外部数据和模型仍有各自许可。已读文档和 manifest，未拟合模型、跑统计仿真或验证理论证明。

## 补充建议

用固定随机种子的独立 train / conformalize / test 三划分做基线，同时报告总体与预定义子群覆盖、样本量、区间宽度 / 集合大小及误差条。另设时间后移或分布变化测试，观察拒答率与业务成本。升级 v1.6.0 时保留原版结果和依赖锁，逐一确认数值变化来自修复而非数据泄漏。

## 参考资料

- [README.md](https://github.com/scikit-learn-contrib/MAPIE/blob/f1cc3d07460b2d7198f557d40d60cd563c51822b/README.md)。
- [LICENSE](https://github.com/scikit-learn-contrib/MAPIE/blob/f1cc3d07460b2d7198f557d40d60cd563c51822b/LICENSE)。
- [pyproject.toml](https://github.com/scikit-learn-contrib/MAPIE/blob/f1cc3d07460b2d7198f557d40d60cd563c51822b/pyproject.toml)。
- [doc/content/getting-started/quick-start.md](https://github.com/scikit-learn-contrib/MAPIE/blob/f1cc3d07460b2d7198f557d40d60cd563c51822b/doc/content/getting-started/quick-start.md)。
- [doc/content/conformal-prediction/theory.md](https://github.com/scikit-learn-contrib/MAPIE/blob/f1cc3d07460b2d7198f557d40d60cd563c51822b/doc/content/conformal-prediction/theory.md)。
- [doc/content/conformal-prediction/conditional-guarantees.md](https://github.com/scikit-learn-contrib/MAPIE/blob/f1cc3d07460b2d7198f557d40d60cd563c51822b/doc/content/conformal-prediction/conditional-guarantees.md)。
- [doc/content/risk-control/llm-risk-control.md](https://github.com/scikit-learn-contrib/MAPIE/blob/f1cc3d07460b2d7198f557d40d60cd563c51822b/doc/content/risk-control/llm-risk-control.md)。
- [v1.6.0 的依赖声明](https://github.com/scikit-learn-contrib/MAPIE/blob/v1.6.0/pyproject.toml)。
- [仓库 API](https://api.github.com/repos/scikit-learn-contrib/MAPIE)、[发行 API](https://api.github.com/repos/scikit-learn-contrib/MAPIE/releases?per_page=1)；动态元数据仅代表本轮采样。
- 事实来源为以上一手材料；价值、风险评估和建议为本库工程判断，未当作上游实测结果。
