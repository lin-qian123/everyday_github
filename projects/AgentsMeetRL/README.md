# AgentsMeetRL

- GitHub：<https://github.com/thinkwee/AgentsMeetRL>
- 项目站点：<https://thinkwee.top/amr/>
- 抓取时间：2026-07-03（Asia/Shanghai）
- 今日信号：GitHub API 显示抓取时约 `1.6k stars / 64 forks`；README 标注 2026-06 更新，新增 43 个 agentic RL 相关仓库，并把语料封装成 Claude Code skill。

## 定位

`AgentsMeetRL` 是一个聚焦“用强化学习训练 LLM agents”的开源项目索引。它不只是普通 awesome-list，而是围绕 agent 项目是否涉及多轮交互、工具调用、奖励设计、环境和训练框架做结构化归类。

它覆盖基础 RL 框架、搜索与 RAG agent、Web/GUI agent、工具调用、代码与 SWE agent、多智能体、记忆、具身、VLM agent、安全与自进化等方向，适合作为 agentic RL 研究入口。

## 用法

最直接的使用方式是打开项目站点或 README，按任务类型筛选：

- 想做工具调用 agent：看 Tool-Use、Reward & Training、Environment 分类。
- 想做浏览器/桌面 agent：看 Web & GUI、VLM Agent、Safety 分类。
- 想做代码 agent 训练：看 Code & SWE、Reasoning、Base Framework 分类。

项目还提供 Claude Code skill：

```bash
/plugin marketplace add thinkwee/claude-plugins
/plugin install agents-meet-rl@thinkwee
```

也可以手动安装：

```bash
git clone https://github.com/thinkwee/AgentsMeetRL
cp -r AgentsMeetRL/skills/agents-meet-rl ~/.claude/skills/
```

## 原理

该项目的核心不是运行时框架，而是一个持续维护的分类知识库：

1. 收集开源 agent / RL / tool-use / environment 项目。
2. 标注项目所属类别、技术路线、论文链接和训练/奖励相关信息。
3. 将机器可读语料打包为 skill，让 coding agent 在调研、实验设计和故障排查时检索使用。

这让它从“链接列表”变成了 agentic RL 选型和实验设计辅助工具。

## 价值

- 对研究：快速看到 agentic RL 领域的项目密度、分类和近月新增方向。
- 对工程：为训练工具调用 agent、Web agent、代码 agent 时选择框架和 benchmark 提供入口。
- 对本仓库：补齐“agent 从调用模型到可训练系统”的趋势线索，避免只看应用层 agent。

## 风险边界

- README 明确说明其项目识别部分依赖代码分析和人工复核，仍可能有遗漏或误分类。
- awesome-list 不能替代论文复现；真正选型仍需看代码活跃度、许可证、训练资源和评测协议。
- RL for agents 的指标很容易跨任务不可比，日报中不应把星标和 benchmark 直接等同为能力领先。

## 补充建议

- 后续可重点跟踪它收录的 2026 年新增项目，如 AgentJet、HarnessX、OpenWebRL、Polar、Agent World Model 等。
- 与 `GUI-Agents-Paper-List`、`agent-lightning`、`Open-AgentRL` 等方向结合，形成 agent 训练和评测的长期观察线。

## 参考资料

- GitHub 仓库：<https://github.com/thinkwee/AgentsMeetRL>
- 项目站点：<https://thinkwee.top/amr/>
- Claude Code skill 目录：<https://github.com/thinkwee/AgentsMeetRL/tree/main/skills/agents-meet-rl>
