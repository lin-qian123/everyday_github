<!-- markdownlint-disable MD013 MD034 -->

# youtube-automation-agent：审批优先的 YouTube 生产流水线

> 上游仓库：https://github.com/darkzOGx/youtube-automation-agent · README 中称 AgentTube · 归类：语音、视频与多模态 · 本页基于 2026-09-16 的 README、package、`.env.example`、release、LICENSE 与 GitHub REST API 静态整理；未连接模型、YouTube 账号或生成/上传视频。

## 定位

`youtube-automation-agent` 是一个自托管的 YouTube 内容生产与运营工作台。它把选题、研究、脚本、配音、视觉素材、视频装配、metadata、权利/事实审阅、排期、发布和 analytics 拆成持久化阶段，并强调默认在人工批准前不进入发布队列。

2026-09-16 的 GitHub 官方 JavaScript Trending 抓取显示约 `+62 stars today`；REST API 快照为 `3,490 stars / 1,013 forks / 15 open issues`，MIT。master 的 package / README 为 `2.10.0`，但 GitHub 最新 Release 仍是 `v2.4.0`（2026-07-16），版本面存在明显时差。

## 用法

Node.js 要求 `>=18`，快速开始为：

```sh
git clone https://github.com/darkzOGx/youtube-automation-agent.git
cd youtube-automation-agent
npm install
npm run walkthrough
npm start
```

Dashboard 默认在 `http://localhost:3456`。walkthrough 会检查 FFmpeg、SQLite、provider key 与 YouTube OAuth；正式启用前应在 Production readiness 中执行小额 live probe，并单独选择是否允许付费图片/视频探测。

## 原理

- 多个职责 agent 串成生产链：研究与内容策略生成 plan，脚本/视觉/配音阶段生成带 provider 和成本证据的素材，FFmpeg/Playwright 组装成视频。
- 每个阶段写 SQLite checkpoint；中断后从首个未完成阶段继续，避免把已付费素材全部重做。
- scene manifest 记录提示词、时间轴、来源、权利状态和修订；修补一个 scene 会使相关音频、事实审阅或最终视频失效。
- 默认 approval-first：质量、事实、权利、素材与隐私 gate 未满足时不排期；疑似上传成功但无 video ID 时要求先对账。
- `2.10.0` 主分支加入可选 DarkzSEO adapter、受控标题/缩略图实验和 ROI 证据；通过 JSON stdin/stdout 调用外部审计器。

## 价值

- 将“自动生成视频”改造成可恢复、可审阅的生产状态机，比一次性脚本更容易查错和控制重复费用。
- 把事实来源、素材权利、provider task、成本与人工决定放进同一 review 流程，便于追责。
- 支持多 provider 和本地 FFmpeg，允许团队按成本、隐私和质量替换单个环节。
- Shorts、场景修补、实验和 analytics 都保留父生产记录，适合小规模内容工作室做流程评估。

## 风险边界

- README 仍以“24/7 自动化”营销，但外部发布、版权、事实、未成年人内容、广告披露和品牌风险不能交给自然语言 gate 单独决定。
- YouTube OAuth、模型 key、媒体文件、评论和 analytics 集中在本地服务；应限制 scope、端口、备份、日志与多人访问，不能因“self-hosted”就视为安全。
- provider 会接收选题、脚本、图片、声音或视频；paid probe、重试和整组重跑可能产生不可忽略的成本与数据外发。
- YouTube 重复/低质内容、AI 内容披露、版权和 monetization 政策会变化；生成成功不等于允许发布或可变现。
- GitHub Release 停在 `2.4.0`，而 master 已到 `2.10.0`；release 的 `16/16` 测试不能证明当前主分支所有新 gate、实验和 adapter 都已验证。
- 本页未授权 YouTube，也未验证 readiness、端到端视频、自动发布、恢复、费用或 analytics 归因。

## 补充建议

1. 使用测试频道、低额度 provider key 和最小 OAuth scope，默认 `private`，完成回读后再允许人工改为公开。
2. 固定 commit 与依赖 lockfile，按 master 版本建立端到端 fixture，特别测试重试、重复上传、无 video ID 和撤销排期。
3. 对每个事实声明保留来源和人工签字；对上传素材保留授权、人物同意和生成模型条款。
4. 将生成费用、人工审阅时长、版权返工、发布后更正与长期观看指标一起算，不用产量替代收益或质量。

## 参考资料

- 上游 README：https://github.com/darkzOGx/youtube-automation-agent
- 环境变量模板：https://github.com/darkzOGx/youtube-automation-agent/blob/master/.env.example
- Production 文档：https://darkzogx-youtube-automation-agent.mintlify.app/guides/first-video
- 最新 GitHub Release `v2.4.0`：https://github.com/darkzOGx/youtube-automation-agent/releases/tag/v2.4.0
- GitHub REST API：https://api.github.com/repos/darkzOGx/youtube-automation-agent
- LICENSE：https://github.com/darkzOGx/youtube-automation-agent/blob/master/LICENSE
