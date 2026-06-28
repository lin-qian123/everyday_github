# FluidVoice（altic-dev/FluidVoice）

- GitHub: https://github.com/altic-dev/FluidVoice
- 记录日期: 2026-06-29 (Asia/Shanghai)

## 定位

`FluidVoice` 是一个面向 macOS 的开源离线语音转文字应用，强调本地运行、低延迟听写和设备端 AI 后处理。它的代表性在于把语音输入从云端订阅服务拉回本地桌面工作流。

## 热度信号

1. GitHub API 在 2026-06-29 抓取时显示约 `3,688 stars`、`236 forks`。
2. GitHub 全站日榜在 2026-06-29 抓取时出现该项目。
3. 官方 README 明确写到 `Open source voice-to-text dictation app for macOS with on-device AI enhancement`，并提供 Homebrew cask 安装方式。

## 用法

### 1) Homebrew 安装

```bash
brew install --cask fluidvoice
```

也可以从 GitHub Releases 下载最新版本。

### 2) 选择语音引擎

README 中列出 Nemotron Speech、Parakeet、Cohere、Apple Speech、Whisper 等支持路径。用户需要根据语言、延迟、隐私和硬件性能选择合适模型。

### 3) 本地 AI 增强

`Fluid Intelligence` 负责本地后处理，包括格式化、大小写和上下文相关润色。README 同时说明该运行时目前是单独维护的私有组件，因此开源边界需要单独注意。

## 原理

1. 应用把录音、转写、文本后处理和系统输入串成 macOS 原生听写体验。
2. 本地语音模型负责主要识别，后处理模型负责把原始转写变成更可用的文本。
3. 相比云端听写，它把隐私、延迟和成本控制放在本机，但也把性能压力转移到用户设备。

## 价值

- 对重度写作者、开发者和研究人员，本地听写可以成为低摩擦输入方式。
- 对隐私敏感场景，离线语音转文字比云端服务更容易解释数据边界。
- 对开源 AI 应用生态，它说明语音方向的热点不仅是 TTS / 角色语音，也包括“日常输入层”。

## 风险边界

- 高质量低延迟转写依赖硬件、模型和语言适配，不能默认所有语言都同样好用。
- GPLv3 许可和私有 `Fluid Intelligence` 组件的边界需要在二次分发时看清。
- 听写文本进入其他应用后仍可能泄露敏感信息，本地转写不等于全链路无风险。

## 补充建议

1. 先测试自己的常用语言、专业词汇和噪声环境，再决定是否替换现有听写工具。
2. 若用于工作资料输入，明确录音缓存、模型缓存和日志位置。
3. 与 `voicebox`、`fish-speech`、`MOSS-TTS` 区分：它更偏输入层，而不是生成语音内容。

## 参考资料

- https://github.com/altic-dev/FluidVoice
- https://github.com/trending
