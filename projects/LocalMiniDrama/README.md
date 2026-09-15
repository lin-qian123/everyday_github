<!-- markdownlint-disable MD013 MD034 -->

# LocalMiniDrama：本地工作台式 AI 短剧流水线

> 上游仓库：https://github.com/xuanyustudio/LocalMiniDrama · 归类：语音、视频与多模态 · 本页基于 2026-09-16 的 README、配置文档、package、release、LICENSE 与 GitHub REST API 静态整理；未下载桌面发行包，也未调用任何生成 API。

## 定位

LocalMiniDrama（本地短剧助手）是 Electron / Web 形态的 AI 短剧与漫剧工作台，从故事、角色/场景/道具、分镜、图片、视频和配音一路组织到成片。项目数据与素材目录由本机 SQLite / 文件系统管理，并提供列表与画布两种生产视图。

2026-09-16 的 GitHub 官方 JavaScript Trending 抓取显示约 `+28 stars today`；REST API 快照为 `1,676 stars / 420 forks / 28 open issues`，MIT，最新 release 与桌面/backend package 均为 `v1.2.8`，main 最近 push 为 2026-09-14。

## 用法

普通用户可从 Releases 下载桌面版；源码路径需要 Node.js `>=18`：

```sh
git clone https://github.com/xuanyustudio/LocalMiniDrama.git
cd LocalMiniDrama/backend-node
npm install
cp configs/config.example.yaml configs/config.yaml
npm start
```

随后在 AI 配置页填写文本、图片、视频与配音 provider。项目支持 DashScope、Volcengine/Seedance、Kling、Vidu、Gemini、OpenAI-compatible 和部分本地模型，具体数据流取决于所选服务。

## 原理

- 故事生成后抽取角色、场景和道具，再生成分镜文案、图片、视频与音频；实体和任务状态落在 SQLite。
- 画布与列表复用同源数据，用户可框选分镜组成 workflow 并整组重跑，也可在节点内单独编辑或重新生成。
- Node.js backend 管理异步任务、provider adapter、文件、压缩包和图像处理；Electron 将 backend 与前端打包成桌面应用。
- `v1.2.8` 增加 Agnes、Seedance 2.0 与 ModelArk 私有资产库支持，并允许配置图床上传 URL、超时和重试。
- 最终视频依赖 FFmpeg；桌面 package 会把 FFmpeg、示例项目、backend 与原生依赖一起放进发行包。

## 价值

- 不只提供 prompt，而是把长视频制作中的资产、分镜、状态、重跑和成片组织成可见工作流。
- 本地项目目录便于备份、迁移和人工修补，也减少把所有管理数据托管在单一 SaaS 的依赖。
- 多 provider adapter 允许按文本、图像、视频分别选模型，避免强绑定一家的全栈能力。
- MIT 代码和画布实现可二次开发，适合研究角色一致性、失败恢复和人机协同制作。

## 风险边界

- “数据不出本机”只适用于本地存储层；调用 DashScope、Volcengine、Kling、Gemini、Agnes、图床或 ModelArk 时，提示词、素材、角色图、视频与凭据会进入外部服务。
- 剧本、人物肖像、声音、音乐、参考图和生成视频涉及版权、肖像权、声音同意、商用条款与 AI 内容标识，MIT 只覆盖本仓库代码。
- 画布整组重跑和视频 provider 重试可能快速放大费用、排队时间和重复内容；任务状态不能代替 provider 账单对账。
- Windows 构建配置显示 `signAndEditExecutable=false`；下载发行包时应核验 release 来源、哈希、签名状态和自动更新边界。
- 自动抽取角色/场景、连续分镜和“模型越新效果越好”等描述没有统一质量 benchmark，示例视频不能证明任意剧本都保持一致性。
- 本页未安装 `v1.2.8`，没有验证 provider 兼容、离线能力、外发范围、成片质量、费用或安全性。

## 补充建议

1. 先画 provider 数据流并分 key：文本、图像、视频、配音、图床各用低额度独立凭据，禁止无提示 fallback。
2. 用自有或明确授权素材做短 fixture，记录每个节点输入、模型/version、seed、费用、输出哈希和人工验收。
3. 对整组重跑设置预算、最大次数与取消机制；provider 返回不确定时先对账，避免重复扣费。
4. 将项目库、原始素材、生成资产与最终成片分层备份，并提供一键删除外部资产与撤销公开发布的流程。

## 参考资料

- 上游 README：https://github.com/xuanyustudio/LocalMiniDrama
- AI 配置文档：https://github.com/xuanyustudio/LocalMiniDrama/blob/main/docs/configuration.md
- 快速开始：https://github.com/xuanyustudio/LocalMiniDrama/blob/main/docs/quickstart.md
- `v1.2.8` release：https://github.com/xuanyustudio/LocalMiniDrama/releases/tag/v1.2.8
- GitHub REST API：https://api.github.com/repos/xuanyustudio/LocalMiniDrama
- LICENSE：https://github.com/xuanyustudio/LocalMiniDrama/blob/main/LICENSE
