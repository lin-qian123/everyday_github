<!-- markdownlint-disable MD013 -->

# NeuralNote v2（DamRsn/NeuralNote）中文解读

> 上游仓库：<https://github.com/DamRsn/NeuralNote> · 归类：语音、视频与多模态 · 证据快照：2026-10-17（Asia/Shanghai）。API：3,198 stars / 227 forks / 24 open issues；GitHub Release / CMake `v2.1.0` / `2.1.0`；代码 Apache-2.0；MuScriptor 权重 CC BY-NC 4.0，另有第三方组件条款。本页为上游资料与相关代码的静态整理，未安装运行、复测性能或完成全面安全审计。

## 定位

NeuralNote 是把音频转成可编辑 MIDI 的 VST3 / AU / Standalone 工具。v2 用 MuScriptor transformer 替换旧 Basic Pitch，支持多乐器分组和内置合成试听；适合教学分析、扒谱初稿与音符整理，MIDI 转录仍不是排好版、声部 / 指法可靠的正式乐谱。

## 用法

按平台从上游 Release 选择制品，在 DAW 测试副本或 Standalone 里加载一段有权使用的短音频，选择乐器、模型与 compute device 后转录，逐乐器试听并导出 / 拖出 MIDI。模型首次需另下载；先选 small。README 称 macOS 安装包签名 / notarized、Windows 未签名，Linux 预编译尚在 roadmap；本次没有验证制品签名或实际安装。

## 原理

- JUCE 插件采集或载入音频，独立的 muscriptor.cpp / ggml 引擎在本机解码音符事件，再按乐器渲染 piano roll / synth。
- small / medium / large GGUF 模型分别约 210MB / 620MB / 2.7GB，从 Hugging Face 下载；Metal / Vulkan / CPU 的速度取决于平台与设备。
- 可暂停 / 续跑，输出 MIDI 供 DAW 后续编辑；引擎与 GUI 分仓，便于独立评估。

## 价值

本机转录减少把原始录音交给云推理服务的需求；分乐器试听和可编辑 MIDI 让人工纠错更直接。评价应比较音高、起止、重叠声部、乐器识别和人工修订时间；README 的 M1 Pro 速度只是特定机器作者测量。

## 风险边界

- **代码与权重许可不同**：README 明确 MuScriptor 权重 CC BY-NC 4.0，只能非商业使用；Apache-2.0 仅覆盖代码，不能据此认定默认模型适合商业制作。
- README 称推理音频不出本机，仅联网下载模型与查更新；本次未做完整出站审计。DAW、插件宿主、crash report、项目备份另有数据边界。
- 音符 / 乐器 / 时值会出错，密集混音和打击乐等需金标核对，导出 MIDI 不等于完整记谱或可演奏编配。
- 硬件覆盖仍有限，较大模型未必实时；JUCE、ASIO、字体 / soundfont 等第三方条款和 Windows 制品信任要独立核查。

## 补充建议

用自录单声部与授权多声部各 20–30 秒建立金标，记录 note onset / offset、音高错误、乐器误分、推理时间和修改工时。学习 / 非商业测试先用 small；商业计划先核清模型使用条件，保留原音频与人工修订 provenance。

## 参考资料

- 上游仓库：<https://github.com/DamRsn/NeuralNote>
- GitHub REST API：<https://api.github.com/repos/DamRsn/NeuralNote>
- README / 使用 / 权重许可：<https://github.com/DamRsn/NeuralNote/blob/main/README.md>
- 应用版本：<https://github.com/DamRsn/NeuralNote/blob/main/CMakeLists.txt>
- 代码许可：<https://github.com/DamRsn/NeuralNote/blob/main/LICENSE>
- 第三方许可清单：<https://github.com/DamRsn/NeuralNote/blob/main/Installers/license.txt>
- Releases：<https://github.com/DamRsn/NeuralNote/releases>
