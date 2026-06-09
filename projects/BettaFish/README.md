# BettaFish（微舆）项目速览与实操笔记

- 项目地址：https://github.com/666ghj/BettaFish
- 适合人群：需要做舆情洞察、品牌/事件分析、竞品监控、内容运营策略的人。
- 本文状态：基于 2026-03-23 可获取的公开信息整理。

## 1. 这是什么

BettaFish 是一个「多 Agent 舆情分析系统」，核心目标是把“信息采集 -> 观点提炼 -> 情绪与立场分析 -> 报告生成”串成自动化流程。官方定位强调：

1. 对国内外社媒做持续抓取与分析（README 提到覆盖 30+ 主流社媒与大量评论）。
2. 不仅靠一个 LLM，而是多引擎协同（Query/Media/Insight/Report 等）。
3. 最终产出可直接阅读的分析报告（HTML/Markdown/PDF）。

## 2. 怎么用（快速上手）

### 路径 A：Docker 一键启动（推荐）

官方 README 给出的最短路径：

```bash
cp .env.example .env
# 编辑 .env，填好数据库和模型 API 配置

docker compose up -d
```

关键配置点：

- 数据库默认是 PostgreSQL（`DB_HOST=db`, `DB_PORT=5432` 等）。
- LLM 调用遵循 OpenAI 兼容接口规范（可替换到兼容提供商）。

### 路径 B：源码启动（便于二开）

```bash
# Python 3.11 环境（conda 或 uv 均可）
pip install -r requirements.txt
playwright install chromium
python app.py
```

适合你要做的事情：

- 调整 Agent 策略（检索深度、反思轮次、报告模板）。
- 插入自己的数据源与过滤规则。
- 把报告结果接入内部 BI 或知识库。

## 3. 原理拆解（为什么它能做“舆情分析”）

根据仓库结构和 README 信息，可以把系统理解成四层：

1. 数据层：采集网页/社媒内容与评论，形成原始素材。
2. 分析层：不同 Agent 分工（检索、媒体视角、洞察、情绪/倾向等）。
3. 编排层：调度器把多 Agent 结果做融合、去重、对齐。
4. 交付层：Report Engine 将结构化中间结果渲染为可读报告。

这种设计相比“单轮提问一个大模型”更稳的原因：

- 可追溯：每一步有中间产物，不是黑箱一次性输出。
- 可控：你能单独调一个子引擎而不影响全链路。
- 可扩展：新接一个信源或模板，只改局部模块。

## 4. 你可以直接借鉴的工程点

1. 多引擎解耦目录结构（`QueryEngine` / `MediaEngine` / `InsightEngine` / `ReportEngine`）。
2. 支持“重渲染”脚本（`regenerate_latest_html.py` / `regenerate_latest_md.py` / `regenerate_latest_pdf.py`），便于对同一批分析结果做不同交付格式。
3. Web + 命令行双入口，适配“运营同学看报告”和“工程同学跑批任务”两种使用场景。

## 5. 风险与落地建议

1. 合规风险：涉及社媒抓取时，要评估平台协议、地区法律与企业合规边界。
2. 幻觉风险：报告层应加“来源引用+置信度”约束，避免模型过度归纳。
3. 时效风险：热点事件窗口很短，建议把抓取/分析任务做成定时批处理。
4. 成本风险：多 Agent + 长文本报告会放大 token 成本，建议分层缓存与分级推理。

## 6. 一个可执行的最小实践

1. 选一个话题（例如某品牌新品发布）。
2. 先做 24 小时窗口抓取，生成第一版报告。
3. 人工复核 10 条关键结论与原始引用是否一致。
4. 再扩大到 7 天窗口，观察情绪与主题漂移。
5. 输出“可行动建议”（公关、投放、产品反馈）并复盘准确率。

## 7. 参考来源

- GitHub 仓库主页：https://github.com/666ghj/BettaFish
- README（项目说明、快速开始、目录结构）：https://github.com/666ghj/BettaFish/blob/main/README.md
- GitHub Trending（今日榜单页）：https://github.com/trending
