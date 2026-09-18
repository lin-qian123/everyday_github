<!-- markdownlint-disable MD013 MD034 -->

# skill-up：Agent Skill 的声明式评测与演进工具

> 上游仓库：https://github.com/alibaba/skill-up · 归类：Agent 框架与技能生态 · 本页基于 2026-09-19 的中英文 README、设计 / 用户配置文档、release、LICENSE 与 REST API 静态整理；未调用模型、Agent judge 或 GitHub Action。

## 定位

阿里巴巴 `skill-up` 把 Agent Skill 评测做成声明式 CLI 与 CI 工作流：用 YAML 定义环境、引擎、模型、用例和 judge，输出 JSON、JUnit、HTML 与 benchmark 报告；配套 `skill-upper` Skill 还能读取失败、修改 Skill 或 eval、补回归用例并启动下一轮评测。它关注的是“如何持续测 Skill”，不是又一个 Skill 聚合目录。

2026-09-19 的 GitHub 官方 Go Trending 抓取显示约 `+12 stars today`；REST API 快照为 `968 stars / 75 forks / 21 open issues`，Apache-2.0。最新 release 为 `v0.12.0`（9 月 18 日）。

## 用法

推荐在 Codex 或 Claude Code 中安装仓库内的 `skill-upper`：

```sh
npx skills add https://github.com/alibaba/skill-up/tree/main/skills/skill-upper -g -a codex -y
```

也可安装 CLI 后手工维护 `evals/eval.yaml` 与 `cases/*.yaml`：

```sh
curl -fsSL https://raw.githubusercontent.com/alibaba/skill-up/main/install.sh | bash
skill-up validate ./evals/eval.yaml
skill-up run ./evals/eval.yaml
```

CI Action 是 Linux container action；生产 workflow 应 pin release tag 或 commit SHA，并通过 secret 传入 provider key。

## 原理

- evaluator 准备 workspace、安装目标 Skill、调用 Claude Code、Codex、Qoder CLI、Qwen Code 或 custom engine，并保存结构化事件和结果。
- judge 支持确定性 `rule_based`、用户脚本和 `agent_judge`；三者的可重复性、权限与费用边界不同。
- report 层生成 `result.json`、Anthropic-compatible `grading.json` / `benchmark.json`、JUnit XML、HTML 与 Markdown。
- `skill-upper` 让 Agent 解释失败，并选择修改 `SKILL.md`、supporting files 或 eval cases，再重新运行；这是自动化改进闭环，不是独立 oracle。
- user config 可设置 OTLP exporter、环境变量与 runtime kwargs；README 提醒 secret 应使用环境变量引用，不要把 literal 写进配置。
- CI 镜像预装多个 engine CLI，`action.yml` 负责把参数与凭据传给评测运行。

## 价值

- 把临时手工对话变成版本化用例、报告与 CI gate，使 Skill 回归可以被复查和比较。
- with / without Skill、规则 / 脚本 / Agent judge 和多 engine 组合，有助于区分 Skill 带来的真实增益与宿主差异。
- JUnit 和 JSON 输出可接入现有 CI、趋势分析与失败归档，而不是只保留聊天截图。
- Apache-2.0、Go CLI、文档和 `v0.12.0` release 提供较清晰的二次集成入口。

## 风险边界

- Agent judge 与被测 Agent 可能共享模型偏差；自动修 eval 还可能让测试逐渐迎合当前实现，形成过拟合或“改题过关”。
- script judge、custom engine、安装 Skill 和运行 Agent CLI 都会执行代码或工具，必须在隔离 workspace 与最小权限环境中运行。
- 多引擎比较若模型、版本、system prompt、预算、工具和随机性没有冻结，结果不可直接归因于 Skill。
- CI 需要 provider secret，镜像预装多个 CLI；使用 `@main` 会引入供应链漂移，report / trace 可能包含 prompt 与业务数据。
- OTLP 由用户配置，embedded defaults 为空；这不等于下游没有 telemetry，也不保证 secret 自动脱敏。
- 本页未复跑仓库示例、未验证 judge 一致性、custom engine 隔离、并发稳定性、费用或 Windows 限制。

## 补充建议

1. 先用确定性 rule / script judge 和合成 fixture 建基线，再引入 blind Agent judge；judge 模型与被测模型尽量分离。
2. 冻结 engine、model、版本、预算、tool allowlist、seed 与环境镜像，保留原始 trace 和失败 artifact。
3. 将自动修复分成“修 Skill”和“修 eval”两类 PR，由人工审核；保留隐藏 holdout，防止 skill-upper 只优化公开用例。
4. CI pin commit SHA，把 provider secret 放在最小权限环境，并对报告、OTLP 和 artifact 做脱敏与保留治理。

## 参考资料

- 上游 README：https://github.com/alibaba/skill-up
- `v0.12.0` release：https://github.com/alibaba/skill-up/releases/tag/v0.12.0
- 官方用户手册：https://alibaba.github.io/skill-up/zh/
- Custom engine 设计：https://github.com/alibaba/skill-up/blob/main/docs/design/custom-engine.md
- GitHub REST API：https://api.github.com/repos/alibaba/skill-up
- LICENSE：https://github.com/alibaba/skill-up/blob/main/LICENSE
