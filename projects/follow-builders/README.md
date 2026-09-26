<!-- markdownlint-disable MD013 -->

# Follow Builders（zarazhangrui/follow-builders）

> 上游仓库：<https://github.com/zarazhangrui/follow-builders> · 归类：办公、商业与行业应用 · 本页基于 2026-09-26 的 GitHub API、README、SKILL 与 feed 文件静态整理，未安装 Skill、订阅中心 feed、创建定时任务或发送 Telegram / Email。

- 抓取快照：6,794 stars、887 forks、57 open issues。
- 热度信号：GitHub JavaScript Trending 抓取时约 +7 当日 stars。
- 版本与许可：无 GitHub Release / tag；README 声称 MIT，但 API 未识别 SPDX，根目录快照未见 LICENSE 文件。

## 定位

Follow Builders 是面向 OpenClaw、Claude Code 等 Agent 的 AI 行业资讯 Skill。它从一组经过策展的 X 账号、YouTube 播客和官方博客生成日报或周报，强调跟踪实际建设者而不是泛流量账号，并支持按语言、长度、主题和交付渠道重组摘要。

## 用法

用户把仓库安装成 Skill 后，可按需调用 `/ai`，或在 onboarding 中选择每日 / 每周频率、时区、语言和交付方式。OpenClaw 路径调用自身 cron 与消息渠道；其他终端 Agent 需要系统 crontab 加 Telegram bot 或 Resend 邮件，也可以只保留当前会话中的按需输出。

## 原理

上游中心任务每天从博客抓取、YouTube transcript 服务和 X 官方 API 汇集公开内容，生成公共 feed；本地 Skill 发起一次 HTTP 请求获取 feed，再由当前 Agent 按用户偏好改写为摘要。配置、阅读历史和可选交付密钥保存在 `~/.follow-builders`，来源清单与默认 prompt 随仓库维护。

## 价值

它把多平台追踪、转录和基础清洗从每个用户的运行环境移到共享 feed，降低 API key 与定时抓取成本；Skill 形式又允许用户用现有 Agent 选择语言、深度和交付渠道。固定来源表便于复核“看了谁”，也比不可解释的推荐流更容易做长期对照。

## 风险边界

- “无需 API key”来自中心化 feed，不等于无第三方依赖；上游可以改变来源、筛选、正文、更新时间和可用性，本地用户看不到 X / YouTube 抓取的完整执行证据。
- feed 与公开帖子都是不可信输入，可能包含 prompt injection、错误信息或营销内容；让 Agent 直接“remix”不能替代原文链接、事实核验和利益冲突检查。
- Telegram / Email 模式会读取本地 token 并向外部服务发送摘要；OpenClaw channel 也有自己的身份、retention 和目标选择边界。
- 默认追踪名单体现维护者选择，不代表全行业覆盖或中立排序；X、YouTube、博客的可见性和转录质量也不对等。
- README 声称 MIT，但根目录没有独立 LICENSE 且 API 未识别 SPDX；转载代码、prompt 或 feed 前应先澄清许可和内容再分发权利。

## 补充建议

首次只用 stdout / 按需模式，不配置消息密钥；保存每次 feed 时间戳、原始链接和摘要 prompt，抽样对照 X 原帖、YouTube transcript 与博客全文。为 feed 内容加引用保留、域名 allowlist、prompt-injection 隔离和“无法核实”标记；对来源增删、连续缺更和中心 feed hash 建立告警。

## 参考资料

- [GitHub 仓库](https://github.com/zarazhangrui/follow-builders)
- [GitHub REST API](https://api.github.com/repos/zarazhangrui/follow-builders)
- [README](https://github.com/zarazhangrui/follow-builders/blob/main/README.md)
- [SKILL.md](https://github.com/zarazhangrui/follow-builders/blob/main/SKILL.md)
- [X feed](https://github.com/zarazhangrui/follow-builders/blob/main/feed-x.json)
- [Podcast feed](https://github.com/zarazhangrui/follow-builders/blob/main/feed-podcasts.json)
