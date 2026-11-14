<!-- markdownlint-disable MD013 -->

# SkillEvaluator

- 上游：[NVIDIA/SkillEvaluator](https://github.com/NVIDIA/SkillEvaluator)
- 分类：Agent 框架与技能生态。
- 核验：2026-11-15（Asia/Shanghai）；仓库 ID `1278676884`，主线快照 `0d5e356583fee63c3d12e4930581c7dfb3352911`；发行与 PyPI 均为 `0.9.0`。下述主线文档不等于已逐项验证发行包。
- 证据范围：官方 API、发行、固定 SHA 文档 / 清单与 CI 说明的静态核读；未安装、调用模型、启动 Agent 或运行扫描器。

## 定位

SkillEvaluator 为 Agent Skills 提供三层评估：Tier 1 检查格式、质量和静态风险；Tier 2 检查指令重复与语义重叠；Tier 3 对同一任务分别运行有技能 / 无技能的 Agent，比较任务结果。适合技能维护者建立可追溯的检查和对照实验。[README](https://github.com/NVIDIA/SkillEvaluator/blob/0d5e356583fee63c3d12e4930581c7dfb3352911/README.md)

它是实验性、社区支持项目，官方不承诺企业 SLA。静态检查通过、技能被触发、任务成功和对照增益是不同结论。

## 用法

先在独立 Python 环境固定版本。项目声明 Python `>=3.12,<3.15`，基础依赖不包含 Harbor 和模型客户端；需要的能力通过 extras 添加。[清单](https://github.com/NVIDIA/SkillEvaluator/blob/0d5e356583fee63c3d12e4930581c7dfb3352911/pyproject.toml)、[PyPI 元数据](https://pypi.org/pypi/skillevaluator/json)

```bash
python -m pip install skillevaluator==0.9.0
skillevaluator quality-check ./my-skill -r cli -r json -o reports/quality
skillevaluator validate ./my-skill --tiers 1 --no-llm
```

以上为上游入口示例，未在本轮执行。第一项质量检查在安装依赖后可离线运行；它不运行安全扫描器，也不测 Agent 能力，报告发布证据仍可能是 `INCOMPLETE`。第三行的 Tier 1 需要扫描器；缺失时会获取固定版本的第三方工具，`--no-llm` 不等于免安装、免联网或完整扫描。[快速入门](https://github.com/NVIDIA/SkillEvaluator/blob/0d5e356583fee63c3d12e4930581c7dfb3352911/docs/quickstart.mdx)

再做 Tier 2 / Tier 3 时，先选定模型、凭据、经过人工审核的数据集和执行环境。不要直接把 `ci init` 当只读检查：它可以创建配置或开设置 PR。

## 原理

- Tier 1 结合规则、外部扫描器及可选模型 rubric；一个静态质量分不能覆盖所有安全证据。
- Tier 2 使用 embeddings 和聊天模型分析重叠。可接本地兼容服务，但需同时核实 embeddings 与 chat 两条路由；更换 embedding 模型后，旧向量不能直接比较。
- Tier 3 用 Harbor 等环境运行配对实验。Skill Lift 是有技能与无技能两臂的分数差，不是“技能通过率”，也不是与旧技能版本的差。[配置](https://github.com/NVIDIA/SkillEvaluator/blob/0d5e356583fee63c3d12e4930581c7dfb3352911/docs/configuration.mdx)、[实时评测](https://github.com/NVIDIA/SkillEvaluator/blob/0d5e356583fee63c3d12e4930581c7dfb3352911/docs/tier3-live-evaluation.mdx)

`--skip-baseline` 可用于调试激活，但不能测 Skill Lift；评分器异常、缺失轨迹或不完整臂应保留为失败 / 不完整证据，不能当零分或成功。自动生成的少量技能内生案例也不能代表独立任务分布。

## 价值

把“技能写得好”“扫描没有发现问题”“能被正确调用”“实际改善任务”拆成可审查证据，比单看技能数量或一个总分更有工程意义。0.9.0 增加预算、可复用 baseline、版本比较和更明确的期望覆盖，适合持续记录技能迭代。[发行说明](https://github.com/NVIDIA/SkillEvaluator/releases/tag/v0.9.0)

对本仓库的选型价值主要是评估方法与证据格式；本轮未复现实测增益，也未比较不同技能产品的效果。

## 风险边界

1. **CI 绿灯与有效增益分开。** 采样主线的三层 CI 模板仅由 Tier 1 决定阻断，Tier 2 / Tier 3 为 advisory，连失败或缺证据也不会使这一门控失败；旧 `tier3-required` 开关已弃用并被忽略。CLI 联合管线的阻断选项另有语义，不能套用到 CI。[CI 说明](https://github.com/NVIDIA/SkillEvaluator/blob/0d5e356583fee63c3d12e4930581c7dfb3352911/ci/templates/all-tiers/README.md)
2. **模型评分存在条件与方差。** 固定任务、模型、harness、评分器、尝试预算与技能快照，记录全部失败臂；只报告成功样本会改变分母。模型评审需要人工抽查和确定性结果核验。
3. **执行环境与数据出口独立。** Docker 默认环境、本地模式和托管沙箱权限不同；本地模式不能按容器隔离理解。技能正文、任务和轨迹可能进入模型服务；保留轨迹即使已脱敏凭据，也可能含任务输入及输出。
4. **预算不是固定报价。** 试验量约为“案例 × Agent × 尝试 × 对照臂”，每次还可能有多轮模型和评分调用。预算停止保留的部分结果不等于完整对照。
5. **许可与支持分层。** 根代码 Apache-2.0；第三方扫描器、模型、执行环境有各自条款。实验性支持不构成安全认证。[许可](https://github.com/NVIDIA/SkillEvaluator/blob/0d5e356583fee63c3d12e4930581c7dfb3352911/LICENSE)

## 补充建议

先用无密钥静态质量路径熟悉报告，再在非敏感、可重置环境运行小型人工审核数据集。分别记录 met / unmet / unchecked / inapplicable、激活证据、配对覆盖、耗时、可用 token 计数和实际费用。

若要将 Agent 增益作为合并条件，先确认当前版本实际 CI 语义并设计团队策略；不要依赖已被忽略的开关。独立测试集和失败轨迹应与技能作者生成的示例分开保存。

## 参考资料

- [仓库 API](https://api.github.com/repos/NVIDIA/SkillEvaluator)、[0.9.0 发行](https://github.com/NVIDIA/SkillEvaluator/releases/tag/v0.9.0)。
- [固定 README](https://github.com/NVIDIA/SkillEvaluator/blob/0d5e356583fee63c3d12e4930581c7dfb3352911/README.md)、[Python / extras 清单](https://github.com/NVIDIA/SkillEvaluator/blob/0d5e356583fee63c3d12e4930581c7dfb3352911/pyproject.toml)、[许可](https://github.com/NVIDIA/SkillEvaluator/blob/0d5e356583fee63c3d12e4930581c7dfb3352911/LICENSE)。
- [快速入门](https://github.com/NVIDIA/SkillEvaluator/blob/0d5e356583fee63c3d12e4930581c7dfb3352911/docs/quickstart.mdx)、[模型路由](https://github.com/NVIDIA/SkillEvaluator/blob/0d5e356583fee63c3d12e4930581c7dfb3352911/docs/configuration.mdx)、[实时评测](https://github.com/NVIDIA/SkillEvaluator/blob/0d5e356583fee63c3d12e4930581c7dfb3352911/docs/tier3-live-evaluation.mdx)、[三层 CI](https://github.com/NVIDIA/SkillEvaluator/blob/0d5e356583fee63c3d12e4930581c7dfb3352911/ci/templates/all-tiers/README.md)。
