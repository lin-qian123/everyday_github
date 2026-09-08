<!-- markdownlint-disable MD013 MD034 -->

# i-have-adhd（ayghri/i-have-adhd）

> 记录日期：2026-09-09（Asia/Shanghai）。本页依据上游 README、安装说明、skill 文本、仓库结构、LICENSE 与 GitHub REST API 做静态整理；本轮未安装该 skill/plugin，也未运行其 evals 或验证它对准确率、遗漏率、阅读负担的实际影响。

## 定位

`i-have-adhd` 是一个面向 coding agent 输出风格的 skill/plugin：要求模型先给行动、为多步骤任务编号、抑制旁支、显式重述状态，并以一个具体下一步结束。它借用了 ADHD 友好表达的命名，但 README 明确写着不要求用户有 ADHD 诊断；它改变的是 agent 的沟通约束，不是医疗、诊断或治疗工具。

2026-09-09 的 GitHub 官方综合 / Python Trending 抓取显示约 `+422 stars today`；REST API 快照为 `30,225 stars / 1,845 forks / 31 open issues`，MIT。仓库没有 GitHub release；根 `package.json` 版本为 `0.2.0`，因此升级时不能把默认分支与稳定 release 等同。

## 用法

上游建议直接把仓库安装请求交给兼容 CLI：

```text
Install the i-have-adhd skill/plugin from https://github.com/ayghri/i-have-adhd, refer to the repo's AGENTS.md for instructions.
```

更稳妥的试用方式是先在浏览器中审阅 `INSTALL.md`、`AGENTS.md`、`skills/i-have-adhd/SKILL.md` 与 plugin manifests，再把固定 commit 的 skill 放进一次性测试 profile。不要只凭一条自然语言安装指令直接允许 agent 修改用户级配置。

## 原理

- **十条输出规则**：强调 action first、步骤编号、单一下一步、控制旁支、重述当前状态与具体时间估计。
- **跨宿主打包**：仓库同时提供 Claude / Codex plugin manifest 与通用 plugin 元数据，核心行为由可读的 `SKILL.md` 表达。
- **提示层约束**：它不替换模型、工具或执行器，而是在模型输出阶段压缩铺垫和收束结构。
- **可调副本**：上游鼓励 fork 后修改规则，说明其本质是可版本化的团队沟通政策。
- **评测入口**：仓库包含 `evals/`，但本页没有运行，不能据目录存在推断其效果已被独立验证。

## 价值

- 对长篇铺垫、行动项埋在末尾和任务状态漂移有直接、低门槛的约束。
- 规则文本短且可审阅，适合团队把“回答风格”从个人偏好变成版本化配置。
- 同一表达约束可随 plugin / skill 在多个 coding-agent 宿主之间复用。
- 对需要低认知负担界面的用户，编号、状态重述与单一步骤可能比泛化“简洁一点”更可操作。

## 风险边界

- “ADHD-friendly”是上游的产品表述，不是临床有效性、无障碍合规或对所有 ADHD 用户都适用的证据；个体需求差异很大。
- 过度压缩可能隐藏前提、风险、替代方案和验证边界；安全、法律、医疗、科研或不可逆操作不能为了短而省略关键说明。
- “具体时间估计”若无执行数据支撑，可能把不确定性包装成精确数字。
- 反复重述状态与固定格式也可能增加噪声，或与仓库自身写作规范、系统指令发生冲突。
- 远程 skill 是高信任 prompt 供应链；安装说明可能随默认分支变化，MIT 许可证不等于内容安全。
- Trending 与 stars 只说明公开关注度，本页未证明它能提升任务成功率、理解度或可访问性。

## 补充建议

- 用固定的 20–50 个真实任务做 A/B：测首个可执行动作位置、关键 caveat 漏失率、用户追问次数、总 token 与任务完成率。
- 把“不能删减的边界”写成更高优先级规则，例如危险命令、医疗/法律免责声明、科研证据等级与失败日志。
- 在仓库级或专用 profile 试用，不直接覆盖全局写作规则；固定 commit 并记录卸载路径。
- 邀请真实目标用户评估阅读体验，不用 stars、短输出或开发者偏好替代可访问性研究。

## 参考资料

- GitHub 仓库：https://github.com/ayghri/i-have-adhd
- GitHub REST API：https://api.github.com/repos/ayghri/i-have-adhd
- 安装说明：https://github.com/ayghri/i-have-adhd/blob/main/INSTALL.md
- 核心 skill：https://github.com/ayghri/i-have-adhd/blob/main/skills/i-have-adhd/SKILL.md
- Evals：https://github.com/ayghri/i-have-adhd/tree/main/evals
- LICENSE：https://github.com/ayghri/i-have-adhd/blob/main/LICENSE
