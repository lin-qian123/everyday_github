<!-- markdownlint-disable MD013 -->

# AutoShorts（JayWebtech/autoshorts）

> 上游仓库：<https://github.com/JayWebtech/autoshorts> · 归类：语音、视频与多模态 · 本页基于 2026-10-01 的 GitHub API、README、environment template、Tauri / package manifests 与 Release 静态整理，未安装未签名构建、处理媒体或调用云模型。

- 抓取快照：1,023 stars、195 forks、17 open issues。
- 热度信号：GitHub Rust Trending 抓取时约 +93 当日 stars。
- 版本与许可：GitHub API 为 `NOASSERTION`，根目录未见 LICENSE；latest Release / tag 为 `v0.1.5`，但 package 与 Tauri manifest 仍为 `0.1.3`。

## 定位

AutoShorts 是 Tauri 2 + React + Rust + SQLite 桌面应用，把长视频 / 音频导入、转写、AI “viral moment” 排序、竖屏裁剪与 H.264 导出串成单机工作流。它提供 Ollama + Whisper 的本地路径，也支持 Deepgram、DeepSeek、Claude 等云端服务。

## 用法

用户可从 GitHub Release 下载 macOS、Windows 或 Linux 构建，也可安装 FFmpeg 后以 `npm install`、`npm run tauri:dev` 从源码启动。首次向导选择本地或云端：本地路径会拉取 Ollama 模型并要求安装 Whisper；云端路径要求输入转写与 LLM API keys。项目与 transcript、candidate、render metadata 保存到本地 SQLite。

## 原理

FFmpeg / FFprobe 负责音频提取、画面裁剪、字幕与编码；转写结果交给本地或云模型识别候选片段、时间戳和 hook，再由桌面应用管理项目、人工选择与渲染。Tauri 只提供应用壳与 Rust 命令桥，`csp` 在当前配置中为 `null`；provider 与 credential 流程主要由应用配置决定。

## 价值

它把创作者常见的转写、寻找片段、竖屏裁剪和导出集中到可本地管理的桌面项目中，并保留完全离线的可选路线。相比只给时间戳的聊天输出，SQLite 项目与可重复 render 更方便人工复核和继续编辑。

## 风险边界

- 仓库没有可识别根许可证，不能仅凭“open-source”描述推定复制、修改或商业分发权。
- Release、package 与 Tauri 版本不一致，且默认分支最后 push 为 2026-08-02；应按具体 artifact / commit 固定。
- README 指导绕过 macOS Gatekeeper 和 Windows SmartScreen，而构建未有受信签名；不能在未审计二进制与来源时照做。
- “本地”路径仍会下载模型、Python 包和 FFmpeg 依赖；云端路径会外发音频 / transcript / prompt，并产生费用。
- “viral moment”排名、时间戳与成本是项目方主张，本轮未用金标视频、不同语言或长内容复验。
- 媒体、声音、字幕、模型输出和发布平台各有版权、肖像、隐私与内容政策；自动裁剪不等于获得再发布权。

## 补充建议

优先从固定 commit 自行构建，在隔离机器扫描依赖和 Tauri capability，并保留 Gatekeeper / SmartScreen；不要运行来源不明的 unsigned installer。先用自有授权短片测试离线模式，记录转写误差、片段召回、时间戳、裁剪和字幕，再逐个开启云 provider。API key 使用低额度测试账户，原始媒体、SQLite 和输出设置保留期与人工发布审批。

## 参考资料

- [GitHub 仓库](https://github.com/JayWebtech/autoshorts)
- [GitHub REST API](https://api.github.com/repos/JayWebtech/autoshorts)
- [README](https://github.com/JayWebtech/autoshorts/blob/main/README.md)
- [环境变量模板](https://github.com/JayWebtech/autoshorts/blob/main/.env.example)
- [Tauri 配置](https://github.com/JayWebtech/autoshorts/blob/main/src-tauri/tauri.conf.json)
- [package.json](https://github.com/JayWebtech/autoshorts/blob/main/package.json)
- [v0.1.5 Release](https://github.com/JayWebtech/autoshorts/releases/tag/v0.1.5)
