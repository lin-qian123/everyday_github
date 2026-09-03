<!-- markdownlint-disable MD013 MD034 -->

# DeepSWE：用长时程原始工程任务评测 Coding Agents 的基准

## 项目概览

- 上游仓库：https://github.com/datacurve-ai/deep-swe
- GitHub API 快照（2026-09-04）：1,592 stars、106 forks、72 个开放 issue
- 当前 release：未发布 GitHub Release；默认分支最近 push 为 2026-08-26
- 主要技术：113 个 TypeScript / Go / Python / JavaScript / Rust 任务、Harbor task format、Pier、隔离 verifier
- 许可证：Apache-2.0

## 定位

DeepSWE 是面向 frontier coding agents 的长时程软件工程基准，任务取自活跃开源仓库，强调原始问题、可复现容器、隐藏测试和行为级验证。

它衡量的是规定环境和任务集合中的完成情况，不是对模型整体编码能力、生产可靠性、安全性或成本效益的单一排名。

## 用法

上游通过 Pier 运行 Harbor-compatible 任务：

```bash
git clone https://github.com/datacurve-ai/deep-swe
uv tool install datacurve-pier
pier run -p deep-swe/tasks --agent mini-swe-agent --n-tasks 10 --sample-seed 0
```

使用云端模型需自行配置对应 API key；也可指定单任务、CLI agent 或 `--env modal` 并行沙箱。复现实验时应固定仓库 commit、Pier 版本、agent/model 版本、采样参数和执行后端。

## 原理

每个任务包含 `task.toml`、自然语言指令、Docker 环境、tests/verifier 和参考 solution。agent 工作环境与 verifier 环境分离，参考补丁不参与评分；verifier 依据可观察行为产生 binary reward、pass fraction、机器可读测试报告和原始日志。

Pier 负责在隔离环境中驱动 `mini-swe-agent` 或 Claude Code、Codex、Gemini CLI、OpenCode 等 CLI，并保存 trajectory 供后续 critique。隔离和隐藏测试降低部分作弊面，但不能消除任务泄漏、训练污染、评分盲区或基础镜像差异。

## 价值

- 多语言、长时程任务比短函数题更接近真实仓库修改。
- 环境、测试、日志和参考解可审阅，有利于失败分析与重复实验。
- verifier 与 agent 环境分离，降低 agent 直接读取 grader 内容的风险。
- 同一 task format 可比较多个 agent/model 组合，而不只看最终补丁文本。

## 风险边界

- 公开任务和参考解可能进入训练、人工调参或缓存，排行榜不能天然证明未污染泛化。
- hidden tests 只覆盖被编码的行为；通过测试不等于设计、可维护性、安全或全部需求正确。
- 模型别名、provider 后端和 CLI 会变化；不固定版本、温度、预算与重试就难以公平比较。
- 并行 Modal 运行、API token、超时和工具调用会影响成本与成功率，单一 pass rate 不能表达全部权衡。
- 原始开源 issue 的许可、隐私和维护者意图仍需按任务来源核验。
- 本页只做静态资料核验，未执行 113 个任务，也未复现排行榜。

## 补充建议

1. 先抽取 10 个固定任务做 smoke run，保存完整版本、镜像 digest、trajectory、成本和 wall time。
2. 报告 pass rate 时同时给出失败类型、重试策略、token/费用、人工介入和测试覆盖盲区。
3. 对公开任务做 contamination audit，并保留新的私有/时间后切分作为补充。
4. 用人工 reviewer 检查通过任务的补丁质量、安全、可维护性与最小性。
5. 将 DeepSWE 与本团队真实 issue 集并行使用，不把公共榜单当作采购或上线的唯一依据。

## 参考资料

- 仓库与 README：https://github.com/datacurve-ai/deep-swe
- 官方站点：https://deepswe.datacurve.ai/
- Pier：https://github.com/datacurve-ai/pier
- Harbor task format：https://www.harborframework.com/docs/tasks
- 任务目录：https://github.com/datacurve-ai/deep-swe/tree/main/tasks
