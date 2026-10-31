<!-- markdownlint-disable MD013 -->

# anarlog

- 上游：[fastrepl/anarlog](https://github.com/fastrepl/anarlog)；分类：办公、商业与行业应用。
- 核读：2026-11-01（Asia/Shanghai）；固定主线 `5e9c98edb0dca47c28171ea54083200a374920f5`。
- [仓库 API](https://api.github.com/repos/fastrepl/anarlog) 快照：9,716 stars / 820 forks / 25 open issues（含 PR）；发行首项 [desktop_v1.4.34](https://github.com/fastrepl/anarlog/releases/tag/desktop_v1.4.34)，2026-10-29 UTC。发行与主线分别看。
- 证据：上游文档及指定文件静态核读；本轮未安装运行、调用模型或复现作者实验。

## 定位

Tauri / React / Rust 构建的本地优先会议笔记应用，捕获设备音频，提供转写、摘要、聊天和 Markdown 导出，不需要会议 bot 加入参会列表。官方 Rust daily 榜本轮显示 +45 stars。仓库原名 Hyprnote，短暂使用过 char；当前团队的 char 产品与本仓库分开，README 明确 Anarlog 继续维护。

## 用法

按固定 README 的下载入口选择平台制品。安装后先查看 **Settings → Transcription** 和 **Settings → Intelligence**：前者选择转写，后者选择摘要 / 聊天。支持条件允许时，可用设备端转写模型，加 Ollama / LM Studio 等本地 Intelligence。

首次试用先录一段已获许可的测试音频，生成摘要、人工编辑并导出 Markdown，再检查音频保留期。**Settings → Meetings → Audio → Audio file retention** 提供 Don't save 到 Forever 等选项；**Settings → Privacy** 分别控制 Share usage data (PostHog) 和 Error。

源码构建按当前 README 需要 Node 22+、pnpm 11.1.1、Rust 1.94.0、process-compose 1.122.0+ 及 Tauri 系统依赖；Apple Silicon 还需完整 Xcode 的 Metal Toolchain。`pnpm dev:desktop` 与含 API / Supabase 的完整开发栈分别配置，不能照搬旧 Hyprnote 教程。

## 原理

采音 → 转写 → 本地 SQLite / 文件 → 所选模型摘要，是相互独立的环节。转写可本机或 hosted，摘要可本机、用户 key 或 managed cloud。主线文档中 Cloud 转写优先 Soniox 5，managed Auto Intelligence 经 OpenRouter 使用 Claude Sonnet alias；这些动态路由应以实际 Settings 显示为准。

Cloud Sync 提供可选加密同步；分享会上传选中的内容；Cloud API & Connectors 则可另行上传服务端可读的会议数据，供远端 Agent 使用。三种能力不能仅凭“云功能”合并为同一种数据流。

## 价值

将记录、转写与模型选择拆开，并提供本地可读数据与导出，适合需要自行管理会议资料的个人和团队。价值需由口音 / 噪声条件下的逐字准确率、行动项可靠性和导出恢复能力确认。

## 风险边界

- “没有 bot”不意味着不采集音频，录音前仍需确认参会者授权。本地转写也不能保证云摘要、搜索、日历、分享或 connectors 不外发。
- 主线 settings schema 中 `telemetry_consent` 与 `crash_reporting_consent` 默认 true；Privacy 文档说明 PostHog 开关同时控制产品统计和桌面 session replay。它们与模型数据发送是独立开关；本轮未抓包或核发行二进制行为。
- Don't save 仍会在录制中使用有限临时音频以恢复缺口，停止 / 清理后删除；不能解释为从不写临时文件。音频过期后笔记和 transcript 仍保留。
- 社区层 MIT，`enterprise/**` 商业许可；公开可读企业源码不代表可按 MIT 再分发。名称变更不代表本仓库就是当前 char 产品代码。

## 补充建议

用授权短会对照人工稿，逐项核姓名、数字、说话人和行动项；测试断网、关闭统计、临时音频清理、导出 / 恢复。若要求全本地，同时选择本地转写与 Intelligence，并关闭不需要的 sync、sharing、Cloud API 与 hosted 功能，再用实际网络观测验收。

## 参考资料

- [固定 README / 名称与工作流](https://github.com/fastrepl/anarlog/blob/5e9c98edb0dca47c28171ea54083200a374920f5/README.md)。
- [模型与路由](https://github.com/fastrepl/anarlog/blob/5e9c98edb0dca47c28171ea54083200a374920f5/docs/models-and-providers.mdx)。
- [数据流、保留与开关](https://github.com/fastrepl/anarlog/blob/5e9c98edb0dca47c28171ea54083200a374920f5/docs/data-and-privacy.mdx)。
- [主线默认设置](https://github.com/fastrepl/anarlog/blob/5e9c98edb0dca47c28171ea54083200a374920f5/apps/desktop/src/settings/schema.ts)。
- [Privacy 设置入口](https://github.com/fastrepl/anarlog/blob/5e9c98edb0dca47c28171ea54083200a374920f5/apps/desktop/src/settings/privacy/index.tsx)。
- [社区与企业许可边界](https://github.com/fastrepl/anarlog/blob/5e9c98edb0dca47c28171ea54083200a374920f5/LICENSING.md)。
- [企业许可提示](https://github.com/fastrepl/anarlog/blob/5e9c98edb0dca47c28171ea54083200a374920f5/LICENSE.enterprise)。
