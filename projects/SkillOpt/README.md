<!-- markdownlint-disable MD013 -->

# SkillOpt（microsoft/SkillOpt）

> 上游仓库：<https://github.com/microsoft/SkillOpt> · 归类：Agent 框架与技能生态 · 本页基于 2026-09-29 的 GitHub API、README、版本化文档、论文、SkillOpt-Sleep 说明、Release、Security Policy 与 LICENSE 静态整理，未运行训练、调用付费模型或复现论文结果。

- 抓取快照：17,800 stars、1,669 forks、54 open issues。
- 热度信号：GitHub Python Trending 抓取时约 +111 当日 stars。
- 版本与许可：MIT；latest Release、tag 与 `pyproject.toml` 版本均为 `v0.2.0` / `0.2.0`。

## 定位

SkillOpt 把自然语言 skill 文档当作可训练参数：目标模型权重保持不变，optimizer model 根据任务轨迹与评分提出文本修改，再由验证集门控是否采用。仓库同时包含 benchmark-oriented research engine 和 SkillOpt-Sleep preview；两者入口、数据来源与安全边界不同。

## 用法

研究路径可安装 `skillopt`，或 clone 仓库后安装 benchmark extras、配置 provider / CLI credentials、materialize 数据切分，再运行 train 与 eval 命令，最终产出 `best_skill.md`。WebUI 默认应绑定 `127.0.0.1`。Sleep 路径会读取受支持 coding-agent 的历史 session，离线提出 skill / memory 更新，用户仍需审核后采用。

## 原理

训练循环是 rollout → reflect → aggregate → select → update → validation gate：目标模型执行任务，optimizer 分析 trajectory，聚合并裁剪 edit patch，更新 Markdown skill，再在 selection split 上决定接受或回退。epoch boundary 还可做 slow update 与 meta-skill 记忆；部署阶段只使用已选出的文本 skill，不增加额外模型调用。

## 价值

它把原本靠手工反复改 prompt / skill 的过程转换为带 split、epoch、learning rate、验证门与 artifact 的实验流程，便于记录“哪次修改为何被接受”。文本产物可 diff、审阅和跨 harness 携带，对不能或不想微调模型权重的团队有实际价值。

## 风险边界

- 上游报告的 52 个 model / benchmark / harness 结果与 GPT-5.5、Codex、Claude Code 增益未在本轮重跑，不能外推到私有任务、更新后的模型或生产 Agent。
- optimizer 可过拟合 selection split，或把 benchmark 答案、评价器弱点与不安全捷径写进 skill；validation gate 只和测试设计一样可靠。
- trajectory、企业样本与 coding-agent session 可能包含源码、路径、secret 或个人数据；provider backend 与 CLI harness 会产生不同的数据外发与保留边界。
- Codex / Claude Code exec harness 可能继承真实工作区与工具权限；“优化文本”不自动限制执行副作用。
- SkillOpt-Sleep 仍是 preview；夜间自动总结若缺少人工 diff 与回滚，会把偶发错误、注入内容或过时习惯固化成持久规则。

## 补充建议

把 train、selection、unseen test 与安全 adversarial set 分开并冻结，禁止 optimizer 读取最终测试答案。使用低权限、无 secret 的副本工作区和预算上限运行 rollout；记录模型版本、seed、数据 commit、成本与全部 skill diff。通过性能门后仍要做权限、注入和副作用审查，再以 canary 方式采用 `best_skill.md`，保留上一版本的一键回滚。

## 参考资料

- [GitHub 仓库](https://github.com/microsoft/SkillOpt)
- [GitHub REST API](https://api.github.com/repos/microsoft/SkillOpt)
- [v0.2.0 Release](https://github.com/microsoft/SkillOpt/releases/tag/v0.2.0)
- [Documentation](https://microsoft.github.io/SkillOpt/docs/guideline.html)
- [SkillOpt-Sleep](https://github.com/microsoft/SkillOpt/blob/main/docs/sleep/README.md)
- [论文](https://arxiv.org/abs/2605.23904)
- [上游演示视频](https://www.youtube.com/watch?v=JUBMDTCiM0M)
- [Security Policy](https://github.com/microsoft/SkillOpt/blob/main/SECURITY.md)
- [LICENSE](https://github.com/microsoft/SkillOpt/blob/main/LICENSE)
