<!-- markdownlint-disable MD013 -->

# spirula-studio（harry7557558/spirula-studio）

- GitHub：<https://github.com/harry7557558/spirula-studio>
- 抓取快照：2026-09-24，720 stars、55 forks、35 open issues
- 热度信号：GitHub 综合 Trending 抓取时约 +99 当日 stars
- 版本与许可：GPL-3.0；latest GitHub Release 为 `v2026.9.20`

## 定位

Spirula Studio 是一体化 3D Gaussian Splatting（3DGS）训练与重建工具，把照片 / 视频抽帧、SfM、AI masking、训练、viewer 和 mesh 导出组合到单个 C++ 应用。它同时提供 GUI 与 CLI，以 Vulkan 覆盖 NVIDIA、AMD、Intel、Apple GPU，并保留 CUDA 后端。

## 用法

桌面用户可从 Release 下载 Windows、Linux 或 macOS 构建，导入照片 / 视频后走 dataset、train、mesh 流程；远端训练可用 `spirula train` 并通过 HTTP viewer 观察进度。源码构建推荐 Vulkan backend，macOS 通过 MoltenVK；CUDA 路径仅面向 NVIDIA。AI masking 需另行下载 SAM checkpoint。

## 原理

CLI 与 ImGui GUI 共用 `TrainerCore`，再进入不含 CUDA 依赖的 process-global engine；`backend/api` 将训练逻辑分到 CUDA kernels 或 Vulkan launchers / Slang shaders。数据层原生解析 COLMAP、Nerfstudio、Metashape，训练和 checkpoint、eval、web viewer 均在 C++ 中实现；3DGS、Mip 与 3DGUT 是编译期 primitive 类型。

## 价值

它降低了从视频到 splat / textured mesh 的多工具拼装成本，也让非 NVIDIA GPU、Apple Silicon 和 360° 相机进入较一致的工作流。GUI 适合快速试验，CLI、batch 和统一配置则便于形成可复现的内容生产或科研流水线。

## 风险边界

- README 的 10M Gaussians / 8 GB VRAM、跨 vendor 性能与画质主张依赖数据集、driver、backend 和参数，本轮未独立复现。
- 3D 重建会处理人物、室内和地理环境影像；采集同意、隐私、素材版权与发布权限需在训练前处理。
- `-DSS_ENABLE_PATENTED=ON` 涉及 AVC / HEVC 专利责任；SAM 2.1 与 SAM 3 checkpoint 的许可证不同，均不随 GPL 主程序自动覆盖。
- engine 是 process-global singleton，切换 dataset 需正确 reset；长批处理、并发隔离和 checkpoint 恢复应先做故障注入。
- 单维护者项目与快速版本节奏意味着生产环境应固定 Release、GPU driver、模型 checkpoint 和输出格式。

## 补充建议

先用自有或明确授权的短视频建立小型金标，固定相机模型、backend、driver、训练预算与 commit，对比几何完整性、颜色、floaters、mesh 回读、峰值 VRAM 和耗时。把照片 / 视频许可、SAM 权重许可、AVC / HEVC 选项和导出资产许可记录在同一 provenance 清单中。

## 参考资料

- [GitHub 仓库](https://github.com/harry7557558/spirula-studio)
- [GitHub REST API](https://api.github.com/repos/harry7557558/spirula-studio)
- [v2026.9.20 Release](https://github.com/harry7557558/spirula-studio/releases/tag/v2026.9.20)
- [架构说明](https://github.com/harry7557558/spirula-studio/blob/master/docs/architecture.md)
- [测试说明](https://github.com/harry7557558/spirula-studio/blob/master/docs/testing.md)
- [LICENSE](https://github.com/harry7557558/spirula-studio/blob/master/LICENSE)
