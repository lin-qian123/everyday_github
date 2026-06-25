# ai-berkshire（xbtlin/ai-berkshire）

- GitHub: https://github.com/xbtlin/ai-berkshire
- 记录日期: 2026-06-26 (Asia/Shanghai)

## 定位

`ai-berkshire` 是一个把价值投资研究流程 agent 化的开源框架。它不是通用量化回测库，也不是单个选股脚本，而是把巴菲特、芒格、段永平、李录四种价值投资视角拆成可复用的 skills、研究模板和多 Agent 并行流程，目标是让个人研究者用 Claude Code 组织出更系统的投研工作流。

## 热度信号

1. GitHub API 在 2026-06-26 抓取时显示约 `1,803 stars`、`292 forks`，仓库在 `2026-06-25T22:06:43Z` 仍有推送。
2. GitHub Trending 全站与 Python 日榜在 2026-06-26 抓取时都出现该项目，Trending 页面显示约 `201 stars today`。
3. 官方 README 直接把它定义为 `AI-era Berkshire: a value investing research framework built on Claude Code`，并强调 `4 masters' methodologies + multi-agent adversarial analysis`。

## 用法

### 1) 先准备 Claude Code 运行环境

README 把 Claude Code 作为主入口，先安装 CLI：

```bash
npm install -g @anthropic-ai/claude-code
```

### 2) 克隆仓库并进入项目

```bash
git clone https://github.com/xbtlin/ai-berkshire.git
cd ai-berkshire
```

### 3) 从技能入口发起研究

README 展示的核心使用方式不是调用单一脚本，而是在 agent 会话里使用技能命令，例如：

- `/investment-research`
- `/investment-team`
- `/earnings-review`
- `/portfolio-review`

这意味着它更像“投研 workflow 包”，而不是给你一个 REST API。

## 原理

1. 仓库把投资研究拆成技能层、Agent 层和工具层三层结构。
2. 技能层负责定义研究场景，例如公司深度研究、财报精读、行业筛选、组合管理。
3. Agent 层把不同投资风格拆成并行角色，让多视角互相挑战，而不是只给出平均化结论。
4. 工具层负责金融数据校验、计算精度与结果复核，避免 LLM 在估值、单位换算和数字推断上“看起来合理但实际有误”。

## 价值

- 对中文投资研究者，这个项目的价值不在“AI 会不会写研究报告”，而在“能不能把研究流程做成可重复、可比较、可复盘的纪律系统”。
- 它把 coding agent 从写代码扩展到了知识工作流，说明 AI agent 的一个现实落点是高强度分析型行业，而不只是软件开发。
- 如果后续社区继续围绕具体行业沉淀 skill 包，这类项目会是“领域化 agent 框架”的典型样本。

## 风险边界

- 官方 README 展示了历史收益与实盘截图，但这不构成可验证、可外推的未来收益承诺；任何策略收益都可能受样本期、仓位、市场环境影响。
- 该项目更像投研辅助系统，不是自动交易系统；即使结论结构化，最终投资责任仍在使用者。
- 多 Agent 分析会放大研究深度，也会放大信息源质量问题；若输入数据失真，流程越复杂不一定越可靠。

## 补充建议

1. 把它当成“研究流程模板”比“买卖信号生成器”更合适。
2. 试用时优先选自己熟悉、数据公开度高的公司，便于判断四种视角是否真的带来增量信息。
3. 若你关注的是更通用的金融 agent，建议把它与 `TradingAgents`、`AI-Trader`、`daily_stock_analysis` 对照来看：`ai-berkshire` 更强调价值投资框架和研究纪律，而不是短频交易或看板系统。

## 参考资料

- https://github.com/xbtlin/ai-berkshire
- https://github.com/trending
- https://github.com/trending/python
