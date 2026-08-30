<!-- markdownlint-disable MD013 -->

# OpenMAIC

> 上游仓库：[THU-MAIC/OpenMAIC](https://github.com/THU-MAIC/OpenMAIC) · 归类：AI 学习与教育资源 · 本页基于 2026-08-31 的 GitHub Trending、REST API 与上游 README 快照整理。

## 定位

OpenMAIC（Open Multi-Agent Interactive Classroom）是清华大学 THU-MAIC 团队的开源多智能体互动课堂平台：用户输入主题或上传材料，系统生成课程大纲、幻灯片、测验、交互式 HTML、项目式学习活动和课堂互动。官方 Trending 抓取时显示约 +4,468 当日 stars；REST API 快照为 23,865 stars、4,479 forks、218 个开放 issue，默认分支最近推送于 2026-08-30，API 许可证为 MIT。它是公开关注度与代码/文档能力的信号，不等于教学效果或生产可靠性。

## 用法

最小本地路径需要 Node.js 20+、pnpm 10+ 和至少一个模型 provider：

```sh
git clone https://github.com/THU-MAIC/OpenMAIC.git
cd OpenMAIC
pnpm install
cp .env.example .env.local
pnpm dev
```

在 `.env.local` 中配置 OpenAI、Anthropic、Gemini、DeepSeek、Ollama 或其他 OpenAI-compatible provider。可先用公开主题或脱敏材料生成一节课，再检查每个场景的来源、公式、图片、互动逻辑和测验答案；需要时导出可编辑 `.pptx` 或交互式 HTML。生产部署可参考 Docker、Vercel 与 PostgreSQL-backed runtime 文档。

## 原理

- 生成链路分成“主题/材料 → 结构化课程大纲 → 场景内容”两阶段，场景可落成 slides、quiz、interactive、PBL 等类型。
- `lib/orchestration/` 使用 LangGraph 状态机管理教师、助教、同学等角色的轮次、讨论和问答；播放引擎再按 action 驱动语音、白板、聚光灯、激光笔等课堂动作。
- v1.0.0 引入 agent workbench、可恢复的服务端 session、材料面板、20 个内置 skills 与可插拔存储；运行时依赖 provider 的模型、搜索、语音、图像和持久化能力。
- 文档解析、网页搜索、TTS/ASR 和导出是独立的数据路径；`ACCESS_CODE`、provider 能力开关和 fail-loud routing 可用于限制共享部署中的暴露面。

## 价值

- 把“备课、展示、练习、讨论、反馈”放入同一可交互产物，适合课程原型、公开教材和个人学习实验。
- 多 agent 角色与白板/语音/测验组合，比纯聊天更容易观察学习流程和交互状态。
- 可编辑 PPTX、交互式 HTML、可恢复 session 和材料复用，为人工修订、课堂复盘和版本化交付提供入口。
- provider-neutral 设计允许用云端模型，也可用 Ollama、Lemonade、FunASR 等本地组件进行隐私敏感的原型验证。

## 风险边界

- 自动生成课程可能出现事实、引用、公式、图示、答案和教学顺序错误；“生成成功”不等于内容经过教师或领域专家审核。
- 上传的 PDF、音频、视频和网页内容可能包含个人数据、版权材料或提示注入；必须分离解析、检索、模型调用和导出权限。
- 多 agent 讨论会制造看似多源、实际同源的错误共识；AI 同学和 AI 教师的互动表现不能直接证明学习增益。
- GitHub README 的根许可证与仓库 API 当前都指向 MIT，但站点页面存在旧的 AGPL 表述；仓库还列出 `packages/mathml2omml` 的 LGPL-3.0-or-later 等第三方条款，商业分发前应逐文件核验。
- 网页搜索、OpenClaw、provider API、TTS/ASR 和远程数据库会扩大网络、凭据、成本与数据留存边界；不应把本地运行默认理解为完全离线。

## 补充建议

1. 用公开教材或合成材料建立固定 fixture，逐场景回到原文核验事实、引用、公式、图片和测验评分。
2. 先关闭 OpenClaw、网页搜索、远程音频和自动写入，只验证大纲、场景 schema、导出和 session 恢复，再逐项打开能力。
3. 为每次课程保存 commit、模型/provider、提示、材料哈希、生成日志和人工修改记录；对敏感课堂使用本地模型或脱敏副本。
4. 将学习效果作为独立的前后测或受控教学研究问题，不用 stars、演示视频或课程数量替代教育评估。

## 参考资料

- [上游 README、Quick Start 与架构说明](https://github.com/THU-MAIC/OpenMAIC)
- [OpenMAIC 中文项目页](https://openmaic.io/zh/)
- [OpenMAIC v1.0.0 Changelog](https://github.com/THU-MAIC/OpenMAIC/blob/main/CHANGELOG.md)
- [REST API 元数据](https://api.github.com/repos/THU-MAIC/OpenMAIC)
- [GitHub Trending](https://github.com/trending)
