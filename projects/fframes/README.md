<!-- markdownlint-disable MD013 -->

# fframes（dmtrKovalenko/fframes）

> 上游仓库：<https://github.com/dmtrKovalenko/fframes> · 归类：语音、视频与多模态 · 本页基于 2026-10-01 的 GitHub API、README、Cargo manifests、benchmark 目录、Release 与 LICENSE 静态整理，未安装 Rust / codec 依赖、渲染样例或复跑速度比较。

- 抓取快照：1,549 stars、29 forks、5 open issues。
- 热度信号：GitHub Rust Trending 抓取时约 +722 当日 stars。
- 版本与许可：MIT；latest Release 与 tag 均为 `v1.1.0`。

## 定位

fframes 是用 Rust、SVG tree、Skia / Vulkan / Metal 与 FFmpeg 构建的程序化视频框架，并为 coding agent 提供专用 skill。它把 timeline、frame render、音频分析、contact sheet、onion skin、snapshot diff、preview 与最终编码纳入同一项目，使不能直接“观看”视频的 Agent 也能读取结构化 QA 证据。

## 用法

可用 `cargo install --locked cargo-fframes` 创建项目，进入目录后通过 `cargo run --release -- preview` 或 `render` 操作；Agent 路径可从官网安装 fframes skill，再按自然语言生成项目。开发和不同系统需要 Rust、Node、FFmpeg / codec、LLVM / libclang 等依赖，Windows 还需配置共享 FFmpeg 路径。

## 原理

视频是实现 `Video` trait 的 Rust 程序，每帧由 `svgr!` 生成 SVG tree；静态标记编译期缓存，Skia GPU 或 CPU backend 绘制，再通过 libav 编码。`inspect` 检查缺字体、裁切、无效 SVG 和 panic，`strip` / `onion` / `frame` 输出视觉证据，`audio analyze` 给出 LUFS、true peak、clipping 和 silence。

## 价值

显式代码与确定性 frame / audio 工具把视频生成从黑盒 prompt 变成可 diff、可回归、可逐帧定位的工程资产。对批量模板、技术演示和 Agent 生成，contact sheet、snapshot 与 JSON 输出能在最终人工观看前发现一部分布局、字体和音频错误。

## 风险边界

- “约 10× GPU”“48 分钟制作、36 秒渲染”等是上游特定样例 / 环境主张，本轮未复跑，不能跨硬件与 codec 泛化。
- 静态 inspect、contact sheet 和音频数值不能替代完整观看；节奏、叙事、闪烁、无障碍和品牌正确性仍需人审。
- Agent skill 会安装工具、写代码、下载 / 编译大型 native 依赖并执行 render；应在资源受限的项目副本中运行。
- FFmpeg、x264 / x265、VPX、Opus、字体、音乐、图片与 shader 各有许可证 / 专利 /素材权利，MIT 只覆盖仓库代码。
- native cache 若跨 CPU 恢复可能触发 `SIGILL`；GPU / codec / Windows shared DLL 组合也需按目标环境验收。
- 生成视频可能含素材侵权、事实错误、危险闪烁或不当内容，结构化 QA 不覆盖内容政策。

## 补充建议

固定 `v1.1.0`、Rust toolchain、feature 与 codec 清单，在小样例分别记录 CPU / GPU render 时间、峰值内存、输出 hash 与播放兼容。CI 先跑 timeline、inspect、snapshot 和音频阈值，最终制品仍进行逐帧抽样、全片带声观看、字幕 / 无障碍和版权清单审查。Agent 安装 skill 前先读内容并限制 shell、网络、媒体目录与构建缓存。

## 参考资料

- [GitHub 仓库](https://github.com/dmtrKovalenko/fframes)
- [GitHub REST API](https://api.github.com/repos/dmtrKovalenko/fframes)
- [README](https://github.com/dmtrKovalenko/fframes/blob/main/README.md)
- [Agent Skill](https://github.com/dmtrKovalenko/fframes/blob/main/skills/fframes-video/SKILL.md)
- [Render benchmark 目录](https://github.com/dmtrKovalenko/fframes/tree/main/render-bench)
- [v1.1.0 Release](https://github.com/dmtrKovalenko/fframes/releases/tag/v1.1.0)
- [LICENSE](https://github.com/dmtrKovalenko/fframes/blob/main/LICENSE.txt)
