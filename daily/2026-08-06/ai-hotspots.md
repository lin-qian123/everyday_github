<!-- markdownlint-disable MD013 -->

# 2026-08-06 AI 热点日报

> 抓取时间：2026-08-06（Asia/Shanghai）。创建时间、stars、forks 与许可证来自 GitHub REST API 快照，之后会变化。下表项目均创建于 2026-08-05，是早期开发者信号，不代表 GitHub 全站 Trending 或生产成熟度。X、Instagram、YouTube 的搜索与时间线受登录、索引和动态加载影响，未独立复核的互动量不填写。

## 今日判断

- 新仓库最清晰的信号不是新模型，而是“把 agent 产出变成可编辑工作物”：`open-kimi-ppt-skill` 交付 PPTD 加 PPTX，`human-writing` 把写作材料与修订规则打包成 skill；两者的首日 star 较高，但都不足以说明交付质量或长期兼容性。
- Agent 基础设施继续向可控输入与上下文成本延伸：`SparkFetch` 负责把网页变成 LLM 输入，`zeromem` 试图把历史 turn 变成零 LLM 调用的检索记忆，`portable-agent-skills` 和 `hud-mode` 则分别关注执行前 gate 与执行中可观测性。

## GitHub 热点项目

| 项目 | 可核验信号 | 分类 | 评价 |
| --- | --- | --- | --- |
| [`human-writing`](../../projects/human-writing/README.md) | 08-05 创建；约 1,013 stars、99 forks；MIT。 | Agent 框架与技能生态 | 中文写作 skill 的早期高热入口，强调材料和逐段修订；“活人感”属主观目标，仍需要事实与版权审核。 |
| [`open-kimi-ppt-skill`](../../projects/open-kimi-ppt-skill/README.md) | 08-05 创建；约 550 stars、155 forks；MIT。 | 办公、商业与行业应用 | 以 PPTD 中间层交付可编辑 PPTX；明确非官方逆向实现，应隔离安装并测试兼容性。 |
| [`SparkFetch`](../../projects/sparkfetch/README.md) | 08-05 创建；约 37 stars、8 forks；MIT。 | RAG、检索与知识处理 | 自托管抓取/抽取 API，适合 Web context 接入；抓取授权、注入防护与正文正确性需在外部控制。 |
| [`portable-agent-skills`](../../projects/portable-agent-skills/README.md) | 08-05 创建；约 11 stars、0 forks；MIT。 | Agent 框架与技能生态 | 将研究、部署前检查与 skill 安全扫描写成可移植流程；静态 PASS 不等于运行时安全。 |
| [`hud-mode`](../../projects/hud-mode/README.md) | 08-05 创建；约 8 stars、0 forks；MIT。 | Coding Agents 与终端助手 | 将多个 coding CLI 的事件流压缩为可交互仪表；会改动用户级配置，状态面板不能替代工程验收。 |
| [`zeromem`](../../projects/zeromem/README.md) | 08-05 创建；约 8 stars、0 forks；MIT。 | 记忆层与个人 AI 基础设施 | 原始 turn 驱动的图、时间与混合检索实现；论文映射和零 token 口径尚未由本仓库独立复现。 |

候选来自 [08-05 创建的 AI/agent/LLM/MCP 仓库 API 搜索](https://api.github.com/search/repositories?q=created%3A2026-08-05+%28agent+OR+ai+OR+llm+OR+mcp%29&sort=stars&order=desc&per_page=100)、项目 README 与 [GitHub Trending](https://github.com/trending) 观察入口。首日 star 易受作者网络和小样本影响，因此不表述为固定 Trending 名次或长期采用率。

## X、Instagram 与 YouTube 观察

| 平台 | 可追溯入口与状态 | 本轮可得信号 | 讨论与边界 |
| --- | --- | --- | --- |
| X | [human-writing 搜索入口](https://x.com/search?q=%22human-writing%22%20KKKKhazix&src=typed_query)；搜索结果读取受登录与动态加载影响。 | 本轮没有取得可独立核验的原帖时间或互动量。 | 不将 GitHub stars 归因于 X，也不写“X 热传”结论。 |
| Instagram | [AI writing 标签入口](https://www.instagram.com/explore/tags/aiwriting/)；公开标签搜索。 | 未独立核验与上述任一项目对应的当日贴文或互动量。 | 不以泛 AI 写作内容替代项目级传播证据。 |
| YouTube | [open-kimi-ppt 搜索入口](https://www.youtube.com/results?search_query=open-kimi-ppt-skill)；可作为 demo 观察入口。 | 未独立核验当天发布或观看数据。 | 不将仓库 README 中的示例或本地演示等同于 YouTube 平台热度。 |
| GitHub | [Trending](https://github.com/trending) 与上述 API 查询。 | 六个候选首日约 8--1,013 stars；创建日期、fork 与许可证均可由 API 复查。 | 这是本轮唯一的量化发现信号，且仍是早期、小样本观察。 |

## 后续跟踪

- 用有来源的中文材料对 `human-writing` 测试事实遗漏、风格误伤与编辑返工；对 `open-kimi-ppt-skill` 复查 npm 包、文件写入范围、字体授权及跨 Office 渲染。
- 在 allowlist 与限速下测试 SparkFetch 的 crawl 范围、正文准确性和网页 prompt injection 清洗；对 `zeromem` 用合成对话评估跨会话泄漏、删除和离线检索误差。
- 在隔离环境审阅 `portable-agent-skills` 的脚本与真实运行时权限；安装 `hud-mode` 前记录各用户级配置的备份，并验证卸载和敏感链接留存行为。
