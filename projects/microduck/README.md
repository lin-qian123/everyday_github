<!-- markdownlint-disable MD013 -->

# Microduck：把强化学习策略接到双足机器人的运行时

- 主上游：[pollen-robotics/microduck](https://github.com/pollen-robotics/microduck)；repository ID `1315850547`。
- 采样日期：2026-10-27（Asia/Shanghai）；分类：模型、训练与推理基础设施。
- API 累计快照：12,376 stars / 1,545 forks / 80 open issues（含 PR 口径），与榜单日增分开。
- 默认分支 `main`；本页主线静态依据固定在 `96b89d8613f06722c1d64ce75ab0d7124fed9d8f`。发行 API 首项 [daemon-v0.17.9](https://github.com/pollen-robotics/microduck/releases/tag/daemon-v0.17.9)，UTC 2026-10-26T11:19:51Z，正式发行标记。
- 核验层级：读取一手文档、许可、元数据与所列部分实现；未安装运行上游、调用模型或复现实验。

## 定位

Microduck 是 Pollen Robotics 小型双足机器人的机载软件，约 25 cm、800 g，采用 Rockchip RK3566、15 个舵机和 50 Hz 控制循环。这个仓库提供运行时、配置、媒体、蓝牙与更新服务；训练位于已收录的 [microduck_rl](../microduck_rl/README.md)，两者用途不同，不重复归并。

## 用法

已有机器人先看 cheat sheet，用只读命令检查状态与策略，而非直接覆盖固件：

```bash
robotctl monitor
robotctl policy list
robotctl policy check
```

修改策略、更新或控制机器人属于另一权限层。开发者可按文档用 `scripts/duck-sim` 在 MuJoCo 中运行真实 daemon，或按专用开发板安装流程准备硬件。本轮只查文档，未运行模拟、刷机、下载模型或驱动舵机；daemon-v0.17.9 的发布不是整套机器人 / 策略训练的版本号。

## 原理

相邻训练仓库通过 MuJoCo、PPO 和域随机化输出 ONNX 策略；本仓库的 robotd 负责推理、传感器和电机总线。configd 管配置与身份，padd 接手柄，btd 走蓝牙，mediad 处理 WebRTC，updaterd 负责签名更新与健康回滚。服务通过 Unix socket 上的 JSON-RPC 交换意图，由 robotd 保持控制与安全权威。

策略 manifest 区分持续步态和有终点的动作，并描述观测 / 动作维度、model_api、命令编码、时长与训练来源。可导入同格式文件，不代表它与所有硬件或动作条件兼容。

## 价值

为学习型机器人补足从策略到真机的工程层：控制权仲裁、掉线处理、版本、日志与回滚都可追踪。适合研究 sim2real 部署和可观测性；不能由 README 展示的步行、抓取或起身推断任意场地稳定、安全或具备通用 LLM 智能。

## 风险边界

- 架构提出 heartbeat / deadman、跌倒 / 关节 / 温度限制和物理优先接管；本轮未验证实际延迟、失联和急停行为。硬件实验仍需保护架、限幅和可触及急停。
- manifest 的 `obs_len`、`action_len`、`model_api` 等有接收检查，而 `hw_rev`、`servos`、`control_hz`、训练和 eval 字段部分仅展示。元数据齐全不是执行效果或安全认证。
- 蓝牙配对、网络 token、视频 / 麦克风远程会话是不同授权路径；设计要求会话同意和流媒体指示灯，不能仅凭加密传输推断没有隐私风险。
- 签名与健康回滚覆盖更新来源及部分启动状态，不证明社区策略动作安全；主线设计文档与某一已装发行的实现范围须逐项核对。
- 本仓库代码为 Apache-2.0；硬件、第三方依赖和外部策略权重需单独检查许可。

## 补充建议

先在模拟中固定 daemon SHA、策略文件哈希、manifest、控制频率和物理参数，再用保护架逐步检查站立、手柄接管、失联、异常输入与回滚。分别记录仿真结果和实体观察，避免把一次演示当成跨地形可靠性结论。

## 参考资料

- [README.md](https://github.com/pollen-robotics/microduck/blob/96b89d8613f06722c1d64ce75ab0d7124fed9d8f/README.md)。
- [docs/design/architecture.md](https://github.com/pollen-robotics/microduck/blob/96b89d8613f06722c1d64ce75ab0d7124fed9d8f/docs/design/architecture.md)。
- [docs/policy-manifest.md](https://github.com/pollen-robotics/microduck/blob/96b89d8613f06722c1d64ce75ab0d7124fed9d8f/docs/policy-manifest.md)。
- [docs/robot/cheatsheet.md](https://github.com/pollen-robotics/microduck/blob/96b89d8613f06722c1d64ce75ab0d7124fed9d8f/docs/robot/cheatsheet.md)。
- [LICENSE](https://github.com/pollen-robotics/microduck/blob/96b89d8613f06722c1d64ce75ab0d7124fed9d8f/LICENSE)。
- [仓库 API](https://api.github.com/repos/pollen-robotics/microduck)、[发行 API](https://api.github.com/repos/pollen-robotics/microduck/releases?per_page=1)；动态元数据仅代表本轮采样。
- 事实依据为以上一手材料；价值、风险判断与建议为本库工程分析，未写作实测结论。
