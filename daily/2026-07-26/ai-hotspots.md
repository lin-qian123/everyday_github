<!-- markdownlint-disable MD013 -->

# 2026-07-26 AI 热点日报

> 抓取时间：2026-07-26（Asia/Shanghai）。GitHub 数据来自 GitHub REST API：下列项目均创建于 2026-07-25，star/fork 为抓取时快照，并结合项目 README、许可证与安装说明核对。它们均只有 2--4 stars，是新仓库的早期开发者信号，不等同于 GitHub 全站 Trending 或成熟推荐。社媒互动量在无法独立复核时不编造。

## 今日判断

- 今天的样本把焦点从“再造一个 agent”转向 agent 的输入、交付和验收表面：上下文压缩、PDF 批注回写、文档 schema 统一与签名交付都在解决可用性与可复核性。
- 本地优先仍是重要叙事，但含义并不相同：端侧多模态强调原始音视频不出机，桌面知识工作台仍涉及模型、MCP、浏览器与运行时边界；不能把“本地”直接等同于安全。
- 所有项目上线不足两天，星标只能反映初始发现度。可靠性、性能、许可证适配、模型供应链、跨平台与团队维护必须通过独立试验判断。

## GitHub 热点项目

| 项目 | 可核验信号 | 分类 | 评价 |
| --- | --- | --- | --- |
| [`Kition`](../../projects/kition/README.md) | 07-25 创建；3 stars；0 forks；beta；AGPL-3.0。 | 办公、商业与行业应用 | 将文档、表格、浏览器研究和工作流合到桌面工作台；公开客户端不等于完整可重建运行时。 |
| [`Verchestra`](../../projects/verchestra/README.md) | 07-25 创建；4 stars；0 forks；`0.0.0-qualification`；GPL-3.0-only。 | Agent 框架与技能生态 | 用签名证据、policy gate 与人工审批组织 AI 交付；当前没有公开安装器。 |
| [`ctx-diet`](../../projects/ctx-diet/README.md) | 07-25 创建；2 stars；0 forks；MIT；作者自测 65.6% 输入 token 节省。 | Coding Agents 与终端助手 | PostToolUse 压缩直击长会话成本，但效果和错误保真必须独立回归验证。 |
| [`MagicTeX-mcp`](../../projects/MagicTeX-mcp/README.md) | 07-25 创建；2 stars；0 forks；npm/MCP Registry；AGPL-3.0。 | 前端、UI 与 Agent 交互层 | 用 PDF 锚定批注驱动 agent 修改 LaTeX；WASM 编译覆盖与隐私边界需实测。 |
| [`Docvion`](../../projects/docvion/README.md) | 07-25 创建；2 stars；1 fork；PyPI；MIT。 | RAG、检索与知识处理 | 为多种解析器提供统一文档 schema；中立层不代表 OCR/布局精度自动等价。 |
| [`OpenEyes-Live`](../../projects/OpenEyes-Live/README.md) | 07-25 创建；2 stars；0 forks；Apache-2.0；Python 3.10+。 | 语音、视频与多模态 | 端侧可插拔视觉/语音引擎有明确模块化价值，但摄像头、声纹与模型供应链风险很高。 |

## X、Instagram 与 YouTube 观察

- X：可从 [OpenAI 官方账号](https://x.com/OpenAI) 追踪 agent、多模态和开发者内容。本轮未找到能够独立核验为 07-26 发布、且直接对应上表六个早期项目的官方或作者单帖，因此不把账号活跃度伪作项目热度，也不记录不可复核互动数。
- GitHub：上述项目的创建时间、stars/forks、描述与许可证以各自仓库 REST API 返回为准；[GitHub Trending](https://github.com/trending) 可作为当天全站探索入口，但没有提供可用于本报告逐项复核的固定 AI 排名快照。
- Instagram：从 [OpenAI 官方账号](https://www.instagram.com/openai/) 可进入生成式 AI 产品与创作内容；登录、地区和动态排序限制使本轮不能独立确认 07-26 单帖的发布时间、播放或点赞，故只保留可追溯入口。
- YouTube：从 [OpenAI 官方频道](https://www.youtube.com/@OpenAI) 可查看 agent 与多模态演示。本轮没有检索到可独立确认在当天发布、并与上表仓库直接相关的单条视频，故不将频道本身表述成日榜或热度证据。

## 后续跟踪

- 为 `ctx-diet` 建立保留原始输出的回归夹具，评估节省率与诊断丢失之间的权衡。
- 对 `Verchestra` 用无生产权限仓库演练 policy 拒绝、证据 digest 不一致与人工批准流程，观察 qualification 设计是否可落地。
- 用含表格、公式、多语言和低清扫描的基准文档比较 `Docvion` adapter，保留原始输出并检查 schema 丢失。
- 复核 `MagicTeX-mcp` 的 WASM TeX 覆盖、导出可复现性和敏感论文边界；对 `OpenEyes-Live` 先审计模型下载、网关、录制同意和日志。
- 继续观察 `Kition` 的公开客户端/签名运行时分界、AGPL 义务以及数据在浏览器、模型和 MCP 间的实际流向。
