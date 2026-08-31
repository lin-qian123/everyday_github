<!-- markdownlint-disable MD013 MD034 -->

# microduck_rl：面向 Microduck 双足机器人的强化学习与 sim2real 环境

## 项目概览

- 上游仓库：https://github.com/pollen-robotics/microduck_rl
- GitHub API 快照（2026-09-01）：1,119 stars、193 forks、15 个开放 issue
- 默认分支：`develop`
- 主要技术：Python、MuJoCo、mjlab、强化学习、ONNX
- 代码许可证：Apache-2.0；上游注明 3D 模型文件为 CC BY-SA-NC

## 定位

microduck_rl 为 Pollen Robotics 的小型双足机器人 Microduck 提供强化学习训练环境、机器人模型、执行器模型、策略导出和仿真回放。任务包括行走、跌倒恢复、坐站、踢球、翻滚、轮滑和不同地形控制。

## 用法

上游使用 `uv` 管理环境。典型流程是训练策略、在 viewer 中回放、导出 ONNX，再用 CPU MuJoCo 键盘控制做部署前演练：

```bash
uv run train Mjlab-Velocity-Flat-MicroDuck --env.scene.num-envs 4096
uv run scripts/export.py Mjlab-Velocity-Flat-MicroDuck --wandb-run-path <run>
uv run scripts/infer_policy.py --walking output.onnx
```

没有本地 GPU 时，上游还提供 Hugging Face Jobs 入口。任何真机部署都应先完成仿真回归、限幅、急停和低能量测试。

## 原理

项目在 MuJoCo/mjlab 中并行运行大量环境，通过奖励函数和域随机化训练运动策略。执行器层使用针对 Dynamixel XL330 的 BAM M6 模型，并随机化电池电压、压降、延迟和摩擦；Backlash 变体为伺服齿隙增加被动关节和输出侧编码器观测。

策略导出为 ONNX 后，运行时通过共享的 61 维观测契约在步行、恢复和动作策略间切换。这个契约有利于部署，但仿真中的观测一致并不保证真实机器人上的稳定性。

## 价值

- 将小型双足机器人的训练、仿真、导出和部署接口放在同一仓库。
- 对执行器、齿隙与电池效应建模，明确面向 sim2real 差距。
- 多任务和地形变体适合研究策略复用、恢复和动作切换。
- 提供测试台、观测对比和日志脚本，便于定位仿真/真机差异。

## 风险边界

- 真机 RL 策略可能导致跌落、夹伤、电机过热、结构损坏或电池事故。
- 域随机化与执行器模型只是近似，不能覆盖装配误差、地面摩擦、线缆、温度和传感器故障。
- “可训练/可导出”不等于策略在指定硬件上稳定；上游任务演示也不是本机复现证据。
- 代码与 3D 模型许可证不同，商用、再分发和衍生硬件需要分别审查。
- 云端训练会外发代码、配置、日志和可能的模型工件。

## 补充建议

1. 固定机器人 URDF/XML、固件、观测顺序、控制频率和 ONNX 哈希。
2. 在仿真中加入传感器丢帧、饱和、延迟、摩擦极值与策略切换压力测试。
3. 真机先悬挂或使用保护架，配置机械限位、软件限幅、急停和温度/电流监控。
4. 逐项比较仿真与真机观测分布，不只看最终动作是否“像演示”。
5. 分开保存代码 Apache-2.0 与 3D 模型 CC BY-SA-NC 的合规清单。

## 参考资料

- 仓库与 README：https://github.com/pollen-robotics/microduck_rl
- Microduck 项目页：https://pollen-robotics.com/microduck
- 训练/导出脚本：https://github.com/pollen-robotics/microduck_rl/tree/develop/scripts
- 执行器实现：https://github.com/pollen-robotics/microduck_rl/tree/develop/src/mjlab_microduck/actuator
- 许可证：https://github.com/pollen-robotics/microduck_rl/blob/develop/LICENSE
