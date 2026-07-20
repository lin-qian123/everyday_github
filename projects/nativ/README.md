<!-- markdownlint-disable MD013 -->

# nativ

## 定位

`nativ` 是面向 Apple Silicon Mac 的本地 AI 工作台，用 SwiftUI 封装 MLX / `mlx-vlm` 模型服务，提供聊天、模型管理、性能监控、本地 API server 和 coding tool 集成。它代表的是“本地推理底座 + 桌面工作台 + OpenAI/Anthropic-compatible API”的路线。

## 今日信号

- GitHub：<https://github.com/Blaizzy/nativ>
- 项目页：<https://blaizzy.github.io/nativ/>
- 创建时间：2026-07-20。
- 抓取时约 146 stars、9 forks。
- 语言 / 许可证：Swift，MIT。

## 用法

用户可以下载 DMG 或从源码构建。应用会发现 Hugging Face cache 中的兼容 MLX 模型，也可下载模型；选择模型后，可以在桌面端聊天、查看 token / latency / decode speed 等指标，或通过本地 `localhost` endpoint 让 Codex、Claude Code、Pi、Hermes、OpenCode 等工具调用本机模型。

## 原理

Nativ 的 SwiftUI shell 通过 `NativServerKit` 管理嵌入式 Python runtime 与 bundled `mlx-vlm` server。模型运行在 Apple unified memory 上，应用层负责模型发现、配置、日志、analytics、menu bar 控制和 API 兼容层。

## 价值

- 将本地 MLX 模型从命令行 runner 包装成可持续使用的 macOS 工作台。
- 对 coding agent 使用者有现实意义：本地模型可作为低成本、私有、可离线的补充后端。
- 同时提供 OpenAI-compatible 和 Anthropic Messages 风格接口，降低接入现有工具的摩擦。

## 风险边界

- 运行要求较新：Apple Silicon、macOS 26+，源码构建还依赖 Xcode、Python、网络下载依赖。
- 本地模型能力受模型大小、显存/统一内存、量化和 MLX 支持范围限制，不能等同于云端前沿模型。
- 本地 API 若开启管理能力，需要正确设置 API key 和监听地址，避免内网暴露。

## 补充建议

- 后续重点观察 release 稳定性、模型兼容列表、API 兼容程度和 Codex / Claude Code 集成是否真正减少配置成本。
- 可与 `Rapid-MLX`、`ollama`、`LocalAI`、`text-generation-webui` 做横向对照：Nativ 更偏 macOS 原生体验，Ollama 更偏通用模型拉取和服务。

## 参考资料

- GitHub 仓库：<https://github.com/Blaizzy/nativ>
- 项目页：<https://blaizzy.github.io/nativ/>
- README：<https://github.com/Blaizzy/nativ#readme>
- MLX：<https://github.com/ml-explore/mlx>
- mlx-vlm：<https://github.com/Blaizzy/mlx-vlm>
