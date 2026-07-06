<!-- markdownlint-disable MD013 -->

# claude-video

## 定位

`claude-video` 是一个把视频理解能力封装成 agent skill / Claude Code plugin 的项目。它提供 `/watch` 命令，让 Claude 或其他支持 Agent Skills 的工具读取 YouTube、Loom、TikTok、X、Instagram、本地视频等来源，抽取字幕、音频转写和关键帧，再基于真实画面与语音回答问题。

它的价值不在于训练新模型，而是把现有 `yt-dlp`、`ffmpeg`、caption、Whisper 和 agent 图片读取能力串成一个可复用技能。

## 用法

Claude Code 安装：

```bash
/plugin marketplace add bradautomates/claude-video
/plugin install watch@claude-video
```

Codex、Cursor、Copilot、Gemini CLI 等支持 Agent Skills 的宿主可用：

```bash
npx skills add bradautomates/claude-video -g
```

典型调用：

```text
/watch https://youtu.be/<video-id> summarize this
/watch bug-repro.mov when does the UI break?
/watch https://youtu.be/<video-id> --start 2:15 --end 2:45
```

## 原理

`/watch` 的流程大致是：

1. 用 `yt-dlp` 优先抓取字幕，能不用下载完整视频时就不下载。
2. 用 `ffmpeg` 按 detail 模式抽取关键帧或场景变化帧。
3. 对无字幕视频抽取音频并调用 Groq 或 OpenAI Whisper 转写。
4. 对相近帧做去重，控制图像 token 成本。
5. 把带时间戳的 transcript 和帧路径交给 agent 读取。

它提供 `transcript`、`efficient`、`balanced`、`token-burner` 等模式，在速度、画面覆盖和 token 成本之间做取舍。

## 价值

- **视频变成 agent 输入**：适合分析发布会、课程、竞品演示、bug 录屏和社媒视频。
- **工程化成本控制**：通过字幕优先、关键帧、场景检测和去重降低上下文消耗。
- **跨宿主技能**：不只面向 Claude Code，也可通过 Agent Skills CLI 安装到 Codex、Cursor、Copilot、Gemini CLI 等环境。
- **可复用脚本结构**：把下载、抽帧、转写、配置、清理拆成独立脚本，便于审计和扩展。

## 风险边界

- 视频平台下载、字幕和登录限制会影响成功率，部分 X / Instagram / TikTok 内容可能不可稳定访问。
- 长视频在 capped detail 下会稀疏采样，不能保证看到每个关键画面。
- Whisper fallback 需要 API key，会产生额外成本和隐私外发。
- 对版权视频和私密会议录屏应先确认授权与数据处理边界。

## 补充建议

- 处理 bug 录屏时优先指定时间窗口，减少 token 成本并提高帧密度。
- 对课程或长会议先用 transcript 模式做结构化摘要，再对关键片段二次抽帧。
- 与 `meetily` 区分：`claude-video` 偏离线/事后视频理解技能，`meetily` 偏实时会议记录与本地转写工作台。

## 参考资料

- GitHub 仓库：<https://github.com/bradautomates/claude-video>
- Agent Skills：<https://agentskills.io>
- GitHub Trending：<https://github.com/trending>
