<!-- markdownlint-disable MD013 -->

# ASPIRE

> 更新：2026-10-19（Asia/Shanghai）。分类：Agent 框架与技能生态。上游 `NVlabs/ASPIRE`；本文基于官方榜单、认证 API 与文档 / 源码静态核验，未安装运行。源码快照 `fa00f0ef2bc1`；Release 与主分支行为分别说明。热度见[当日官方榜单](https://github.com/trending/python?since=daily)。

## 定位

NVIDIA 等机构的机器人技能发现研究工程：让 coding agent 在环境反馈中编写、调试和积累 sensorimotor skills，用可复用程序 / 技能库表达学习结果。当前覆盖 LIBERO-Pro、Robosuite、BEHAVIOR-1K，并有真实机器人演示入口。[来源 1](https://github.com/NVlabs/ASPIRE/blob/fa00f0ef2bc1d91d594b9aa502c22133c9f538f7/README.md)

官方 Python Trending 约 +99 当日 stars；API 为 545 / 40 / 14（stars / forks / open issues）。README 称 2026-10 的 ASPIRE v1.0 已发布，但认证 API 未列 GitHub Release / tag，不能把新闻中的 v1.0 当作可直接检出的 tag。[来源 1](https://github.com/NVlabs/ASPIRE/blob/fa00f0ef2bc1d91d594b9aa502c22133c9f538f7/README.md)[来源 2](https://api.github.com/repos/NVlabs/ASPIRE)

## 用法

先选模拟环境和具体任务，再读对应 runbook。LIBERO-Pro bootstrap 建立冻结环境与 pinned submodules；host 文档另要求 NVIDIA driver、uv、经授权的 SAM3 权重和相应凭据，BEHAVIOR 有额外 CUDA / Isaac / 数据集条件。[来源 3](https://github.com/NVlabs/ASPIRE/blob/fa00f0ef2bc1d91d594b9aa502c22133c9f538f7/docs/host-setup.md)[来源 4](https://github.com/NVlabs/ASPIRE/blob/fa00f0ef2bc1d91d594b9aa502c22133c9f538f7/docs/libero-pro.md)

```bash
# 上游的结构检查入口；需先完成对应环境配置
cap-harness doctor --providers sam3,pyroki,curobo --unit
```

首轮只做一个有记录的模拟任务，保存任务 ID、seed、init_mode、程序、模型、输出与成本；不将模拟 agent 接到实体硬件。本轮未执行 bootstrap、模拟或机器人操作。

## 原理

Agent 利用感知 / 运动 provider API 写 Python，反复运行、读取成功或失败反馈、修订程序，再将可复用策略收进技能库；另有 evolutionary search 路径。这里的“训练”主要指技能程序改进，不等同于每轮更新神经网络权重。[来源 1](https://github.com/NVlabs/ASPIRE/blob/fa00f0ef2bc1d91d594b9aa502c22133c9f538f7/README.md)[来源 5](https://github.com/NVlabs/ASPIRE/blob/fa00f0ef2bc1d91d594b9aa502c22133c9f538f7/docs/api-reference.md)

LIBERO-Pro 文档区分 saved 与 seeded 初始化：saved 默认从有限状态集按 seed 取模，较大 seed 会复用状态；结构 smoke / nightly 检查验证 reset、schema、动作和恢复，明确不等于任务成功率基准。[来源 4](https://github.com/NVlabs/ASPIRE/blob/fa00f0ef2bc1d91d594b9aa502c22133c9f538f7/docs/libero-pro.md)

## 价值

适合研究“程序化技能库如何随试错成长”，也提供比较模型策略、工具调用成本和任务成功率的工程入口。输出程序与运行产物有助于复查失败机制；其价值需在固定任务和成本口径下评估，不能由短演示外推通用机器人能力。

## 风险边界

- README 的 99% / SOTA 等为作者选定任务、模型和版本的报告，本轮没有复现实验、统计置信区间或检查全部原始轨迹。[来源 1](https://github.com/NVlabs/ASPIRE/blob/fa00f0ef2bc1d91d594b9aa502c22133c9f538f7/README.md)
- 上游明确：模型生成 Python 有完整 import 权限，trial / watchdog 不是安全 sandbox。需独立主机权限、网络与挂载约束，模拟和真实机器人授权必须分开。[来源 1](https://github.com/NVlabs/ASPIRE/blob/fa00f0ef2bc1d91d594b9aa502c22133c9f538f7/README.md)
- 多个 seed 不保证独立场景；历史 seeded 初始化问题、有限 saved states 与 GPU 渲染设备选择会影响结果解释。[来源 4](https://github.com/NVlabs/ASPIRE/blob/fa00f0ef2bc1d91d594b9aa502c22133c9f538f7/docs/libero-pro.md)
- 实体演示 recipe 可能来自已有 session 的蒸馏，不是新增真实机器人验证；动作完成、物理成功和安全完成要逐项检查。
- 自有代码 Apache-2.0，第三方组件、模型与数据另循 NOTICE 和许可索引；SAM3 需先获得访问权。[来源 3](https://github.com/NVlabs/ASPIRE/blob/fa00f0ef2bc1d91d594b9aa502c22133c9f538f7/docs/host-setup.md)[来源 6](https://github.com/NVlabs/ASPIRE/blob/fa00f0ef2bc1d91d594b9aa502c22133c9f538f7/NOTICE)

## 补充建议

先建立“单任务 / 单 seed / 单模型”可复现基线，再扩大 seed 与任务。报告同时列 task success、恢复次数、模型成本、仿真时间和程序版本；区分结构检查、选定样例、完整基准与实体实验。尤其检查 saved / seeded 和渲染 GPU，不以 exit code 代替物理成功。

## 参考资料

1. [README 与作者结果](https://github.com/NVlabs/ASPIRE/blob/fa00f0ef2bc1d91d594b9aa502c22133c9f538f7/README.md)
2. [仓库 API](https://api.github.com/repos/NVlabs/ASPIRE)
3. [主机准备](https://github.com/NVlabs/ASPIRE/blob/fa00f0ef2bc1d91d594b9aa502c22133c9f538f7/docs/host-setup.md)
4. [LIBERO-Pro 配置与证据边界](https://github.com/NVlabs/ASPIRE/blob/fa00f0ef2bc1d91d594b9aa502c22133c9f538f7/docs/libero-pro.md)
5. [Provider API](https://github.com/NVlabs/ASPIRE/blob/fa00f0ef2bc1d91d594b9aa502c22133c9f538f7/docs/api-reference.md)
6. [NOTICE](https://github.com/NVlabs/ASPIRE/blob/fa00f0ef2bc1d91d594b9aa502c22133c9f538f7/NOTICE)
7. [LICENSE](https://github.com/NVlabs/ASPIRE/blob/fa00f0ef2bc1d91d594b9aa502c22133c9f538f7/LICENSE)
