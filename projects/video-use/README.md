# video-use（browser-use/video-use）

- GitHub: https://github.com/browser-use/video-use
- 记录日期: 2026-06-28 (Asia/Shanghai)

## 定位

`video-use` 是一个让 coding agent 直接参与视频剪辑的开源工作流。它的核心不是传统 NLE 界面，而是把“转写、裁切、字幕、音频淡入淡出、动画叠加、自检输出”都交给 agent 和脚本链路来完成。

## 热度信号

1. GitHub API 在 2026-06-28 抓取时显示约 `10,486 stars`、`1,497 forks`。
2. GitHub Python 日榜在 2026-06-28 抓取时出现该项目，Trending 页面显示约 `216 stars today`。
3. 官方 README 直接写到：`Edit videos with coding agents`，并明确兼容 Claude Code、Codex、Hermes、Openclaw 等 agent。

## 用法

### 1) 克隆仓库并安装依赖

```bash
git clone https://github.com/browser-use/video-use ~/Developer/video-use
cd ~/Developer/video-use
uv sync
```

若本机没有 `uv`，README / install 文档也说明可以改用 `pip install -e .`。

### 2) 安装视频依赖

- `ffmpeg` / `ffprobe` 是硬依赖。
- 若要处理在线视频素材，可额外安装 `yt-dlp`。
- 转写依赖 ElevenLabs API key，需放到仓库根目录 `.env`。

### 3) 在素材目录里调用 agent 剪辑

把原始视频放到目标目录后，在该目录里启动 agent，然后下达类似：

```text
edit these into a launch video
```

根据官方说明，输出会落到 `edit/final.mp4`，并保留项目记忆与中间产物。

## 原理

1. 项目把视频处理拆成一串可编排步骤：转写、去口头禅、节奏裁切、字幕、调色、动画生成和渲染校验。
2. 它不是“让模型直接生成视频”，而是让 agent 驱动既有脚本、ffmpeg 和外部服务完成视频后期。
3. 这说明 agent 热点开始渗透到传统创作软件之外，用脚本化流程替代菜单式剪辑。

## 价值

- 对短视频、教程、访谈和产品演示内容，这种工作流能显著减少重复后期操作。
- 它与 `OpenMontage`、`hyperframes`、`Open-Generative-AI` 共同说明：AI 视频方向正在分化成“生成”“编辑”“自动化生产线”三条不同路线。
- 对熟悉终端与自动化的人，这类项目比重 UI 视频工具更容易嵌入持续生产流程。

## 风险边界

- 视频审美、节奏感和品牌风格仍很依赖素材质量与人工把关，不能把 agent 输出直接当最终成片。
- ElevenLabs、ffmpeg、动画引擎等外部依赖较多，环境稳定性和成本需要单独核算。
- 涉及人物肖像、字幕正确性和自动删减内容时，仍需人工复核，避免误剪和误导表达。

## 补充建议

1. 先用一小段真实素材验证转写、裁切和字幕链路，再决定是否纳入日常工作流。
2. 如果团队已有 Remotion、Premiere 或 CapCut 流程，重点比较它在批量化和可重复性上的优势，而不是只比界面体验。
3. 适合和 `OpenMontage`、`hyperframes` 一起观察，看 AI 视频工具最终会更多落在“生成”还是“后期自动化”。

## 参考资料

- https://github.com/browser-use/video-use
- https://github.com/trending/python
