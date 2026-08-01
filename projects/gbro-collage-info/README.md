# gbro-collage-info

## 定位

`gbro-collage-info` 是把中文口播逐字稿转为竖屏信息动画的 Agent Skill：以 HTML/CSS/GSAP 和 HyperFrames 本地渲染半调纸拼贴风 MP4，明确不调用图片生成模型。截至 2026-08-02 的 GitHub API 快照：项目创建于 2026-08-01，约 18 stars、1 fork，MIT。

## 用法

克隆到 Claude Code 等兼容工具的 skills 目录，先运行 `scripts/check_setup.sh` 检查 Node 22+、headless Chrome 与 FFmpeg/ffprobe；随后提供有权使用的逐字稿。流程按“选段与动效分配—样帧—渲染与 QA”三道确认门推进，不能把确认步骤当作可自动跳过的提示词。

## 原理

skill 从脚本中挑选适合信息表达的段落，把视觉语法、字幕安全区、镜头节奏和拟音 cue 写成规则；HyperFrames 将本地 HTML/CSS/GSAP 合成为视频。真实截图缺失时使用抽象占位，而不是伪造界面，这是其可审阅性设计的一部分。

## 价值

- 把短视频信息图做成可版本控制、可重复渲染的前端资产。
- 通过多道确认和最终 MP4 QA 降低脚本误读、字幕越界和风格漂移风险。

## 风险边界

- 文案事实、截图授权和音效/素材许可仍由使用者负责；本地渲染不自动保证可商用。
- 自动分段与动效不应替代叙事、品牌或无障碍审校。
- 依赖具体 Node、Chrome、FFmpeg 版本，跨机交付前要复渲染。

## 补充建议

先用一段无敏感事实的 30 秒脚本压测，逐门保留批准记录；发布前复核字幕、画面中的数据、素材来源和成片编码。

## 参考资料

- GitHub：<https://github.com/pyang5166/gbro-collage-info>
- 渲染依赖：<https://github.com/heygen-com/hyperframes>
- GitHub API 快照：<https://api.github.com/repos/pyang5166/gbro-collage-info>
