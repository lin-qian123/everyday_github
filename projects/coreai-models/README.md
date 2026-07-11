# coreai-models

<!-- markdownlint-disable MD013 -->

## 定位

`coreai-models` 是 Apple 发布的 Core AI 模型导出、Python primitives 与 Swift runtime utilities 仓库，用于把开放模型导出为 Core AI 格式，并在 macOS / iOS 应用中运行。它还包含帮助 coding agents 使用 Core AI 的 skills。

截至 2026-07-12，GitHub API 显示该仓库约 1367 stars、116 forks，创建于 2026-06-08，许可证为 BSD-3-Clause。README 将主要目录分成 `models/`、`python/`、`swift/`、`skills/`。

## 用法

安装 `uv`：

```bash
brew install uv
```

克隆仓库并查看模型导出 recipe：

```bash
git clone https://github.com/apple/coreai-models.git
cd coreai-models
```

不同模型族在 `models/` 下有独立 README。运行和集成要求 macOS / iOS 27.0+ 与 Xcode 27.0+。

## 原理

Core AI 模型被导出为 `.aimodel` 文件。语言模型需要 tokenizer，扩散模型可能由多个模型和资源组成，因此导出 recipe 会生成模型文件与资源目录。Swift package 提供 app 集成所需的 runtime utilities，Python 侧提供导出和自定义模型 primitives。

## 价值

- 代表 Apple 端侧 AI 工具链开始公开化、工程化。
- 对希望把开放模型落到 iOS / macOS app 的开发者，比纯论文或 demo 更直接。
- `skills/` 目录说明厂商也在把 coding agent 纳入模型部署工作流。
- 与 `Rapid-MLX`、`local-llm` 共同构成 Apple Silicon / Apple 平台本地 AI 路线。

## 风险边界

- 依赖 macOS / iOS 27.0+ 与 Xcode 27.0+，当前可用人群受平台版本限制。
- 导出成功不等于模型在移动端性能、内存和延迟满足产品要求。
- Core AI 格式和 API 仍可能随 Apple 平台演进变化。
- 使用第三方开放模型时仍需遵守原模型许可证和再分发限制。

## 补充建议

- 对移动端 AI app，优先用小模型验证端侧延迟、内存和能耗，再考虑复杂多模型 pipeline。
- 观察 `skills/` 是否会形成 Apple 官方 agent 部署 skill 模板。
- 与 MLX 路线对比：MLX 偏研究 / 本地推理，Core AI 更偏应用集成与系统框架。

## 参考资料

- GitHub 仓库：<https://github.com/apple/coreai-models>
- Core AI 文档：<https://developer.apple.com/documentation/coreai>
- Apple Developer：<https://developer.apple.com/>
