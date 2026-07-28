<!-- markdownlint-disable MD013 -->

# 2026-07-29 AI 热点日报

> 抓取时间：2026-07-29（Asia/Shanghai）。项目创建时间、stars、forks 和许可证来自 GitHub REST API 快照及项目原始 README；数值会持续变化。下表项目均创建于 07-28，属于“早期开发者信号”，并不代表 GitHub 全站 Trending 或生产成熟度。社媒页面可访问性与帖文排序受登录、地区和时间线影响；未独立复核的互动量一律不填写。

## 今日判断

- 07-28 的新增信号横跨两条主线：一条是让 coding agent 更可控（极简规则、并行协作、授权安全测试），另一条是把大模型放回可观测的本机/训练实验（MoE 按需缓存、JAX 并行训练）。
- 最值得谨慎跟踪的并非“用了 agent”本身，而是边界是否落到可执行机制：`succubus` 有 advisory lease，`frieren-dast-ai` 必须有书面授权，`dreamvault` 用检索隔离而非仅提示词声明。

## GitHub 热点项目

| 项目 | 可核验信号 | 分类 | 评价 |
| --- | --- | --- | --- |
| [`ponytail-improved`](../../projects/ponytail-improved/README.md) | 07-28 创建；约 378 stars、55 forks；MIT。 | Coding Agents 与终端助手 | 将“先复用后新增”固化为 skill/hook；项目自报节省幅度尚缺独立基准。 |
| [`deltafin`](../../projects/deltafin/README.md) | 07-28 创建；约 73 stars、5 forks；API 未声明 SPDX 许可证。 | 模型、训练与推理基础设施 | Apple Silicon 跑超大 MoE 的透明实验，但磁盘、延迟、网络和上游许可成本极高。 |
| [`frieren-dast-ai`](../../projects/frieren-dast-ai/README.md) | 07-28 创建；约 18 stars；Apache-2.0。 | Agent 框架与技能生态 | 将 MITM、规则与多 agent DAST 汇总到 dashboard；只适用于明确授权的目标。 |
| [`jaxotron`](../../projects/jaxotron/README.md) | 07-28 创建；约 13 stars；Apache-2.0。 | 模型、训练与推理基础设施 | 可读的 JAX 3D 并行训练样本；真实集群稳定性和吞吐仍需自行验证。 |
| [`succubus`](../../projects/succubus/README.md) | 07-28 创建；约 8 stars、1 fork；MIT。 | Coding Agents 与终端助手 | 为并行 agent 提供任务、提问和文件租约；不能替代 Git/CI 的强质量门。 |
| [`dreamvault`](../../projects/dreamvault/README.md) | 07-28 创建；约 8 stars、1 fork；代码 Apache-2.0、文档 CC BY 4.0。 | 记忆层与个人 AI 基础设施 | 给 companion memory 提供隔离治理样本；价值主张是规范性的，检测效果未获独立验证。 |

GitHub 的当天 [Trending 页面](https://github.com/trending) 仍把 agent/video 工具放在显著位置，其中 `claude-video` 已有本仓库条目；本轮新增页改以 [07-28 创建的 AI/agent/LLM 仓库 API 搜索](https://api.github.com/search/repositories?q=%28agent%20OR%20llm%20OR%20ai%29%20created%3A2026-07-28&sort=stars&order=desc&per_page=100) 及逐仓库元数据为准，因此不把它们误写为 Trending 固定名次。

## X、Instagram 与 YouTube 观察

| 平台 | 可追溯入口与状态 | 本轮可得信号 | 讨论与边界 |
| --- | --- | --- | --- |
| X | [OpenAI 官方账号](https://x.com/OpenAI)；页面可打开，时间线完整读取受登录/动态加载影响。 | agent 与开发者发布仍应以官方账号/项目作者原帖为优先核验入口。 | 本轮未独立确认与上表六个 07-28 新仓库直接相关的作者或官方单帖；不把通用账号活跃度转写为项目热度。 |
| Instagram | [OpenAI 官方账号](https://www.instagram.com/openai/)；页面可打开，排序和完整贴文通常受登录影响。 | 适合作为多模态、创作型产品展示的观察入口。 | 无法独立核验日榜或与上述项目的直接传播链，故不填写互动数，也不做“Instagram 热传”判断。 |
| YouTube | [OpenAI 官方频道](https://www.youtube.com/@OpenAI)；频道可打开。 | 适合跟踪发布演示、开发者讲解与长视频产品说明。 | 未检索到可直接归因于这六个新仓库的当天官方视频；频道内容不能替代项目维护者的发布证据。 |
| GitHub | [Trending](https://github.com/trending)；直接可打开。 | 当天可见 `claude-video` 等 agent 工具的社区关注。 | Trending 是按页面当天快照变化的探索入口，不能反推出所有新仓库排名或长期采用。 |

## 后续跟踪

- 以小型受控任务对 `ponytail-improved` 做“代码量、缺陷率、返工率”三指标对照，而不复用其自报百分比。
- 对 `deltafin` 记录实际 cache 命中、磁盘增量、首 token/每 token 延迟和断点下载恢复；只在 loopback 与低权限测试客户端试验。
- 在靶场先运行 `frieren-dast-ai` 的被动扫描，审计 CA、会话存储、scope 和停止条件后再决定是否启用主动插件。
- 用二会话冲突、daemon 中断和 lease 过期案例回归 `succubus`；继续把 merge、测试和安全审查交给 Git/CI。
- 用合成矛盾记忆评估 `dreamvault` 的漏隔离、误隔离与检索泄漏，并另行设计删除、导出、加密和人工申诉流程。
