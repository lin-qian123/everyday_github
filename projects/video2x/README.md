<!-- markdownlint-disable MD013 -->

# video2x（k4yt3x/video2x）

- 更新：2026-11-06（Asia/Shanghai）；官方 C++ daily +51，为读取快照，不是自然日结算。
- GitHub API：22,617 stars / 1,975 forks / 145 open issues（含 PR）；仓库 ID `122758193`。
- 核读基线：`7db9c18d6278bbad9c3eda0e4e4ae210f9a688eb`；文档与抽样实现核验，不是安装运行、安全或性能认证。

## 定位

Video2X 是视频超分辨率和插帧框架。6.x 已由旧版 Python / 管道方案改为 C/C++，结合 FFmpeg、libplacebo、ncnn / Vulkan 调度 Anime4K、Real-ESRGAN、Real-CUGAN 与 RIFE。适合本地批量视频后处理；它不能恢复原视频从未记录的事实细节。

## 用法

当前稳定 Release 为 `6.4.0`（UTC 2025-01-24），不是今日新发版。Windows 可选 Qt6 安装包，Linux 有发行包 / AppImage；预编译 CPU 要求 AVX2，GPU 要求 Vulkan。先在目标机器确认驱动、后端和模型文件，再用授权短片试跑：

```bash
video2x --list-gpus
video2x -i input.mp4 -o output.mp4 -p realesrgan -s 4 --realesrgan-model realesr-animevideov3
```

第一条列设备，第二条是官方 CLI 的 4 倍超分示例；不是插帧命令。RIFE 走独立插帧选项，应按安装版本的 `--help` 核对。输出使用新文件名，记录 codec、像素格式与模型，先检查几十秒再处理长片。本轮没有安装、下载模型或转码。

## 原理

6.x 架构按解码 → 处理 → 编码传递 `AVFrame`，只在需要时转换像素格式，避免旧架构把每帧写入磁盘。文档注明尽量留在 GPU 的路径仍部分实现，不能称全链零拷贝。超分生成更高分辨率帧，RIFE 估计中间帧；两者分别改变空间与时间采样，均可能产生伪影。

## 价值

将多个增强后端和编码参数组织成统一 CLI / GUI，便于对自己的素材做可重复比较。有效质量指标包括文字、线条、纹理、遮挡、镜头切换、音画同步和人工观看；更高分辨率或帧率本身不能证明更忠实。

## 风险边界

- **历史演示与当前制品分开**：README 明标视频演示 Outdated；360P→4K 描述不能覆盖视频标题的 1080P，也不能证明 6.4.0 的实时性能。硬件、模型、输入与编码参数必须一起报告。
- **macOS 路径需验证**：README 对原生支持写 Windows / Linux，又称容器可用于 macOS；容器实际要求 Vulkan GPU。本轮未验证 Apple Silicon / Docker GPU 通路，不能从“能启动容器”推出能加速运行。
- **容器权限**：上游排障示例含 `--privileged` 和可写目录挂载；不应把扩大主机权限作为默认安装前提，应先定位 GPU / 驱动问题并限定挂载。
- **素材与依赖许可**：根代码 AGPL-3.0，依赖、权重、编码器和输入素材的许可各自核对；仓库示例还明确列出动画版权归属。公开演示入口不等于允许再发布素材。
- 超分会生成猜测纹理，插帧会生成中间运动；证据、科研测量和档案用途须保留原片、参数及处理标记。Colab 免费额度等 README 宣传不是当前资源保证。

## 补充建议

建立授权短片集，包含文字、细线、暗部、快速移动和切镜；固定模型 / commit、输入哈希和编码参数，分别比较超分、插帧与串联路径。验证帧数、时长、色彩、音轨 / 字幕和主观伪影，再评估整片耗时、显存和输出体积。

## 参考资料

- [README.md](https://github.com/k4yt3x/video2x/blob/7db9c18d6278bbad9c3eda0e4e4ae210f9a688eb/README.md)
- [docs/book/src/running/command-line.md](https://github.com/k4yt3x/video2x/blob/7db9c18d6278bbad9c3eda0e4e4ae210f9a688eb/docs/book/src/running/command-line.md)
- [docs/book/src/developing/architecture.md](https://github.com/k4yt3x/video2x/blob/7db9c18d6278bbad9c3eda0e4e4ae210f9a688eb/docs/book/src/developing/architecture.md)
- [docs/book/src/running/container.md](https://github.com/k4yt3x/video2x/blob/7db9c18d6278bbad9c3eda0e4e4ae210f9a688eb/docs/book/src/running/container.md)
- [仓库与 API 快照](https://api.github.com/repos/k4yt3x/video2x)；[发行列表](https://github.com/k4yt3x/video2x/releases)。
- [发行 6.4.0](https://github.com/k4yt3x/video2x/releases/tag/6.4.0)。
