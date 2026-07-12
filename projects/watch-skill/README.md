# watch-skill

<!-- markdownlint-disable MD013 -->

## 定位

`watch-skill` 是一个本地优先的视频理解与自验证层，目标是让 AI agent 能“看视频、记住证据、检查自己的工作”。它把视频、直播、会议、浏览器录屏和桌面录屏转成带时间戳的可搜索证据，并通过 MCP、CLI、REST、skills 和框架适配器开放给 agent。

截至 2026-07-13，GitHub API 显示该仓库约 171 stars、22 forks，创建于 2026-07-05，许可证为 MIT。

## 用法

Claude Code 安装：

```text
/plugin marketplace add oxbshw/watch-skill
/plugin install watch-skill@watch-skill
```

macOS / Linux 安装：

```bash
curl -fsSL https://raw.githubusercontent.com/oxbshw/watch-skill/main/scripts/install.sh | sh
```

基础命令：

```bash
watch-skill watch "https://youtu.be/..." "Summarize the important moments."
watch-skill ask <video_id> "When does the demo first fail?"
watch-skill search "pricing decision"
watch-skill serve
```

## 原理

watch-skill 将视频拆成 scene-aware frames、OCR、转写、索引和时间戳引用。对 agent 自己的浏览器或桌面会话，它强调 capture -> critique -> fix -> proof 的反馈循环，让 agent 不只生成结果，还能回看录屏并验证 UI、流程或视频输出是否符合条件。

## 价值

- 把多模态输入从“一次性总结”提升为可检索证据库。
- 对 UI 回归、浏览器流程、演示视频、会议记录和 agent 屏幕录制尤其有用。
- MCP + CLI + REST 多入口，便于接入 Claude Code、Codex 或自定义 agent。
- 与 `claude-video`、`claude-real-video`、`Browser-BC` 分工明确：它更强调可验证闭环和视频证据层。

## 风险边界

- 视频 OCR、转写和视觉问答仍可能误判，关键结论要回到时间戳人工复核。
- 录屏可能包含个人信息、客户数据、访问 token 或内部 UI，需要脱敏与保留策略。
- 视觉 Q&A 若使用外部模型，会产生视频帧或文本外传风险。
- 安装脚本依赖 ffmpeg、whisper、yt-dlp 等生态，跨平台稳定性需实测。

## 补充建议

- 优先用于“agent 做了可视化工作后必须证明结果”的场景。
- 与 Playwright 截图、trace、测试报告结合，能形成更强的 UI 验收证据。
- 持续观察 23 个 MCP tools 的权限边界和默认配置是否足够保守。

## 参考资料

- GitHub 仓库：<https://github.com/oxbshw/watch-skill>
- Trendshift 热度页：<https://trendshift.io/repositories/74186>
- 视频理解同类项目：<https://github.com/jrusso1020/video-understand-skills>
