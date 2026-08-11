# ai-nuclear-spectroscopy

## 定位

从公开 NNDC/ENSDF 数据到 γ coincidence GCD 寿命估计的可审计人机协同参考工作流。它将来源保存、筛选、实验统计、结构化 AI 审阅、人工批准与估计结果拆开；当前 `0.1.0` 是使用虚构合成数据的 alpha，不是正式实验分析。

## 用法

```bash
git clone https://github.com/JWP-p/ai-nuclear-spectroscopy.git
cd ai-nuclear-spectroscopy
python -m venv .venv
.venv/bin/python -m pip install -e '.[dev]'
anspec demo --config configs/demo_workflow.json --output demo-output
```

演示产生结果、报告和 provenance manifest。公开数据需显式 `anspec fetch-ensdf`，并复核 manifest 与 NNDC 引用要求。

## 原理

保存 URL、时间、数据集标识、字节数和 SHA-256；解析受限 ENSDF record 子集，枚举 source-local F-D-G cascade 并检查背景统计。AI 仅输出证据/反证/建议记录；人工批准后才做四区域 timing subtraction、signed centroid、PRD 修正和协方差传播。

## 价值

展示如何把机器推荐、人工批准分析范围与正式科学结论清晰分离，适合教学、软件验证和 agent protocol 研究。

## 风险边界

bundled scheme/spectra 为虚构合成数据；测试通过不能验证真实探测器、物理指认或可发表寿命。解析器不能替代 NNDC/ENSDF 工具和专家判断，真实实验还需标定、系统学、数据权利和协作审查。

## 补充建议

先作为 synthetic benchmark 固定配置、版本与 manifest；真实 isotope 接入前逐项验证数据版本、PRD、背景与不确定度，并记录具资格研究者批准。

## 参考资料

- [GitHub 仓库](https://github.com/JWP-p/ai-nuclear-spectroscopy)
- [科学工作流](https://github.com/JWP-p/ai-nuclear-spectroscopy/blob/main/docs/scientific_workflow.md)
- [科学限制](https://github.com/JWP-p/ai-nuclear-spectroscopy/blob/main/docs/limitations.md)
