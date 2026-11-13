<!-- markdownlint-disable MD013 -->

# Veyra-NRVideo：Windows 上的视频增强与采集预览工作台

- 上游：[`Likely7/Veyra-NRVideo`](https://github.com/Likely7/Veyra-NRVideo)；仓库 ID：`1362562155`。
- 核读：2026-11-14（Asia/Shanghai）07 时段；主线固定于 [`8332c8a83822`](https://github.com/Likely7/Veyra-NRVideo/tree/8332c8a8382242096a2699d3ba4dd52ad47bbd74)。
- 热度快照：官方综合 / C++ daily +245；[API](https://api.github.com/repos/Likely7/Veyra-NRVideo) 为 1,593 stars / 71 forks / 60 open issues（含 PR）。首次建档不等于今日首发。

## 定位

把本地视频、图片、采集卡、屏幕和主机 / PC 串流接入同一 GPU 增强链，组合超分辨率、NR 画面增强、调色、HDR 与补帧。它是播放器和处理工作台，不是修改游戏引擎渲染帧率的补丁。稳定便携包 [v2.1.5](https://github.com/Likely7/Veyra-NRVideo/releases/tag/v2.1.5) 发布于 UTC 11-10，另有同版本源码发行。

仓库描述中的“PS5 GTA6 120FPS / DLSS 5”是使用场景与宣传措辞；README 自身明确社区运行库不代表厂商认证或完整官方 DLSS 5 集成。

## 用法

要求 Windows 11 x64、DirectX 12 与受支持显卡 / 驱动。按 **Veyra 实际使用的 GPU** 选择 NVIDIA 或 AMD 便携包，完整解压至可写目录，运行 `veyra_qml_ui.exe`；普通运行不需安装 Qt 或开发 SDK。本轮未下载或执行程序。

先关闭效果检查基础画面和声音，再逐项打开超分、NR、HDR 和补帧，核实显存、输入节奏与显示同步。采集卡需选正确分辨率、帧率、像素格式、音轨和色彩范围。PS5、PC 与 Xbox 串流各有主机设置 / 配对要求，Xbox 为非官方实验功能。

升级前退出旧版并备份数据。新目录迁移只复制 `runtime_local/user-data-2.0.0` 和自定义 `runtime_local/luts`，自定义数据目录以“设置 → 关于”为准；不把整份旧运行库混入新版。离线导出先切回列表并确认效果，节点链不自动转换；实时补帧可用也不代表同后端支持离线补帧。

## 原理

Qt Quick / QML 管界面，输入抽象提供帧、时间戳和色彩信息，共享 EnhanceGraph 执行有效处理链，由原生 D3D12 窗口呈现。NR / 调色可分层，图链有连接与顺序约束，补帧位于末端；可见但未接通的草稿节点不会运行。

2.1.5 针对“40 FPS 内容经过 60 Hz 采集”去重后约 17 / 33 ms 交替到达的问题，按内容时间轴调度生成帧；异常设备时间戳的预览修正与音频读取原始驱动时间分开。它改善呈现节奏，并未增加游戏逻辑更新或真实采集信息量。

## 价值

适合在固定素材与硬件上比较增强顺序、HDR、插帧和采集链，或把播放器预览与导出纳入可追溯流程。上游 2.1.5 的 T911、4K60 NV12、约 40 FPS 内容、VFG 3× A/B 提供了有用的取舍：约 120 提交 FPS 下，提交间隔 P99 从 17.33 降至 9.04 ms，真实帧的采集回调到 Present 返回中位耗时却从 24.12 增至 31.54 ms。这是作者软件侧测量，不是本轮复现或屏幕端到端延迟。

## 风险边界

- **质量与时延**：提交 FPS、物理显示帧数、真实源帧和输入到光子的延迟是不同指标。补帧 / NR 可能引入重影、HUD 或字幕失真、纹理与颜色变化；不能按宣传标题认定游戏原生达到 120 FPS。
- **硬件与实验后端**：主要实测为 RTX 5070；RX 7000 NR 的协议 / CPU fixture 不证明 Radeon 实卡推理。8K、多层 NR 和补帧组合不保证实时；长期 Xbox、VRR 采集、部分社区 NR / 补帧仍有未验证项。
- **许可与分发**：根代码 GPL-3.0；含 Chiaki 的组合程序还涉及 AGPL-3.0 与 OpenSSL 例外。模型、厂商 DLL、ZLUDA、驱动和其他依赖各有权利边界，开源播放器许可证不能替代整包分发许可。
- **来源与恢复**：构建文档列出应用构建提交 `01dc81b3b4ac`、源码 / EXE 哈希和固定依赖，主线文档提交与实际构建提交不同。本轮只核文档 / 发行元数据，没有下载计算哈希、验签或复现构建。更新检查会联网；日志和崩溃转储分享前须检查内容。

## 补充建议

用同一原片建立无增强基线，逐项固定输入帧率、像素格式、色彩 / HDR、显卡驱动、后端和倍率。分别记录真实 / 生成 / 丢弃帧、帧间隔分布、音画同步、GPU / 显存与外部端到端延迟，再完整观看运动、遮挡、字幕和暗部片段。

保留原始素材、设置和发行清单，先用数据副本演练迁移与回退。科研图像或定量测量应保留原数据；生成式增强结果需显式标记，不用作新增物理细节的证据。

## 参考资料

- [固定主线中文 README](https://github.com/Likely7/Veyra-NRVideo/blob/8332c8a8382242096a2699d3ba4dd52ad47bbd74/README_CN.md)：安装、处理链、平台和已知边界。
- [2.1.5 更新与软件计时](https://github.com/Likely7/Veyra-NRVideo/blob/8332c8a8382242096a2699d3ba4dd52ad47bbd74/docs/RELEASE_NOTES_2.1.5.md)、[构建与对应源码](https://github.com/Likely7/Veyra-NRVideo/blob/8332c8a8382242096a2699d3ba4dd52ad47bbd74/docs/BUILD_2.1.5.md)。
- [第三方来源 / 许可](https://github.com/Likely7/Veyra-NRVideo/blob/8332c8a8382242096a2699d3ba4dd52ad47bbd74/THIRD_PARTY_NOTICES.md)、[根许可证](https://github.com/Likely7/Veyra-NRVideo/blob/8332c8a8382242096a2699d3ba4dd52ad47bbd74/LICENSE)、[2.1.5 源码发行](https://github.com/Likely7/Veyra-NRVideo/releases/tag/v2.1.5-sources)。
