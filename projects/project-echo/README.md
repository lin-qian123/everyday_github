# project-echo

## 定位

`project-echo` 是 Commonwealth Bank of Australia 为档案影像整理发布的多模态检索管线：转写音频、抽取关键帧、用视觉模型描述场景，并把结果存成可搜索资料。截至 2026-08-01 的 GitHub API 快照，它创建于 2026-07-31，约 5 stars、0 forks、MIT。

## 用法

准备 Python 3.12+、`uv`、`ffmpeg`、兼容 OpenAI API 的 Whisper 与视觉/LLM 端点。运行 `uv sync` 后复制 `.env.example` 为 `.env.local`；先执行 `uv run video-annotate --dry-run`，确认输入范围，再以 `--max-files` 小批量运行。默认使用本地文件与 SQLite，也可配置 S3 和 DynamoDB。

## 原理

管线针对 `UPLOADED` 文件提取音轨、分块转写、按场景变化抽帧、批量请求视觉描述，可选地用 LLM 汇总，再持久化 transcript、summary 与状态。它用帧数、分块数、文件大小和并发上限约束下游调用量。

## 价值

- 为难以检索的录像建立文本与视觉双入口，保留可配置存储后端。
- `--dry-run`、状态机和资源上限使批处理更便于审计和控制成本。

## 风险边界

- 转写与视觉描述会出错；它们是检索线索，不能替代档案编目、人物识别或历史事实核验。
- 档案影像、音频和生成摘要可能含个人信息、版权或保密材料；须先确认处理与跨境传输授权。
- OpenAI-compatible 不等于隐私相同；第三方端点、日志保留、密钥与对象存储权限需单独审计。

## 补充建议

从已获授权的小型样本集开始，人工抽检时间戳、关键帧召回和检索误命中。为每个输出保存源文件版本、模型版本、提示词和运行参数，并设计删除、访问控制和更正流程。

## 参考资料

- GitHub：<https://github.com/Commonwealth-Bank-of-Australia/project-echo>
- 项目说明：<https://medium.com/@CommBankTechnology/preserving-commbanks-archives-with-ai-from-vhs-to-vision-models-3caff6d4f166>
- GitHub API 快照：<https://api.github.com/repos/Commonwealth-Bank-of-Australia/project-echo>
