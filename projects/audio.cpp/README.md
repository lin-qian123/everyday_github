<!-- markdownlint-disable MD013 -->

# audio.cpp（0xShug0/audio.cpp）

> 上游仓库：<https://github.com/0xShug0/audio.cpp> · 归类：语音、视频与多模态 · 本页基于 2026-09-26 的 GitHub API、README、模型许可表、Release 与根 LICENSE 静态整理，未下载模型、编译 runtime 或生成 / 克隆任何音频。

- 抓取快照：3,031 stars、344 forks、19 open issues。
- 热度信号：GitHub C++ Trending 抓取时约 +23 当日 stars。
- 版本与许可：API 为 `NOASSERTION`，根 LICENSE 为 Apache-2.0；latest Release `v0.8.2-audio8-perf-hotfix`，同时存在正式 tag `v0.8.2`。

## 定位

audio.cpp 是基于 ggml 的原生 C++ 音频推理框架，统一 TTS、ASR、VAD、说话人分离、音源分离、voice cloning / conversion、音乐 / 音效生成、音频编辑与高层 pipeline，目标是在 Windows、Linux、macOS 和多种 GPU / CPU backend 上减少 Python 环境碎片。

## 用法

用户可下载 Release 中的 CPU、CUDA、Vulkan、Metal 构建，或按平台用 CMake / helper script 编译；model manager 从声明式 spec 安装 GGUF 包。CLI 用于单次任务，`audiocpp_server --ui` 提供本地 WebUI，启用 `--ui-management` 后还可浏览 / 下载模型、上传临时素材和切换模型。真实部署应先限定模型目录、监听地址、上传大小和并发。

## 原理

框架将不同音频模型移植到共享 ggml runtime，以统一 tensor、backend、session、CLI、server 与 WebUI surface。模型 family 通过 spec 描述包、精度和 loader；CUDA、HIP / ROCm、Vulkan、Metal 或 CPU 承担计算。实验性 pipeline 可把转录、切块、合并、语音重建、转换和后处理串成 JSON 工作流。

## 价值

它让大量原本依赖不同 Python 栈的音频模型共享原生部署与 server 接口，便于做本地 speech 应用、跨 backend 对比、资源受限部署和多模型 Arena。模型许可表、community / core 边界和性能测试说明为选型提供了比简单支持列表更好的审计入口。

## 风险边界

- Apache-2.0 只覆盖 audio.cpp 源码；README 明确模型权重保留原始许可，部分为 NC / NC-SA、仅本地转换或等待再分发批准，商用前必须逐 family 检查。
- voice cloning、speech editing、音乐 / 音效生成涉及声音同意、身份冒用、版权、人格权和平台政策；技术可运行不代表获得输入、模型或输出的权利。
- README 性能数字来自作者在特定 RTX 5090 / CUDA、模型与基准路径上的测量，本轮未复现；不同 backend 和模型覆盖不一致，量化还可能破坏稳定性与质量。
- `--ui-management` 可下载模型、处理上传与动态切换；对非 loopback 暴露会扩大远程上传、磁盘写入、模型供应链和 GPU DoS 风险。
- Release hotfix tag 与正式 tag 并存、项目迭代很快；server / pipeline / community model surface 仍可能改变，需 commit-level pinning。

## 补充建议

从一个许可证明确、无克隆能力的小模型开始，固定 Release asset、模型 revision、hash 和 backend，在授权音频金标上测 WER / MOS、延迟、峰值 RAM / VRAM、长音频、并发与失败恢复。server 只绑定 loopback、关闭 management 或使用 allowlist；对 voice / music 路径增加可验证同意、来源记录、水印 / 披露和人工发布闸门。

## 参考资料

- [GitHub 仓库](https://github.com/0xShug0/audio.cpp)
- [GitHub REST API](https://api.github.com/repos/0xShug0/audio.cpp)
- [v0.8.2-audio8-perf-hotfix Release](https://github.com/0xShug0/audio.cpp/releases/tag/v0.8.2-audio8-perf-hotfix)
- [Model License Matrix](https://github.com/0xShug0/audio.cpp/blob/main/docs/model_licenses.md)
- [Model Manager](https://github.com/0xShug0/audio.cpp/blob/main/docs/model_manager.md)
- [Server 文档](https://github.com/0xShug0/audio.cpp/blob/main/app/server/README.md)
- [LICENSE](https://github.com/0xShug0/audio.cpp/blob/main/LICENSE)
