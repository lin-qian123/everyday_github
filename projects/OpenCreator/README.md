<!-- markdownlint-disable MD013 MD034 -->

# OpenCreator：以 Codex 为执行内核的本地 AI 创作工作区

> 上游仓库：https://github.com/krillinai/OpenCreator · 归类：语音、视频与多模态 · 本页基于 2026-09-21 的 README、架构 / 用户文档、release、manifest 与 REST API 静态整理；未登录 Codex、配置媒体 provider、启动 daemon 或生成内容。该仓库原名 KrillinAI。

## 定位

OpenCreator 把 Agent conversation、可视化创作 workspace 与 Codex runtime 接到同一任务状态机，用于视频翻译 / 配音、图像与视频生成、数字人、封面、下载、stick figure animation 等流程。它重用 Codex sessions、models、tools、Skills 和 MCP，而不是维护另一套独立 Agent loop。

2026-09-21 的 GitHub 官方 TypeScript Trending 抓取显示约 `+317 stars today`；REST API 快照为 `11,947 stars / 1,193 forks / 31 open issues`，API 未识别 SPDX；最新 release 为 `v3.2.1`（9 月 20 日）。README badge 声称 Apache-2.0，但根目录当前未见独立 LICENSE 文件，复用前应让上游明确许可正文。

## 用法

源码开发要求 Node.js 20+、pnpm 9.15.0、FFmpeg / FFprobe 与有效 Codex CLI 登录：

```sh
pnpm install
pnpm web:dev
# 或启动桌面开发壳
pnpm desktop:dev
```

模型与媒体服务在 Settings 中配置；`OPENCREATOR_DATA_DIR` 可隔离项目数据，`CODEX_HOME` 决定 Codex sessions、配置、Skills、MCP 和 Profiles 的实际来源。

## 原理

- Web / Electron 提供 conversation、project、workspace、approval、schedule 与 creator-tool UI。
- local daemon 连接 Codex app-server，将模型调用、工具、Skills 和 MCP 作为执行 source of truth。
- 每类创作流程建模为 source、configuration、generation、review、revision、export 状态；UI 与对话写入同一 state machine。
- SQLite 保存 projects、threads、Runs、events、schedules、memory 与 approvals；attachments、logs 和 managed workspaces 分目录持久化。
- image、video、voice、transcription provider 与 yt-dlp / FFmpeg 等 runtime component 独立管理，模型可用性取决于用户凭据和 provider 账户。

## 价值

- 把多媒体生成的中间状态、版本、人工审批与对话保存在同一工作区，减少“一条 prompt 后只剩最终文件”。
- 复用 Codex 的 session、tool、Skill 和 MCP 生态，创作 workflow 可通过 `SKILL.md` 扩展。
- 默认本地 daemon 只监听 `127.0.0.1`，API token、受控 preview、redacted diagnostics 和 system credential storage 提供基础防护。
- fake-Codex smoke、unit / integration、Playwright E2E、package verification 与 release runbook 为工程验证提供入口。

## 风险边界

- local-first 不等于所有内容留在本机：语言、图像、视频、语音和 transcription provider 会收到所配置的 prompt、素材或派生数据。
- active `CODEX_HOME` 可能包含真实 sessions、Skills、MCP 与 profile；从 UI 安装或修改它们会影响用户级 Agent 环境。
- yt-dlp、下载素材、数字人、声音克隆、字幕翻译和模板资源涉及平台条款、版权、肖像、声音同意和再分发许可。
- README 的 Apache badge 没有根 LICENSE 正文支撑，GitHub API 也为 `NOASSERTION`；不能据 badge 直接作商业复用结论。
- 本页未验证 `v3.2.1` 的实际 package、ASAR integrity、credential store、provider 数据流或生成质量。

## 补充建议

1. 使用专用 `OPENCREATOR_DATA_DIR` 与隔离 `CODEX_HOME`，只安装经过审查的 Skills / MCP。
2. 从自有短素材、低额度 provider key 和只读 workflow 开始，记录每一步输入、provider、费用、输出与审批。
3. 对语音 / 肖像授权、素材许可证、翻译准确性、字幕同步和最终发布建立独立人工 gate。
4. 在许可证澄清前仅作评估；部署前运行 test、typecheck、build、fake runtime smoke 和 packaged-app verification。

## 参考资料

- 上游 README：https://github.com/krillinai/OpenCreator
- 用户指南：https://github.com/krillinai/OpenCreator/blob/master/docs/opencreator-user-guide-and-troubleshooting.md
- Runtime 设计：https://github.com/krillinai/OpenCreator/blob/master/docs/2026-07-03-codex-native-agent-runtime-design.md
- `v3.2.1` release：https://github.com/krillinai/OpenCreator/releases/tag/v3.2.1
- GitHub REST API：https://api.github.com/repos/krillinai/OpenCreator
- 根目录内容 API（许可证核对）：https://api.github.com/repos/krillinai/OpenCreator/contents
