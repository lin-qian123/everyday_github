<!-- markdownlint-disable MD013 -->

# 2026-07-28 AI 热点日报

> 抓取时间：2026-07-28（Asia/Shanghai）。GitHub 信号来自 GitHub REST API 与项目 README；stars/forks 为抓取时快照。下列仓库均在 07-27 创建，须视为“早期开发者信号”，不等同于 GitHub 全站 Trending 或成熟生产推荐。社媒互动量未能独立复核时不编造。

## 今日判断

- 今日新仓库的共同方向不是训练新模型，而是把 agent 放入具体工程环节：命名、文风、端点诊断、模型路由、群体审议和实体设备控制。
- 最值得保留的不是“多 agent”标签本身，而是可审计边界：`llm-endpoint-doctor` 检查真实协议能力，`council-lab` 暴露预算与过程，`stackchan-cloud-mcp` 明确单租户和传感器隐私。

## GitHub 热点项目

| 项目 | 可核验信号 | 分类 | 评价 |
| --- | --- | --- | --- |
| [`letsfinddomain-skill`](../../projects/letsfinddomain-skill/README.md) | 07-27 创建；约 61 stars、4 forks；MIT。 | Agent 框架与技能生态 | 将域名可用性与续费成本接进 agent，但商标审查仍需人工。 |
| [`oil-tone`](../../projects/oil-tone/README.md) | 07-27 创建；约 36 stars、3 forks；MIT。 | Agent 框架与技能生态 | 中文写作规则 + 确定性 lint，适合做可版本化的改稿实验。 |
| [`open-free-router`](../../projects/open-free-router/README.md) | 07-27 创建；约 10 stars、2 forks；MIT。 | 模型、训练与推理基础设施 | 聚合免费模型上游的本机路由层；密钥、日志和服务条款是关键边界。 |
| [`council-lab`](../../projects/council-lab/README.md) | 07-27 创建；约 9 stars、2 forks；Apache-2.0。 | 前端、UI 与 Agent 交互层 | 让多模型按顺序可见地审议，但不替代外部事实核验。 |
| [`stackchan-cloud-mcp`](../../projects/stackchan-cloud-mcp/README.md) | 07-27 创建；约 8 stars、2 forks；MIT。 | 语音、视频与多模态 | 具身 MCP 的部署笔记价值高；远程摄像头/麦克风与 OAuth 面必须先审计。 |
| [`llm-endpoint-doctor`](../../projects/llm-endpoint-doctor/README.md) | 07-27 创建；约 6 stars；MIT。 | Coding Agents 与终端助手 | 用真实小探针验证中继的流式与工具循环，适合作为接入前检查。 |

## X、Instagram 与 YouTube 观察

- X：从 [OpenAI 官方账号](https://x.com/OpenAI) 可持续跟踪 agent 与开发者动态；本轮未能独立确认 07-28 与上述六个早期仓库直接相关的作者/官方单帖，因此不将通用平台活跃度写成项目热度，也不填互动数。
- GitHub：[Trending](https://github.com/trending) 页面是当天探索入口；它显示 agent 工具仍占显著位置，但不给上述新仓库提供固定 AI 名次。项目级创建时间、stars/forks 以各自 [GitHub API](https://api.github.com/search/repositories?q=%28agent+OR+llm+OR+ai%29+created%3A2026-07-27&sort=stars&order=desc&per_page=100) 快照为准。
- Instagram：从 [OpenAI 官方账号](https://www.instagram.com/openai/) 可观察多模态与创作内容；登录、地区与动态排序使本轮无法独立复核日榜或关联贴，故仅列为观察入口。
- YouTube：从 [OpenAI 官方频道](https://www.youtube.com/@OpenAI) 可跟踪产品演示；本轮未检索到与表中六个仓库直接相关的当天官方视频，不把频道内容当作项目传播证据。

## 后续跟踪

- 用非生产 key 回归 `llm-endpoint-doctor` 的 `/models`、SSE 和工具循环报告，并核对计费。
- 对 `open-free-router` 审计安装脚本、配置落盘、日志脱敏与非 loopback 暴露情形。
- 对 `council-lab` 以带标准答案的决策集比较单模型与多席位结果，并把外部证据核验作为独立步骤。
- 对 `stackchan-cloud-mcp` 先进行网络隔离、密钥轮换和摄像头/麦克风可见同意设计，再考虑真实远程部署。
