<!-- markdownlint-disable MD013 -->

# TokenTracker（xiufengsun/TokenTracker）

> 上游仓库：<https://github.com/xiufengsun/TokenTracker> · 归类：Coding Agents 与终端助手 · 本页基于 2026-10-01 的 GitHub API、README、Privacy、Security、Release 与 manifests 静态整理，未安装 hooks、读取本机 Agent 日志或核对费用。

- 抓取快照：1,917 stars、193 forks、40 open issues。
- 热度信号：GitHub JavaScript Trending 抓取时约 +43 当日 stars。
- 版本与许可：MIT；latest Release 与 tag 均为 `v1.1.5`。

## 定位

TokenTracker 是本地优先的 coding-agent 用量、费用与 quota 仪表盘，覆盖多种 CLI、IDE 和桌面 Agent，并提供 CLI、macOS 菜单栏、Windows / Linux tray、widget、可选排行榜与 skills manager。核心卖点是从已有本地日志抽取 token / 时间等 usage metadata，而不是上传 prompt、回复或代码正文。

## 用法

Node.js 20+ 可用 `npx tokentracker-cli` 启动；首次运行会自动安装 hooks、同步本地数据并打开 `127.0.0.1:7680` dashboard。也可安装原生桌面包。`tokentracker status`、`sync` 与 `doctor` 用于检查采集，`tokentracker uninstall` 会清理其管理的 hooks；账号、云同步、排行榜和 skill 同步均为额外功能。

## 原理

不同 provider 通过 hook、JSONL / SQLite / log 被动读取或官方 quota endpoint 接入，增量 cursor 避免重复计数；本地 `~/.tokentracker/` 保存小时桶、session、project attribution 与缓存。费用由 LiteLLM 价格表和项目 override 估算。可选账号只同步小时 usage bucket，不上传本地 session / project 队列；provider quota 读取会使用各工具已存于本机的凭据直接访问 provider。

## 价值

它将多工具使用量、模型分布、成本估算与限额集中到一个本地视图，适合同时使用 Claude Code、Codex、Cursor、Gemini、OpenCode 等工具的个人或团队。机器可读 `status --json` 也便于 CI / Agent 在不读取对话正文的前提下做预算提示。

## 风险边界

- 首次运行会修改多个 Agent 的用户级 hook / config；必须先备份并核对 `uninstall` 是否只删除受管理内容。
- parser 会读取含对话记录的本地文件，即使只保留 metadata，解析缺陷或未来变更仍属于高敏感隐私面。
- provider quota 路径会读取本地 auth token 并发出网络请求；“不经过 TokenTracker 服务”不等于没有 provider 风险。
- 默认每天发送匿名 heartbeat，并在 dashboard 启用受限 PostHog 分析；可用 `TOKENTRACKER_NO_TELEMETRY=1` 或 `DO_NOT_TRACK=1` 关闭。
- 云同步 / 排行榜、skills 目录、pet 下载和状态页会增加外部数据流；项目名 / 路径虽声明不上传，仍会明文保存在本地队列。
- 费用来自价格表和解析口径，不是供应商账单；未知模型显示 0 美元不代表免费。

## 补充建议

先在可丢弃用户 profile 和无敏感仓库中运行，比较修改前后的 Claude / Codex / IDE 配置与网络连接；默认关闭 telemetry、账号与可选 provider。抽样把小时桶、token 数和官方账单对齐，保留解析版本。共享截图前隐藏项目名、时间模式、quota 与账户信息，并限制 `~/.tokentracker` 权限和备份范围。

## 参考资料

- [GitHub 仓库](https://github.com/xiufengsun/TokenTracker)
- [GitHub REST API](https://api.github.com/repos/xiufengsun/TokenTracker)
- [README](https://github.com/xiufengsun/TokenTracker/blob/main/README.md)
- [Privacy Policy](https://github.com/xiufengsun/TokenTracker/blob/main/docs/PRIVACY.md)
- [Security Policy](https://github.com/xiufengsun/TokenTracker/blob/main/SECURITY.md)
- [v1.1.5 Release](https://github.com/xiufengsun/TokenTracker/releases/tag/v1.1.5)
- [LICENSE](https://github.com/xiufengsun/TokenTracker/blob/main/LICENSE)
