<!-- markdownlint-disable MD013 -->

# OOOSplat

> 更新：2026-11-11（Asia/Shanghai）。分类：语音、视频与多模态。上游 `ooolabdev/ooosplat`，仓库 ID `1335212031`；源码 `82d46203635dfb338f8fa5118c9c09bd66f905ec`。仅静态核读，未安装、处理素材、训练高斯、操作 MCP 或做视觉 / 几何验收。

## 定位

OOOSplat 是把视频或图片序列转成 3D Gaussian Splatting 的本地桌面流水线，集成抽帧、相机重建、训练、预览、非破坏编辑与导出。它重建输入视角对应的外观，不是仅凭文字生成三维网格的模型。[README](https://github.com/ooolabdev/ooosplat/blob/82d46203635dfb338f8fa5118c9c09bd66f905ec/README.md)

Rust daily 为 +38 stars；API 为 2,439 stars / 288 forks / 25 open issues（含 PR）。最新列出 [0.7.1](https://github.com/ooolabdev/ooosplat/releases/tag/0.7.1)，UTC 10-28 发布，标记预发行；清单同为 0.7.1。`releases/latest` 无稳定版不等于没有包。[API](https://api.github.com/repos/ooolabdev/ooosplat)

## 用法

按平台选安装包：Windows、macOS 15+ Apple silicon Alpha、Ubuntu 24.04 x86_64 Alpha 的引擎与验证范围不同。选择普通视频 / 图片或支持的完整 ERP 全景，指定项目目录和质量档位，生成后检查注册率、实际后端及预览，再导出 PLY / SPZ / SOG 等。[平台与素材说明](https://github.com/ooolabdev/ooosplat/blob/82d46203635dfb338f8fa5118c9c09bd66f905ec/README.md)

源码常规流程如下；**macOS 当前分发清单的混合运行时哈希未锁定，会拒绝常规下载**，须先按上游构建流程处理，不要把这段命令当成所有平台即装即用：

```bash
npm ci
npm run setup:engines
npm run verify:engines
npm run verify:licenses
npm run tauri -- dev
```

MCP 可选，初始关闭；启用后默认监听 `127.0.0.1:39877/mcp` 并授权项目根下 Inputs 目录，其他输入目录另加。工具操作运行中的桌面后端，云端自身的 localhost 不能直接连接本机。[MCP 指南](https://github.com/ooolabdev/ooosplat/blob/82d46203635dfb338f8fa5118c9c09bd66f905ec/docs/mcp-v1.md)

## 原理

Tauri / Rust 后端驱动 FFprobe / FFmpeg、COLMAP 和 Brush：先分析 / 抽帧，再估计相机与稀疏结构，最后优化高斯并发布 `final.ply`。COLMAP 的 CUDA / CPU 路径与 Brush 的 Vulkan / Metal 路径独立；macOS COLMAP 当前用 CPU，不能概括成整套 GPU 或整套 CPU 推理。[流水线](https://github.com/ooolabdev/ooosplat/blob/82d46203635dfb338f8fa5118c9c09bd66f905ec/README.md)

新策略默认含重建优化和补帧；明确 GPU OOM 且有可信点数时最多重试一次，将点数上限降至失败时可信点数的 80%，不降低训练分辨率。设备丢失、一般失败与 OOM 分开处理，自动重试开关也不关闭正常补帧或兼容后端回退。[0.7.1 说明](https://github.com/ooolabdev/ooosplat/releases/tag/0.7.1)

## 价值

适合把拍摄素材变成可查看和编辑的外观重建，并保留中间相机、训练和日志资产用于诊断。对希望研究采样、注册率、资源预算与导出损失的人，比只返回成品的远端服务更可观察；“一键”仍需要合适拍摄和独立质量检查。

## 风险边界

- **本地重建不等于没有外发**：匿名统计默认开启，发送随机安装 ID、平台、事件与阶段 / Planner 指标；设置中可关闭。主动错误报告为单独预览 / 同意，更新检查又是另一条通路。没有原始素材上传声明不等于零网络。[隐私说明](https://github.com/ooolabdev/ooosplat/blob/82d46203635dfb338f8fa5118c9c09bd66f905ec/README.md) / [统计默认值](https://github.com/ooolabdev/ooosplat/blob/82d46203635dfb338f8fa5118c9c09bd66f905ec/src-tauri/src/telemetry/service.rs)
- **MCP 无逐 Agent 身份隔离**：不生成或校验 token，旧 Authorization header 被忽略；Host / Origin 和输入根限制仍存在，但启用后本地客户端共享工具与任务。不能把 loopback 当成可信客户端认证。[MCP 边界](https://github.com/ooolabdev/ooosplat/blob/82d46203635dfb338f8fa5118c9c09bd66f905ec/docs/mcp-v1.md)
- **跨平台支持有条件**：macOS 包未签名 / 未公证，Intel Mac 不支持；Ubuntu 作者端到端验证主要在 NVIDIA，CPU-only 软件图形路径尚未闭环。macOS 源码分发哈希仍为空，与已含引擎的安装包不是同一问题。[源码清单](https://github.com/ooolabdev/ooosplat/blob/82d46203635dfb338f8fa5118c9c09bd66f905ec/engines/manifest.macos.json)
- **好看不证明几何准确**：反光、低纹理、运动物体和不足重叠影响重建。SPZ 越界处理可能改变导出副本的位置、尺度和单位；压缩、能打开大模型与能完整训练也有不同条件。[格式与质量限制](https://github.com/ooolabdev/ooosplat/blob/82d46203635dfb338f8fa5118c9c09bd66f905ec/README.md)
- 第一方代码 Apache-2.0；FFmpeg、COLMAP、Brush 等有独立许可，生成模型与输入素材权利不能由软件许可自动推得。[许可说明](https://github.com/ooolabdev/ooosplat/blob/82d46203635dfb338f8fa5118c9c09bd66f905ec/README.md)

## 补充建议

先用短而清晰、视角重叠足够的自有素材，记录输入 SHA、抽帧 / 相机配置、注册数量、后端、显存、重试和耗时；留一组未参与训练的视角检查外观。若要量测，再用已知尺寸 / 标定物验证坐标和尺度。导出后在目标查看器重开，分别验单位、颜色、裁切和压缩损失；MCP 测试通过不能替代真实 GPU 流水线验收。

## 参考资料

1. [固定 SHA README](https://github.com/ooolabdev/ooosplat/blob/82d46203635dfb338f8fa5118c9c09bd66f905ec/README.md)
2. [0.7.1 预发行](https://github.com/ooolabdev/ooosplat/releases/tag/0.7.1)
3. [MCP 功能与验证范围](https://github.com/ooolabdev/ooosplat/blob/82d46203635dfb338f8fa5118c9c09bd66f905ec/docs/mcp-v1.md)
4. [macOS 引擎清单](https://github.com/ooolabdev/ooosplat/blob/82d46203635dfb338f8fa5118c9c09bd66f905ec/engines/manifest.macos.json)
5. [第一方许可](https://github.com/ooolabdev/ooosplat/blob/82d46203635dfb338f8fa5118c9c09bd66f905ec/LICENSE) / [Rust Trending](https://github.com/trending/rust?since=daily)
