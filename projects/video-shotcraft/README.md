<!-- markdownlint-disable MD013 -->

# video-shotcraft

## 定位

`video-shotcraft` 是面向 Claude Code / Codex 的 AI 视频制作 skill，用 Remotion、shot recipe cards、motion previews 和完整模板，把 coding agent 变成产品 promo / launch / demo 视频的动效制作助手。

## 今日信号

- GitHub：<https://github.com/Vincentwei1021/video-shotcraft>
- Gallery：<https://vincentwei1021.github.io/video-shotcraft/>
- 创建时间：2026-07-19。
- 抓取时约 41 stars、4 forks。
- 语言 / 许可证：TypeScript，Apache-2.0。
- Topics：`agent-skills`、`ai-video`、`claude-code`、`codex`、`remotion`、`video-production`。

## 用法

用户可以让 Claude Code / Codex 安装该 skill，也可通过 `npx skills add Vincentwei1021/video-shotcraft` 或手工 symlink 到 `~/.claude/skills/`、`~/.codex/skills/`。之后通过自然语言指定产品、素材和 shot card，agent 按照 pipeline 生成 Remotion 动画、捕获页面、设计镜头、做 beat sync 和最终 QA。

## 原理

项目把视频制作拆成可检索的 shot cards、sequence patterns、aesthetic rules、sound design、music beat sync 和 Remotion demos。agent 不从零猜测动效，而是选择已有镜头语言、参数、时长和已知坑位，再用 TSX / Remotion 生成可渲染视频。

## 价值

- 将 AI 视频热点从“模型生成片段”转向“agent 可操作的可编辑视频工程”。
- 对 SaaS、桌面软件、开发工具的产品演示很实用，因为它能用真实页面截图和代码化动效做可复审交付。
- 体现 `video-use`、`FableCut`、`hyperframes` 之后的另一条路径：把视频制作知识沉淀成 skill 和 recipe 库。

## 风险边界

- 最终质量依赖素材、截图、品牌约束和 agent 对 Remotion 的实现能力。
- 生成的是代码化视频工作流，不等同于 Sora / Veo 这类端到端视频模型。
- 使用内置模板时要避免所有产品都长成同一种“AI promo”风格。

## 补充建议

- 后续观察是否补充更多完整模板、真实客户案例和自动化渲染验证。
- 可和 `FableCut`、`video-use`、`hyperframes`、`motion-anything` 一起归入 agent-native 视频生产链路。
- 用于正式营销前，仍需人工做版权、品牌一致性和字幕校对。

## 参考资料

- GitHub 仓库：<https://github.com/Vincentwei1021/video-shotcraft>
- Gallery：<https://vincentwei1021.github.io/video-shotcraft/>
- README：<https://github.com/Vincentwei1021/video-shotcraft#readme>
- Remotion：<https://www.remotion.dev/>
