<!-- markdownlint-disable MD013 -->

# Product Manager Skills（deanpeters/Product-Manager-Skills）中文解读

> 上游仓库：<https://github.com/deanpeters/Product-Manager-Skills> · 归类：办公、商业与行业应用 · 本页基于 2026-10-14 的 README、77 个 `SKILL.md`、平台指南、校验脚本、Release、许可证与 GitHub REST API 静态整理；未安装到真实团队 Agent、执行市场研究或验证业务结果。

## 定位

Product Manager Skills 将产品管理方法封装为 Agent 可读的结构化技能，覆盖 problem framing、discovery、stakeholder、prioritization、roadmap、PRD、实验、市场情报、AI 产品和 lifecycle / EOL。它面向 Claude、Codex、ChatGPT、Cursor、n8n 等宿主，并提供不同平台的安装包和本地 Streamlit playground。

## 用法

用户可下载 starter / discovery / strategy / delivery / AI PM 等 pack，或把 Codex pack 安装到 `.agents/skills`。更稳妥的方式是先选一个低风险 component skill，在虚构产品背景中核对问题、输入、输出、引用和决策记录，再按需扩大，不应一次性把 77 个技能全部注入真实工作区。

## 原理

- 每个 `SKILL.md` 以 frontmatter、Purpose、Input、Key Concepts、Application、Examples、Pitfalls 与 References 表达方法。
- component、interactive、workflow 三层分别提供模板、引导式决策与跨阶段流程。
- Adaptive Decision Ladder 先询问 3–5 个上下文问题，再给出带适用理由的编号路径。
- validator、catalog generator、library drift 与 trigger checks 用于维护技能结构和分发包一致性。

## 价值

- 把 PM 方法的判断依据、反例和失败模式一起交给 Agent，优于只有模板标题的 prompt 列表。
- 市场情报技能显式区分 Fact / Inference / Assumption，并使用 question budget、do-not-invent 与稳定 schema。
- 77 个技能可单独选用，适合把通用方法与团队自己的产品事实、权限和审批层分开。

## 风险边界

- “battle-tested”与技能数量是上游定位，不证明 Agent 输出的用户研究、市场规模、优先级或路线图已经过真实客户和数据验证。
- GitHub API 许可证为 `NOASSERTION`，根 LICENSE 是 CC BY-NC-SA 4.0；署名、非商业与相同方式共享义务不等同于常见代码开源许可。
- 技能可引导联网研究、文件读取、MCP 和外部工具；Markdown 指令不能限制宿主权限、数据出口或写操作。
- README 同时出现“77 skills”与旧的“70 Skills”小节标题，说明 catalog / 文案可能漂移；安装包与源码需以校验结果和 Release 固定。

## 补充建议

- 为选用技能补团队自己的 evidence schema、数据等级、审批人、禁用动作和完成定义；把 Agent 草案标成草案。
- 用历史已决策案例做盲测，比较无技能 / 单技能输出的遗漏、事实错误、可执行性与评审时间，不以格式完整度当质量。
- 商业分发、课程或付费服务前审查 CC BY-NC-SA 4.0；内部使用也保留来源、版本和修改记录。

## 参考资料

- GitHub 仓库：<https://github.com/deanpeters/Product-Manager-Skills>
- GitHub REST API：<https://api.github.com/repos/deanpeters/Product-Manager-Skills>
- `v0.84` Release：<https://github.com/deanpeters/Product-Manager-Skills/releases/tag/v0.84>
- Catalog：<https://github.com/deanpeters/Product-Manager-Skills/tree/main/catalog>
- Codex 使用指南：<https://github.com/deanpeters/Product-Manager-Skills/blob/main/docs/Using%20PM%20Skills%20with%20Codex.md>
- Validator：<https://github.com/deanpeters/Product-Manager-Skills/blob/main/scripts/validate-skills.sh>
- LICENSE：<https://github.com/deanpeters/Product-Manager-Skills/blob/main/LICENSE>
