<!-- markdownlint-disable MD013 -->

# MuJoCo

## 定位

MuJoCo（Multi-Joint dynamics with Contact）是 Google DeepMind 维护的物理引擎，为机器人控制、强化学习、生物力学等提供关节、接触和可变形体仿真。它计算环境动力学，控制器、奖励函数、训练算法与真实设备验证由使用者提供。

- 上游：[google-deepmind/mujoco](https://github.com/google-deepmind/mujoco)，仓库 ID `400501136`。
- 2026-11-10：16,878 stars / 1,991 forks / 305 open issues（含 PR）；综合 daily +579。
- 稳定发行 [4.0.0](https://github.com/google-deepmind/mujoco/releases/tag/4.0.0)，UTC 2026-11-06；PyPI 同版，Python ≥3.11。本页按主线 `70dede9373277de3a781428e4ce3a428a34abc8b` 静态核读，其中含尚未发行的修复。

## 用法

1. 新环境可安装 `python -m pip install "mujoco==4.0.0"`，或用官方预编译包；先用 Studio / simulate 与小模型检查几何、关节、重力和接触。
2. 用 MJCF 或程序化接口定义模型，编译得到 `mjModel`，为每个状态创建 `mjData`，设置控制后调用 `mj_step`；训练时另接观测、奖励和环境包装。
3. 4.0 将 Python 发行拆成 `mujoco-core`、`mujoco-studio` 与默认安装两者的 `mujoco`。旧环境需照 changelog 处理迁移，避免升级器删除已移交给 core 的文件。
4. 固定 release、模型、积分器、时间步长、求解器与种子；CPU、MJX / GPU 与浏览器 WASM 分开验收。

本轮未安装、运行或修改用户仿真环境；以上入口依据固定 SHA README、overview 与 changelog。

## 原理

编译器将高层模型整理为预分配、交叉索引的低层结构；`mjModel` 保存模型，`mjData` 保存状态和中间量。接触采用可调软约束与凸优化思路；渲染网格与碰撞凸包须区分。

4.0 的推测接触扩展运动包围体，以保守推进估计碰撞时间，排除被遮挡候选，再构造有效接触距离供求解器处理。它有助于减少高速凸几何体穿过薄障碍，但运动外推仅使用步前速度、忽略加速度，不能任意放大时间步长。

## 价值

- 提供可记录、可重复的动力学环境，适合策略采样、控制算法比较和参数敏感性研究。
- 4.0 弹塑性与推测接触扩展可研究场景；材料适用性和精度仍需独立验证。
- 模型 / 状态分离便于并行采样，收益需按后端、模型与线程条件测量。

## 风险边界

- **稳定版与主线修复分开**：主线 Upcoming 节记录 4.0.0 引入的稀疏 Cholesky 错误，可导致 Newton 求解器错误加速度、慢收敛或发散；另有 USD 插件加载与圆柱接触修复。不能写成稳定 4.0.0 已解决。
- **迁移改变结果**：4.0 改动 tendon sidesite 语义、RK4 姿态精度，并用 flex 取代旧 cable / composite；旧模型能加载不等于轨迹一致。
- **仿真与实验不同**：摩擦、软接触、驱动器、传感器和凸分解都会影响策略；渲染逼真不证明 sim-to-real 成功。
- **许可分资产**：源码 Apache-2.0，`doc/` 文档、图片、视频 CC BY 4.0；第三方模型与数据另核。README 明确其不是 Google 官方支持产品。

## 补充建议

先以落球、薄障碍高速碰撞和单关节驱动建立参考，扫描步长与求解器并保存能量 / 接触 / 轨迹诊断。有稀疏约束 Jacobian 的 4.0.0 场景应优先核已知问题和后续补丁；记录模型、依赖哈希，真实控制前另做设备标定和小范围实验。

## 参考资料

- [固定 SHA README：安装与资产许可](https://github.com/google-deepmind/mujoco/blob/70dede9373277de3a781428e4ce3a428a34abc8b/README.md)
- [模型、状态和软接触](https://github.com/google-deepmind/mujoco/blob/70dede9373277de3a781428e4ce3a428a34abc8b/doc/overview.rst)
- [推测接触与加速度限制](https://github.com/google-deepmind/mujoco/blob/70dede9373277de3a781428e4ce3a428a34abc8b/doc/computation/speculative.rst)
- [4.0 迁移与 Upcoming 修复](https://github.com/google-deepmind/mujoco/blob/70dede9373277de3a781428e4ce3a428a34abc8b/doc/changelog.rst)
- [PyPI 版本元数据](https://pypi.org/pypi/mujoco/json)
