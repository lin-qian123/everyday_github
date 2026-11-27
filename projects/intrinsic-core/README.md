<!-- markdownlint-disable MD013 -->

# intrinsic-core：连接感知、规划与工业机器人执行的本地运行栈

- 上游：[intrinsic-ai/intrinsic-core](https://github.com/intrinsic-ai/intrinsic-core)，repository ID `1360910719`；2026-11-28 新建档案。
- 快照：811 stars / 103 forks / 13 open issues（累计，含 PR）；C++ daily +7。
- 默认 SHA `3761260f4818dfa3228ad471162d00bc6a354a1d`，2026-11-27；最新所见发行 `20261022.0`（10-22），annotated tag 指向提交 `50927e35c5c85992b2a4d0b91dabb9cf4172b2d5`。下述主线感知能力未据此归入旧发行。
- 范围：非截断 tree、固定 README、入门、感知文档、主机设置脚本与许可的局部静态核读；未运行脚本、下载发行制品 / 权重、安装 k3s、仿真或连接机器人。

## 定位

Intrinsic Core 提供工业机器人的本地 runtime、SDK、硬件抽象和实时控制基础，尝试把感知、运动规划、数字孪生和真实执行接到同一套应用结构中。它与关联的 OMTS 机床上下料参考方案配合，面向机器人开发和系统集成。

AI 体现在视觉感知与本地推理等模块，并非将任意自然语言直接安全地转成机器人动作。README 也声明它不是官方支持的 Google 产品，源码公开不等于厂商为某个工位提供完整支持。

## 用法

1. 先固定 Core 的版本和对应 OMTS、硬件资产及构建工具。所查入门示例将 Core 固定为 `20261022.0`，却动态取 OMTS 最新发行；复现时还需固定后者，不能只记录一个 Core tag。
2. 以详细入门为目标环境基线：Ubuntu 26.04、x86-64；ARM 明确不支持。仿真可用 AMD，真实硬件实时控制要求 Intel。README 还列较旧 Ubuntu，存在文档范围差异，不能推定所有组合已验收。
3. 入门建议至少 32 GiB RAM、100 GB 可用空间；完整带感知 OMTS 仿真需要独立 NVIDIA GPU。仅显示仿真与跑视觉推理是不同资源需求。
4. 在专用主机检查 `setup_k3s.sh`、GPU 和实时设置脚本，再部署 runtime / inctl，构建 OMTS。入门仿真命令如下，仅摘录，未执行：

   ```bash
   bazel run //:omts_solution --config=lab_bb_01 -- \
     --address localhost:17080 --operation_mode=sim
   ```

5. 先验证仿真模型、坐标、相机标定和故障恢复，再由具备资质的集成人员按目标设备要求处理真实硬件调试与工位验收。文档的约 50 分钟构建时间只是其示例说明。

## 原理

runtime 使用 k3s 管理容器化组件与状态；ICON 负责实时控制和 HAL，规划模块计算受约束的运动路径，SDK / API 连接资产、技能和服务。HAL 减少应用与某种驱动的耦合，但具体机械臂、工具和 I/O 仍需驱动、配置及标定。

所查主线 NVIDIA Pose Estimator 将 SAM 3 分割、FoundationStereo 深度与 FoundationPose 6D 位姿估计组合，通过 gRPC 提供服务；运行时采用 TensorRT 10.16，而非依赖 PyTorch。权重 / 资产、推理引擎、感知结果、规划与实际控制是不同阶段，不能以某个服务已启动代替整条运动链验证。

该文档说明按阶段预热并缓存 TensorRT plans；若预热失败服务仍可启动，首请求会在 GPU 锁内补编译。plans 与目标 GPU、TensorRT 版本相关，启动成功或缓存存在都不证明时延要求达标。

## 价值

它把工业机器人应用中常见的系统接线公开为可追踪的模块，适合研究感知到规划 / 控制的接口，以及数字孪生如何支持调试。OMTS 为实际制造任务提供阅读和仿真入口。

对工程选型，更有价值的是验证目标硬件的兼容、时延、恢复与资产版本一致性。README 的实时、无硬件锁定和开箱即用描述是设计目标 / 作者声明，本轮没有对应实机测量。

## 风险边界

| 议题 | 已核事实与边界 |
| --- | --- |
| 平台与版本 | README 列多个 Ubuntu 版本，详细入门要求 26.04；main 晚于发行，且 Core / OMTS 示例固定方式不同，应按完整版本组合验收。 |
| 主机改动 | k3s 设置脚本涉及安装服务、containerd 用户组 / socket、kubeconfig 与 sysctl；实时脚本涉及内核包、CPU affinity、TuneD 和 GRUB。不是普通虚拟环境安装。 |
| 物理行为 | 仿真成功不证明真实工位的碰撞、限位、急停和人员防护满足要求；软件控制和现场安全功能分别验收。 |
| 模型许可 | Core 根 Apache-2.0 不覆盖所有权重；主线文档要求为 gated SAM 3 接受 Meta SAM License，并指出相关词表也是 SAM Materials。 |
| 运行与质量 | 预热失败后仍可接请求；plans 不跨 GPU / TensorRT 通用。6D pose 输出不等于任意物体、遮挡或照明下的可靠识别。 |
| 图像去向 | 主线文档说磁盘 debug dump 默认未设置，但 visualization 发布默认 true；“不落盘”和“不向其他订阅者发布”是不同边界。 |

## 补充建议

1. 记录 Core / OMTS 提交、Bazel 依赖、资产 digest、驱动、GPU、TensorRT、相机内外参和标定件，先建立可重复的小仿真。
2. 在专用主机保存设置前状态，验证服务、网络、权限、内核 / 引导和卸载恢复，避免直接改动日常工作机。
3. 用标注姿态和目标场景测位置 / 角度误差、失败率及冷 / 热请求时延；显式测试预热失败、模型替换、相机断连和恢复。
4. 真机测试由设备负责人确定操作模式、防护与急停流程；控制周期、任务成功率和现场安全验收分别记录。

## 参考资料

- [仓库 API](https://api.github.com/repos/intrinsic-ai/intrinsic-core)、[固定 README](https://raw.githubusercontent.com/intrinsic-ai/intrinsic-core/3761260f4818dfa3228ad471162d00bc6a354a1d/README.md)、[20261022.0 发行](https://github.com/intrinsic-ai/intrinsic-core/releases/tag/20261022.0)、[固定入门](https://raw.githubusercontent.com/intrinsic-ai/intrinsic-core/3761260f4818dfa3228ad471162d00bc6a354a1d/developer_resources/learn/tutorials/getting_started.md)。
- [k3s 设置](https://raw.githubusercontent.com/intrinsic-ai/intrinsic-core/3761260f4818dfa3228ad471162d00bc6a354a1d/intrinsic_runtime/setup_k3s.sh)、[实时设置](https://raw.githubusercontent.com/intrinsic-ai/intrinsic-core/3761260f4818dfa3228ad471162d00bc6a354a1d/intrinsic_runtime/setup_realtime.sh)、[GPU 设置](https://raw.githubusercontent.com/intrinsic-ai/intrinsic-core/3761260f4818dfa3228ad471162d00bc6a354a1d/intrinsic_runtime/setup_nvidia.sh)。
- [主线感知说明](https://raw.githubusercontent.com/intrinsic-ai/intrinsic-core/3761260f4818dfa3228ad471162d00bc6a354a1d/intrinsic_perception/intrinsic/perception/service/nvidia_pose_estimator/README.md)、[LICENSE](https://raw.githubusercontent.com/intrinsic-ai/intrinsic-core/3761260f4818dfa3228ad471162d00bc6a354a1d/LICENSE)、[SECURITY](https://raw.githubusercontent.com/intrinsic-ai/intrinsic-core/3761260f4818dfa3228ad471162d00bc6a354a1d/SECURITY.md)。
