# FableCut

<!-- markdownlint-disable MD013 MD012 -->

## 定位

`FableCut` 是一个浏览器中的非线性视频编辑器，同时把完整时间线暴露为 JSON、REST 和 MCP 工具。它的核心想法是：视频剪辑项目本身就是 agent 接口，Claude Code、Claude Desktop 或其他 MCP/REST agent 可以直接修改 `project.json`，浏览器 UI 实时热重载。

截至 2026-07-10 抓取时，GitHub 仓库约 `218` stars、`7` forks，主语言为 JavaScript，许可证为 MIT。

## 用法

- 克隆仓库后运行 `node server.js`，在 `http://localhost:7777` 打开编辑器。
- 用户可在 UI 中拖拽素材、剪切、调整滤镜、字幕、keyframe、transition 和导出。
- agent 可通过 MCP 工具读取文档、获取项目、patch 时间线、导入媒体、分析 reference video。
- 也可直接修改 `project.json` 并增加 revision，UI 通过 SSE 在约百毫秒级刷新。

## 原理

项目用零 npm 依赖的 Node server 提供静态页面、REST API、SSE、ffmpeg 导出管线和 MCP server。前端编辑器维护视频/音频 track、clip、effect、transition、keyframe、caption 和 SVG overlay。并发编辑通过 revision counter 检测冲突，避免 agent 覆盖用户未保存修改。

## 价值

- 把 AI 视频从“黑盒生成 API”拉回可检查、可编辑、可回滚的时间线。
- 对短视频改编、reference remake、字幕包装、素材粗剪和社媒内容生产很实用。
- MCP 文档和 patch 操作让 agent 只传增量，而不是反复读写巨大的项目文件。
- 人和 agent 可以共用同一个 UI，适合边看边调而不是等待离线生成。

## 风险边界

- 浏览器端视频合成和 ffmpeg 导出对大素材、长视频和复杂特效的稳定性需实测。
- MediaPipe 背景移除会首次从 CDN 拉模型，离线/企业环境要提前处理依赖。
- agent 修改时间线需要明确素材版权、音乐授权和 reference video 使用边界。
- 零依赖降低安装门槛，但也意味着很多编辑能力由项目自研，成熟度需按实际场景验证。

## 补充建议

- 与 `video-use`、`OpenMontage`、`hyperframes`、`motion-anything` 横向比较，判断视频 agent 工作流会落在剪辑时间线、生成合成还是 HTML 渲染。
- 对团队生产，建议为 `project.json` 建 schema 校验、自动截图预览和导出 smoke test。
- 把 reference analysis 的 blueprint、BPM、cut list 和输出 MP4 一起归档，便于复盘。

## 参考资料

- GitHub 仓库：<https://github.com/ronak-create/FableCut>
- MCP 说明：<https://github.com/ronak-create/FableCut/blob/main/CLAUDE.md>
