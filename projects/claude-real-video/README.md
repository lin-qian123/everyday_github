# claude-real-video

<!-- markdownlint-disable MD013 MD012 -->

## 定位

`claude-real-video` 是一个本地视频 keyframe、转写和 LLM 输入整理工具，目标是让 Claude、ChatGPT、Gemini 或其他 LLM 通过关键帧、contact sheet、transcript 和 manifest 真正“看见”视频。它尤其适合分析 YouTube、Instagram Reels、TikTok、本地 MP4、课程录屏和快剪视频。

截至 2026-07-10 抓取时，GitHub 仓库约 `1449` stars、`104` forks，主语言为 Python，许可证为 MIT，并在 README 中标注曾上 Hacker News front page。

## 用法

- 安装核心包：`pip install claude-real-video`；需要转写时安装 `pip install "claude-real-video[whisper]"`。
- 系统需提供 `ffmpeg`/`ffprobe`；URL 输入依赖 `yt-dlp`。
- 基本命令：`crv "https://www.youtube.com/watch?v=..."`，输出 `frames/`、`transcript.txt` 和 `MANIFEST.txt`。
- 可用 `--grid` 生成 contact sheet、`--viewer` 生成本地查看器、`--why` 指定分析目的、`--kb` 保存到个人知识库。

## 原理

项目不按固定 FPS 盲采样，而是用场景变化检测加密度下限提取关键帧，再用滑动窗口去重，减少静态录屏或重复镜头浪费。音频部分可用 Whisper 转写；字幕存在时优先利用字幕。最终产物是 LLM 可直接读取的图片序列、转写文本和 manifest。

## 价值

- 把“视频理解”拆成可审计的本地预处理流程，用户可以先看模型将看到什么。
- 对快剪、教程、产品 demo、会议片段和社媒视频，比只读 transcript 更可靠。
- 对不支持视频文件的 LLM 客户端提供通用桥接层。
- 可作为更大 agent skill 的视频输入前处理，例如竞争分析、UI demo 复盘、课程摘要。

## 风险边界

- 关键帧抽取不是完整视频理解，动作连续性、语气、音效和细微表情仍可能丢失。
- URL 抓取受平台登录、地区、版权和 cookie 限制影响。
- Whisper 转写质量取决于音频、语言和模型配置。
- 把输出帧上传给第三方 LLM 前仍需自行处理隐私和版权边界。

## 补充建议

- 与 `claude-video` 区分：`claude-video` 更像 Claude/Codex 的 `/watch` skill，`claude-real-video` 更像通用本地 keyframe extractor + viewer。
- 用 `--report` 调整场景阈值，避免 fast-cut 视频漏帧或静态视频过采样。
- 对企业素材，建议固定输出目录、保留 manifest 和 frame list，便于审计模型输入。

## 参考资料

- GitHub 仓库：<https://github.com/HUANGCHIHHUNGLeo/claude-real-video>
- PyPI：<https://pypi.org/project/claude-real-video/>
- Hacker News 条目：<https://news.ycombinator.com/item?id=48766005>
