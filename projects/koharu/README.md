<!-- markdownlint-disable MD013 -->

# Koharu（koharu-rs/koharu）中文解读

> 上游仓库：<https://github.com/koharu-rs/koharu> · 归类：语音、视频与多模态 · 证据快照：2026-10-16（Asia/Shanghai）。API：6,313 stars / 450 forks / 146 open issues；README / Cargo 为 MIT OR Apache-2.0 双许可；API 单列 Apache-2.0；Release / Cargo manifest `0.83.5` / `0.83.5`。本页为上游文档与相关源码的静态整理，未安装运行、接入真实数据 / 凭据、复测性能或完成全面安全审计。

## 定位

Koharu 是 Rust 实现的漫画翻译工作台，把版面检测、OCR、翻译、去字修复、排版与人工校对整合到可编辑项目中。既能使用本地模型，也支持远端 LLM / 机器翻译 provider；它解决的是从一页图像到可审阅译稿的流程集成。

## 用法

从官方 Release 选择系统制品，也可按文档用 Homebrew / WinGet 安装。先导入一张有授权的 PNG / JPEG / WebP，创建 `.khrproj` 项目，选择检测、OCR、翻译与修复模型，运行 Current page，再逐框检查原文、译文和修复范围；最终导出 PNG 或分层 PSD。先固定 `0.83.5` 与模型文件，硬件 / 驱动要求按具体推理后端核对。

## 原理

- 检测阶段寻找文字区、气泡、面板与 mask，OCR 在区域上提取源文本，翻译阶段使用本地 GGUF 或 provider。
- Inpainting 根据 mask 移除原字并重建背景；canvas 提供人工修复、文字摆放、字体回退和竖排 / RTL 布局。
- 各阶段可按页或项目选择重跑，源 OCR 保持可编辑；只有译文被渲染，空译文不会自动以 OCR 原文替代。

## 价值

- 将“识别 → 翻译 → 清理 → 排版”的错误拆开，便于人工逐层校正，保留 PSD 也方便后续编辑。
- 本地推理为隐私与批量成本提供一种选择；可按任务替换检测、OCR、修复和翻译模型。
- 页序、项目与 selective pipeline 比一次性图片翻译更适合章节级工作。

## 风险边界

- local-first 不代表所有路径离线：hosted provider 会接收任务输入；privacy 文档还说明 Sentry 报告可能含日志、IP、URL、路径、错误内容与标识，不能假定匿名。
- 视觉模型和翻译模型有各自的权重许可与资源需求；代码双许可不自动覆盖模型、字体、漫画内容或输出传播权。
- OCR 漏字、专名 / 语气误译和 inpainting 重绘会改变作品；空译文不回退原文，可能产生看似干净的漏译。
- Release、main 文档和 tag 排序不能混用；本次 tags API 首项为旧 `v0.1.1`，而最新 Release 与 manifest 为 `0.83.5`。

## 补充建议

- 用 5 页授权样本建立逐框金标，分别统计检测漏检、OCR 错字、翻译修订和原画误改。
- 先用完全本地模型配合出口观察验证实际数据流，再评估 hosted provider 与诊断上报是否符合素材要求。
- 保留原图、mask、文本层、模型 hash 和字体来源；人工终审后再导出，不以流水线成功状态当译稿验收。

## 参考资料

- 上游仓库：<https://github.com/koharu-rs/koharu>
- GitHub REST API：<https://api.github.com/repos/koharu-rs/koharu>
- README：<https://github.com/koharu-rs/koharu/blob/main/README.md>
- 首张页面流程：<https://github.com/koharu-rs/koharu/blob/main/packages/docs/quickstart.mdx>
- 诊断隐私说明：<https://github.com/koharu-rs/koharu/blob/main/packages/docs/privacy.mdx>
- Cargo manifest：<https://github.com/koharu-rs/koharu/blob/main/Cargo.toml>
- MIT 文本：<https://github.com/koharu-rs/koharu/blob/main/LICENSE-MIT>
- Apache 文本：<https://github.com/koharu-rs/koharu/blob/main/LICENSE-APACHE>
- Releases：<https://github.com/koharu-rs/koharu/releases>
