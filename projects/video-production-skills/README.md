# video-production-skills

<!-- markdownlint-disable MD013 -->

## 定位

`video-production-skills` 是 Pluviobyte 维护的 AI 视频制作 skill 集合，面向 Codex、Claude Code、Cursor 等能读取本地 skill 的编程/创作代理。它不是一个单一视频编辑器，而是把“动效导演、参考视频复刻、SaaS 产品短片、黑底白字片头”等高频视频制作环节拆成可安装的独立 skill。

截至 2026-07-11，GitHub API 显示该仓库约 531 stars，创建于 2026-06-26，近期仍在更新。它的热度来自两个背景：一是 `hyperframes`、`FableCut`、`motion-anything` 等项目把视频时间线逐渐暴露给 agent；二是内容创作者希望把“像 PPT 的静态生成”升级为可验证的运动语言。

## 用法

仓库推荐通过 Skills CLI 安装：

```bash
npx skills add https://github.com/Pluviobyte/video-production-skills --list
npx skills add https://github.com/Pluviobyte/video-production-skills --skill ai-motion-director
npx skills add https://github.com/Pluviobyte/video-production-skills --skill reference-video-replica-qc
```

目前比较明确的入口包括：

- `ai-motion-director`：先定义 motion thesis、beat graph、组件调度和反 PPT 质检标准。
- `reference-video-replica-qc`：对参考视频做抽帧、复刻、对照、返修和组件沉淀。
- `dark-saas-magic-video`：做暗色 SaaS / AI 产品短片。
- `black-white-text-opener`：生成黑底白字逐字打字开场。

## 原理

项目的核心思路是把视频制作拆成“导演层 + 执行层 + 验收层”。导演层先决定节奏、镜头隐喻、运动组件和素材需求；执行层交给 HyperFrames、Remotion、React、CSS、SVG、GSAP 或图像/音频生成工具；验收层用抽帧、contact sheet、局部 crop、PSNR/SSIM/哈希等证据判断是否接近参考目标。

这种方式比单纯让模型“生成一个视频”更工程化：每次复刻都应沉淀可复用组件，记录适用场景、输入参数、时间线、技术栈和对齐限制。

## 价值

- 把视频创作从一次性 prompt 产物变成可复用的 skill 库。
- 对 agent 友好，能让 Codex / Claude Code 直接理解视频制作流程。
- 强调 motion-first，避免 AI 视频只生成静态卡片和幻灯片。
- 对参考视频复刻给出可审计验证路径，适合构建团队内部视频组件库。

## 风险边界

- 仓库未在 GitHub API 中识别到标准许可证，商业复用前应确认授权。
- skill 本身不等于渲染引擎；仍需要本地有 HyperFrames、Remotion、ffmpeg 或相关工具链。
- “像素级复刻”需要硬指标证明，普通手写复刻更适合作为视觉级对齐和组件沉淀。
- 参考视频复刻可能涉及版权、品牌和素材授权，不能默认用于公开商业发布。

## 补充建议

- 与 `FableCut`、`hyperframes`、`motion-anything` 一起观察，看 AI 视频工作流是否会收敛为“skill 规划 + timeline JSON + 可视化编辑器”。
- 对团队场景，应把每次复刻后的组件、失败窗口和修复日志长期归档，而不是只保留成片。
- 如果用于产品发布短片，建议引入人工品牌审查和素材授权清单。

## 参考资料

- GitHub 仓库：<https://github.com/Pluviobyte/video-production-skills>
- `ai-motion-director` 文档：<https://github.com/Pluviobyte/video-production-skills/blob/main/docs/ai-motion-director.md>
- `reference-video-replica-qc` 文档：<https://github.com/Pluviobyte/video-production-skills/blob/main/docs/reference-video-replica-qc.md>
- HyperFrames：<https://github.com/heygen-com/hyperframes>
- FableCut：<https://github.com/ronak-create/FableCut>
