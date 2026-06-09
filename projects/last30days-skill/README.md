# last30days-skill（GitHub AI 热门项目速览）

> 更新时间：2026-04-04（Asia/Shanghai）  
> 项目主页：https://github.com/mvanhorn/last30days-skill

## 这是什么

`last30days-skill` 是一个面向 AI 研究/内容追踪的“聚合研究技能”，核心目标是：
- 在近 30 天范围内跨平台抓取讨论（Reddit、X、YouTube、HN、Polymarket、Web 等）
- 把“热度 + 相关性 +时效性”融合排序
- 输出带引用的结论，而不是只给模型主观总结

它在 GitHub Trending（Python）里长期处于靠前区间，是近期“AI agent + research workflow”类项目里讨论度很高的一类。

## 怎么用

## 1) 安装（README 官方方式）

```bash
# Claude Code 插件方式
/plugin marketplace add mvanhorn/last30days-skill
/plugin install last30days@last30days-skill

# 或手动安装到本地 skills
git clone https://github.com/mvanhorn/last30days-skill.git ~/.claude/skills/last30days

# Codex CLI 场景
git clone https://github.com/mvanhorn/last30days-skill.git ~/.agents/skills/last30days
```

## 2) 直接跑查询

```text
/last30days [topic]
/last30days [topic] for [tool]
```

示例：
- `/last30days prompting techniques for ChatGPT for legal questions`
- `/last30days Claude Code vs Codex`

## 3) 速度/深度控制

- `--quick`：更快，覆盖更少源
- `--deep`：更慢，覆盖更多源
- `--days=N`：改时间窗（如 `--days=7` 做周报）

## 4) 渐进式解锁数据源

- 零配置可用：Reddit + HN + Polymarket
- 执行 `/last30days setup` 可自动检查 X/YouTube 能力
- 加 `EXA_API_KEY` 提升语义 web 搜索
- 加 `SCRAPECREATORS_API_KEY` 可拿到 Reddit 评论增强 + TikTok/Instagram

## 原理（为什么它结果更“像研究”）

项目文档公开了比较完整的排序思路，核心是“多信号融合”：

1. 检索层：多源并行抓取 + 查询扩展
2. 清洗层：去重、实体/账号归一化（含 X handle 解析）
3. 排序层：
   - 文本相关性（相似度、词重叠、同义扩展）
   - 互动强度（点赞/评论/播放等）
   - 权威度与跨平台共振
   - 时间衰减（越近权重越高）
4. 生成层：把高分证据组织成可执行结论，并保留引用

简单说，它不是“只让 LLM 猜趋势”，而是先做数据检索与排序，再让 LLM做归纳。

## 适合什么场景

- 追踪某个 AI 工具的真实社区反馈
- 对比两个产品（如 Claude Code vs Codex）
- 快速做“过去 7/30 天”趋势 briefing
- 为内容创作/产品定位提供“带证据”的社区观点

## 主要优点与争议

优点：
- 把“跨平台搜索 + 排序 +摘要”打包成一个可复用技能
- 配置可渐进，先跑通再加 key
- 对“近期热议”类问题非常实用

争议/限制：
- 结果质量依赖外部源可用性（平台限流、抓取稳定性）
- 深度模式耗时较长（文档给出通常 2-8 分钟）
- 某些平台指标可能受二次抓取口径影响，需要人工复核关键结论

## 参考来源

- GitHub 仓库：https://github.com/mvanhorn/last30days-skill
- README 原文（raw）：
  https://raw.githubusercontent.com/mvanhorn/last30days-skill/main/README.md
- GitHub Trending（Python 快照镜像）：
  https://github-trending.today/python
