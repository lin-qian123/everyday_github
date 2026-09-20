<!-- markdownlint-disable MD013 MD034 -->

# AutoClip：从长视频自动提取高光并生成合集的 AI 流水线

> 上游仓库：https://github.com/zhouxiaoka/autoclip · 归类：语音、视频与多模态 · 本页基于 2026-09-21 的 README、CLI / MCP 文档、security、release、manifest 与许可证静态整理；未下载 YouTube / B 站素材、调用模型、启动 worker 或生成成片。

## 定位

AutoClip 是面向长视频二创的 AI 高光提取系统：从 URL 或本地文件准备素材，分析字幕和内容，划分话题区间、打分片段、生成标题与合集，再输出剪辑结果。它同时提供 Web、CLI、stdio MCP 和 Agent skill，不应被理解为已经证明“最佳片段”判断或平台授权的自动发布系统。

2026-09-21 的 GitHub 官方 Python Trending 抓取显示约 `+325 stars today`；REST API 快照为 `7,881 stars / 1,543 forks / 14 open issues`，MIT，最新 release 为 `v1.3.0`（9 月 20 日）。

## 用法

上游提供 Docker、完整本地服务和轻量 CLI / MCP 三种路径；最小本地模型流程可使用 Ollama：

```sh
pip install -r requirements.txt
pip install -e .
autoclip run talk.mp4 --provider ollama
autoclip mcp
```

完整 Web 部署还包括 FastAPI、React、Celery、Redis、SQLite / PostgreSQL、FFmpeg 与文件存储。worker 必须订阅项目配置的专用 queues，否则任务会停在 `processing`。

## 原理

- downloader / upload layer 取得视频、字幕和 metadata；yt-dlp 覆盖 YouTube、B 站等来源。
- FastAPI 保存项目与任务状态，Celery + Redis 运行耗时 pipeline，WebSocket 向前端推送进度。
- 模型先提取大纲和时间线，再对候选片段评分、命名并推荐合集；FFmpeg 负责实际切片与合成。
- provider 可使用通义千问、OpenAI-compatible、Gemini、SiliconFlow 或本地 Ollama / LM Studio。
- CLI、桌面 / Web 和 MCP 共享项目产物；Agent skill 将常见步骤封装成可调用工作流。

## 价值

- 把下载、理解、候选选择、剪辑、合集和结果管理串成可观察的异步流程。
- 本地模型路径可降低文本外发，但视频下载、平台 cookies、模型、日志和文件存储仍须分别审计。
- CLI / MCP 让已有 Coding Agent 能从同一 pipeline 生成与检查素材，而非重复实现剪辑脚本。
- 人工仍可在结果页修改片段标题、排序合集并下载，适合作为半自动剪辑起点。

## 风险边界

- URL 可下载不等于拥有复制、剪辑、配音、再发布或商业使用权；平台条款、版权、肖像、音乐与隐私须逐条确认。
- “精彩评分”和标题由模型生成，会受字幕错误、语言、时长、prompt 和 provider 影响；不能视为传播效果证明。
- cookies、API keys、原视频、字幕、SQLite / Redis 状态、worker 日志和输出目录都可能包含敏感内容。
- README 将 B 站上传、账号管理、字幕编辑、移动端、批处理等标为开发中，不能按已交付功能宣传。
- 本页未运行 `v1.3.0`，未验证 queue 路由、断点恢复、模型离线性、成片质量或平台兼容性。

## 补充建议

1. 先用自有、明确授权的短视频和本地 Ollama，固定模型、prompt、FFmpeg 与 commit 建小型金标集。
2. 对时间线、保留 / 删除片段、字幕、标题和成片音画同步分别人工验收，不只看 AI score。
3. cookies 与 provider keys 使用专用低权限账号和 secret store；Web / Redis / worker 不直接暴露公网。
4. 发布前执行权利清单、内容审核、平台规则检查与人工确认；自动上传功能即使完成也默认关闭。

## 参考资料

- 上游 README：https://github.com/zhouxiaoka/autoclip
- CLI / MCP 文档：https://github.com/zhouxiaoka/autoclip/blob/main/docs/CLI_AND_MCP.md
- 安全策略：https://github.com/zhouxiaoka/autoclip/blob/main/SECURITY.md
- `v1.3.0` release：https://github.com/zhouxiaoka/autoclip/releases/tag/v1.3.0
- GitHub REST API：https://api.github.com/repos/zhouxiaoka/autoclip
- LICENSE：https://github.com/zhouxiaoka/autoclip/blob/main/LICENSE
