<!-- markdownlint-disable MD013 -->

# UniMate（Friedrich-M/UniMate）

> 上游仓库：<https://github.com/Friedrich-M/UniMate> · 归类：语音、视频与多模态 · 本页基于 2026-10-02 的 GitHub API、README、论文、Hugging Face model / dataset cards 与 LICENSE 静态整理，未下载 checkpoint、数据或复跑训练、推理和用户研究。

- 抓取快照：1,055 stars、100 forks、9 open issues。
- 热度信号：GitHub 综合 / Python Trending 抓取时约 +225 当日 stars。
- 版本与许可：代码仓库 MIT、无 GitHub Release / tag；Hugging Face 权重为 CC BY-NC 4.0，UniML3D 数据集标为按来源混合许可。

## 定位

UniMate 是 SIGGRAPH Asia 2026 的文本到骨骼动画研究项目，目标是用一个模型为双足、四足、鸟类、海洋生物、昆虫、蛇形和关节刚体等不同拓扑生成动作，而不是为每套 skeleton 单独训练。仓库同时发布训练 / 推理代码、UniML3D 处理管线、预览 checkpoint 与交互样例。

## 用法

上游建议建立 Python 3.10 环境并安装 `requirements.txt`；训练通过 Accelerate 读取 JSON config，推理从实验目录的 config、归一化统计和 checkpoint 出发，按目标 object type 与文本 prompt 生成 motion feature 和 MP4 预览。要驱动原始 mesh，还需数据处理管线中的 rig 条件和后续 GLB / FBX 导出步骤。

## 原理

UniML3D 汇集 13,006 条文本配对 motion sequence，并把不同 skeleton canonicalize。模型以 flow matching 学习关节 × 时间 token 的运动场；发布配置比较 graph-factorized spatial / temporal attention 与 full attention，并用拓扑增广、骨长扰动、mask、旋转与平滑损失及 classifier-free guidance 支持异构骨架。in-betweening、局部 motion editing 与长序列 expansion 通过固定一部分已知信号再采样其余部分实现。

## 价值

统一拓扑条件让游戏、动画、机器人原型和 3D 资产批处理有机会减少逐 rig retarget / 重训成本；公开代码、数据处理脚本、条件输入和失败说明也便于研究者检查跨骨架泛化，而不只观看精选视频。

## 风险边界

- README 明确它只是 early step，许多 motion 与 skeleton 仍会失败；“实时”“任意 skeleton”是研究目标与作者描述，不是本轮复现实验结论。
- 新的 out-of-distribution rig 官方预处理管线仍列在 TODO；当前推理依赖训练数据目录中的条件特征，不能把 demo 直接等同于任意生产资产输入。
- Objaverse 侧存在倒置 rest pose、错误朝向和拼接动作等坏数据，上游也记录其可能令训练不稳定或崩溃。
- 代码 MIT 不覆盖全部制品：权重是 CC BY-NC 4.0，数据集按 Mixamo / Objaverse / Truebones 等来源分别授权，Truebones 动作本身不能由项目再分发。
- caption、joint annotation 与数据处理含机器生成步骤，语义、解剖结构和文化偏差仍需人工抽查。
- 大规模训练、模型下载、T5 文本编码与渲染有显著 GPU、存储和供应链成本；生成动作还可能出现碰撞、穿模、不稳定或不适合实际控制系统。

## 补充建议

先锁定仓库 commit、权重 revision、数据来源与许可证清单，只在研究 / 非商业边界明确时使用预览 checkpoint。建立覆盖已见与 OOD rig 的小型金标集，量化 foot sliding、关节极限、碰撞、文本一致性、骨长保持与人工观感；输出进引擎前做 retarget、物理约束和逐段播放验收。商业使用应重新训练或取得权重 / 数据授权，不能只依据代码 MIT。

## 参考资料

- [GitHub 仓库](https://github.com/Friedrich-M/UniMate)
- [GitHub REST API](https://api.github.com/repos/Friedrich-M/UniMate)
- [README 与运行说明](https://github.com/Friedrich-M/UniMate/blob/main/README.md)
- [项目页与交互演示](https://linzhanmou.com/unimate/)
- [论文 arXiv:2609.05415](https://arxiv.org/abs/2609.05415)
- [Hugging Face 权重](https://huggingface.co/Linzhan/UniMate)
- [UniML3D 数据集与许可](https://huggingface.co/datasets/Linzhan/UniML3D)
- [数据处理管线](https://github.com/Friedrich-M/UniMate/blob/main/data_process/README.md)
- [代码 LICENSE](https://github.com/Friedrich-M/UniMate/blob/main/LICENSE)
