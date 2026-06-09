# career-ops

- GitHub: https://github.com/santifer/career-ops
- 记录日期: 2026-04-20 (Asia/Shanghai)

## 这是什么

`career-ops` 是一个面向求职场景的 AI Agent 工作流系统：把“职位检索、岗位匹配评估、定制简历生成、投递跟踪、面试准备”串成可重复执行的流水线。

按 GitHub 仓库页面抓取快照（2026-04-20）显示，该项目约 `36.5k stars`、`7.4k forks`，属于近期增长非常快的 AI 应用型仓库之一。

## 为什么今天值得关注

1. 它不是“聊天机器人”，而是完整任务系统：输入 JD，输出结构化决策与产物（报告/PDF/跟踪记录）。
2. 它把 AI 从“给建议”推进到“有状态执行”，代表 AI 工具从 demo 向 workflow 产品迁移。
3. 它与 Claude Code/Playwright/Go TUI 结合，体现了 2026 年高热方向：`Agent + 自动化 + 人类审批`。

## 怎么用（最短可运行路径）

## 1) 本地安装

```bash
git clone https://github.com/santifer/career-ops.git
cd career-ops
npm install
npx playwright install chromium
```

## 2) 初始化配置

```bash
cp config/profile.example.yml config/profile.yml
cp templates/portals.example.yml portals.yml
```

然后补充你的 `config/profile.yml`（目标岗位、偏好、资历），并新建 `cv.md` 作为简历事实源。

## 3) 健康检查 + 启动 Agent 工作流

```bash
npm run doctor
# 然后在项目内进入你的 AI coding CLI（如 claude）
```

在会话里可直接触发 `/career-ops` 系列模式，例如：

- `/career-ops scan`：扫描配置站点职位
- `/career-ops {JD链接或描述}`：执行完整评估流水线
- `/career-ops pdf`：生成 ATS 导向简历 PDF
- `/career-ops batch`：并行处理多个岗位

## 核心原理（工程视角）

## 1) Agent 化流水线，而非单点提示词

它把任务拆成多个模式（扫描、评估、PDF、批处理、跟踪），每一步产出结构化文件，便于回溯和二次加工。

## 2) 人在回路（HITL）

项目明确强调“AI 评估 + 人类决策”，默认不自动替你提交申请，避免误投与不合规自动化。

## 3) 状态持久化

核心数据落在本地文件（如 `data/*.md`、`*.tsv`、配置 YAML）。优点是可审计、可版本化、可复盘，不依赖闭源 SaaS 后台。

## 4) 多引擎协同

- Agent 与决策逻辑：Claude Code 模式
- 页面抓取与 PDF：Playwright
- 可视化看板：Go + Bubble Tea TUI

这种分层组合让“推理、执行、展示”职责分离，降低单点失效。

## 5) 本地优先的数据边界

README 的免责声明强调：简历与个人信息主要保留在本地，调用模型时直接发往你选定的提供方。这是它在隐私与可控性上的主要卖点之一。

## 典型场景

1. 海投前筛选：先用评分系统过滤低匹配岗位。
2. 针对性投递：对高分岗位生成定制 CV 与故事素材。
3. 多公司并行：批处理 + tracker 降低流程管理成本。
4. 面试准备：从历史评估中沉淀 STAR 题材库与谈薪脚本。

## 价值与争议

## 价值

1. 提升求职流程的“吞吐量 + 一致性”。
2. 减少“盲投”与简历模板化低质量投递。
3. 可复盘：每次评估结论都能回看依据。

## 争议与风险

1. 评估结果依赖输入资料质量，可能放大简历偏差。
2. AI 生成内容若不人工校验，会有事实错误或过度包装风险。
3. 自动扫描/抓取行为需遵守各招聘站点 ToS，避免账号风险。
4. 评分框架是“决策辅助”，不是“真实录用概率”。

## 上手建议（实用）

1. 先用 20 个历史岗位做回测，验证评分与真实面试转化是否相关。
2. 把“硬约束”（地域/薪资底线/岗位级别）前置为过滤规则，减少无效 token 消耗。
3. 每周复盘一次：`投递数 -> 回复率 -> 面试率 -> Offer率`，持续调整权重。

## 参考来源

- https://github.com/santifer/career-ops
- https://github.com/santifer/career-ops/blob/main/docs/SETUP.md
- https://github.com/santifer/career-ops/blob/main/CLAUDE.md
- https://ossinsight.io/trending/ai
