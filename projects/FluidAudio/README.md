<!-- markdownlint-disable MD013 -->

# FluidAudio

- 主上游：[FluidInference/FluidAudio](https://github.com/FluidInference/FluidAudio)
- 分类：语音、视频与多模态。
- 核验日期：2026-10-23（Asia/Shanghai）；主线快照 `c79c4106b954`。
- [API](https://api.github.com/repos/FluidInference/FluidAudio) 快照：3,165 stars / 485 forks / 29 open issues；发行列表首项 [v0.17.7](https://github.com/FluidInference/FluidAudio/releases/tag/v0.17.7)（UTC 2026-10-08，正式）。累计值不代表今日增量。

## 定位

FluidAudio 是面向 Apple 设备的 Swift / CoreML 音频 SDK，提供 ASR 转写、流式语音、TTS、VAD、说话人分离等模型管线。它是应用组件，不是完整会议软件；不同语言、低延迟与音质目标需选择不同模型。[README](https://github.com/FluidInference/FluidAudio/blob/c79c4106b954f81205113c3343e5a7e59a1089b5/README.md)

## 用法

通过 Swift Package Manager 添加包，再向 target 添加 `FluidAudio` product。本轮正式发行首项为 v0.17.7；建议锁定版本与模型 revision。主线基础 manifest 使用 Swift tools 6.0，声明 macOS 14 / iOS 17 等平台下限；个别模型要求更高系统，不能仅看包下限。

先以授权短音频完成一次离线转写，再测流式和分说话人。Swift 6.2+ 另有 traits，可关闭 TTS、Diarizer、NeMo 子系统；三者默认都开启。`traits: []` 在当前主线关闭三者，旧版语义曾不同。[基础 manifest](https://github.com/FluidInference/FluidAudio/blob/c79c4106b954f81205113c3343e5a7e59a1089b5/Package.swift)、[6.2 manifest](https://github.com/FluidInference/FluidAudio/blob/c79c4106b954f81205113c3343e5a7e59a1089b5/Package@swift-6.2.swift)

## 原理

将语音模型转换 / 优化为 CoreML 管线，利用 Apple Neural Engine 等计算路径完成本地推理；批量滑窗转写和真实流式模型的缓存、拼接与时延条件不同。VAD、ASR、speaker embedding / clustering 和 TTS 可组合，但“分离说话人编号”本身不能证明识别了真实人物身份。[模型目录](https://github.com/FluidInference/FluidAudio/blob/c79c4106b954f81205113c3343e5a7e59a1089b5/Documentation/Models.md)

## 价值

适合在 macOS / iOS 产品中减少音频上云依赖，或构建可控的低延迟语音界面。具体优势应以目标设备、语言、口音、噪声、能耗与内存测试判断；不引用作者性能数字作为本轮复现结果。

## 风险边界

- 默认可从 Hugging Face 下载模型。“本地推理”不等于首次运行或缓存损坏恢复时不联网。主线提供 `ModelHub.offlineMode = true`，需在 loader 启动前设置，并准备完整本地模型；缺文件 / 损坏时应验证明确报错而非重下。[下载实现](https://github.com/FluidInference/FluidAudio/blob/c79c4106b954f81205113c3343e5a7e59a1089b5/Sources/FluidAudio/Shared/Download/ModelHub.swift)
- README 安装片段仍有 0.12.4，而 traits 示例已用 0.17.7；当前文档 / 主线能力未必全部包含在旧 tag 中。
- Parakeet 不代表支持所有语言；模型目录另列中文模型和不同流式能力。TTS 声音授权、录音同意、模型权重与转换组件许可需分别核对，SDK 的 Apache-2.0 不替代这些条款。[SDK 许可](https://github.com/FluidInference/FluidAudio/blob/c79c4106b954f81205113c3343e5a7e59a1089b5/LICENSE)
- README 应用演示是集成线索，不是独立准确率或性能评测；宿主应用也可能另有遥测、同步与云模型调用。

## 补充建议

用中文与目标语言分别统计 WER / CER、首字延迟、峰值内存和持续能耗；分说话人另评 DER 与重叠语音。用断网、缺模型和坏缓存三个用例核离线行为；固定硬件、系统、包 commit、模型 revision 与解码设置。本轮未录音、下载权重、安装 SDK 或复现 benchmark。

## 参考资料

- [README.md](https://github.com/FluidInference/FluidAudio/blob/c79c4106b954f81205113c3343e5a7e59a1089b5/README.md)（固定 commit）。
- [Package.swift](https://github.com/FluidInference/FluidAudio/blob/c79c4106b954f81205113c3343e5a7e59a1089b5/Package.swift)（固定 commit）。
- [Package@swift-6.2.swift](https://github.com/FluidInference/FluidAudio/blob/c79c4106b954f81205113c3343e5a7e59a1089b5/Package@swift-6.2.swift)（固定 commit）。
- [Documentation/Models.md](https://github.com/FluidInference/FluidAudio/blob/c79c4106b954f81205113c3343e5a7e59a1089b5/Documentation/Models.md)（固定 commit）。
- [Sources/FluidAudio/Shared/Download/ModelHub.swift](https://github.com/FluidInference/FluidAudio/blob/c79c4106b954f81205113c3343e5a7e59a1089b5/Sources/FluidAudio/Shared/Download/ModelHub.swift)（固定 commit）。
- [LICENSE](https://github.com/FluidInference/FluidAudio/blob/c79c4106b954f81205113c3343e5a7e59a1089b5/LICENSE)（固定 commit）。
- [正式发行列表](https://github.com/FluidInference/FluidAudio/releases)、[仓库 API](https://api.github.com/repos/FluidInference/FluidAudio)（动态状态）。
