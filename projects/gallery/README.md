<!-- markdownlint-disable MD013 -->

# Google AI Edge Gallery（google-ai-edge/gallery）

> 上游仓库：<https://github.com/google-ai-edge/gallery> · 归类：模型、训练与推理基础设施 · 本页基于 2026-10-03 的 GitHub API、README、development / function-calling / skills 文档、model allowlist、Release 与 LICENSE 静态整理，未在 Android、iOS 或 macOS 下载模型、运行 benchmark、相机 / 音频任务或设备 action。

- 抓取快照：24,825 stars、2,707 forks、391 open issues。
- 热度信号：GitHub Kotlin Trending 抓取时约 +4 当日 stars。
- 版本与许可：代码 Apache-2.0；latest Release / tag 为 `1.0.19`，README 标注 experimental Beta，并已同时提供 Android、iOS 与 macOS 入口。

## 定位

Google AI Edge Gallery 是用于在个人设备上试用和评估本地生成式 AI 的多端应用。它覆盖 LLM chat、thinking mode、图像问答、语音转写 / 翻译、Prompt Lab、模型管理与 benchmark，并加入 Agent Skills、Mobile Actions 和 FunctionGemma 驱动的实验任务。

## 用法

Android 12+、iOS 17+ 可从商店安装，Android 也能从 Release 下载 APK，macOS 提供独立 DMG。用户从 allowlist / Hugging Face 下载 LiteRT-compatible 模型或加载自有模型，在设备上选择任务与参数；开发者可修改 Kotlin tool definition 与 action handler，构建自定义 function-calling 行为。

## 原理

应用以 Google AI Edge / LiteRT runtime 在本地执行量化模型，通过模型 allowlist 描述 artifact、大小、估计峰值内存、加速器和任务能力。Chat / Prompt Lab 管理推理参数，多模态任务连接相机、图片和音频；Mobile Actions 把模型生成的 function call 映射到 Android action callback，Agent Skills 则为模型附加 Wikipedia、地图和富卡片等工具能力。

## 价值

它把模型下载、设备适配、任务演示和本机 benchmark 放到同一可视界面，适合快速判断某个量化模型在真实手机上的内存、延迟与能力，而不仅看服务器 benchmark。源码还提供了 function-calling 与 skill 示例，便于理解端侧模型如何接入受控应用动作。

## 风险边界

- README 的“100% on-device privacy”只适用于模型 inference；模型下载、Hugging Face、商店分发、URL skill、Wikipedia / 地图等网络工具仍会产生网络与第三方数据流。
- repo 的 Apache-2.0 只覆盖代码；Gemma、Qwen 及社区转换 artifact 分别有模型 license、使用条款与来源，不能据根许可证统一推断。
- allowlist 的内存估计、加速器和 benchmark 只对特定 artifact / runtime / 设备有意义；本轮未在任何手机上复测速度、能耗、热降频或准确率。
- experimental Beta、391 个 open issues 与多平台差异意味着功能、模型支持和 UI 可能变化；Android 功能不自动等于 iOS / macOS 等价。
- Mobile Actions 和 URL / community skills 会把模型输出连接到设备能力或外部内容；端侧推理不能消除 prompt injection、错误 tool call 和权限过宽。
- thinking mode 展示的是模型输出过程，不是可验证的真实因果解释；视觉、转写和翻译结果仍需任务级金标。

## 补充建议

按设备、OS、app Release、runtime 和模型 revision 建立可复现矩阵，先断网运行不含 skill / action 的公开低风险 prompt，再逐项开启相机、音频、URL skill 和 device action。记录 artifact hash、模型许可、下载来源、峰值内存、首 token、吞吐、能耗和错误案例；对 function call 设置显式 allowlist、参数校验、用户确认和可撤销结果。

## 参考资料

- [GitHub 仓库](https://github.com/google-ai-edge/gallery)
- [GitHub REST API](https://api.github.com/repos/google-ai-edge/gallery)
- [README 与安装入口](https://github.com/google-ai-edge/gallery/blob/main/README.md)
- [Model allowlist](https://github.com/google-ai-edge/gallery/blob/main/model_allowlist.json)
- [Function Calling Guide](https://github.com/google-ai-edge/gallery/blob/main/Function_Calling_Guide.md)
- [Agent Skills 说明](https://github.com/google-ai-edge/gallery/blob/main/skills/README.md)
- [1.0.19 Release](https://github.com/google-ai-edge/gallery/releases/tag/1.0.19)
- [LICENSE](https://github.com/google-ai-edge/gallery/blob/main/LICENSE)
