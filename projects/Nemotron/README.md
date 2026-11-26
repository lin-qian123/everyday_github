<!-- markdownlint-disable MD013 -->

# Nemotron：模型家族的训练配方、步骤与部署资料入口

- 上游：[NVIDIA-NeMo/Nemotron](https://github.com/NVIDIA-NeMo/Nemotron)，repository ID `1069235905`；2026-11-27 新建档案。
- 快照：2,392 stars / 504 forks / 98 open issues（累计，含 PR）；Jupyter Notebook daily +2。这是有界语言榜样本，不将低增星解释成全平台热门。
- main SHA `4bdc0d7bcf304675232955208393273b2fdd0e76`，2026-11-23，更新 Parse 分阶段 uv / 容器执行。最近稳定发行 v0.2.0 为 10-15，tag SHA `ef8c46d439c6853fb454430e3d58725435894ca7`；本页主线行为不倒推为 tag 已有。
- 范围：README、Python 元数据、Steps 与 Parse 文档、阶段依赖及插件技能文本局部静态核读；未安装、加载模型、提交训练、调用云服务或复现性能。

## 定位

这是 NVIDIA Nemotron 模型家族的开发资料仓库，聚合训练 recipes、可组合 steps、部署 cookbooks、数据与应用案例。它不是单一模型权重，也不是所有 Nemotron 型号共享的一组硬件要求。

`src/nemotron/steps/` 用统一契约描述工作单元；`recipes/` 给出训练流程；`usage-cookbook/` 面向已有模型的部署；`use-case-examples/` 面向应用。部分指南是其他 NVIDIA 仓库的集成地图，需要跟随各自实现和版本。

## 用法

先固定本页 SHA，按“只查目录、运行单步、训练、部署”选择入口。README badge / Steps 入门页写 Python 3.10+，但当前 `pyproject.toml` 实际要求 `>=3.11,<3.14`；Parse 控制器示例选择 Python 3.12，阶段环境另行选择版本。

在独立 checkout 中准备依赖后的目录查询示意如下，未执行；其中 `uv sync` 会联网安装依赖：

```bash
uv sync --locked --python 3.12
uv run nemotron steps list --json
uv run nemotron steps show sft/automodel --json
```

Steps 的 list / show 文档定位为元数据查询，不需要集群或 GPU；不能由此推定训练无需 GPU。Parse 的 `nemotron parse sft --dry-run` 文档称只打印配置，不安装阶段依赖或开始训练；准备控制器环境本身仍是安装操作。

仓库另提供 Claude Code 的 `nemotron-customize` 插件，要求从仓库根目录使用，用于规划步骤图、检查 artifact 连线和生成配置。插件成功产出 YAML 仍需检查数据、资源、执行 profile 和启动命令，本轮没有安装该插件。

## 原理

每个 step 声明 consumes / produces artifact 类型、参数、命名配置和运行规格。以数据生成、格式转换、训练、checkpoint 转换和评估串起流程；类型相容是连线检查的一部分，并不自动证明数据内容、训练目标和评估语义一致。

执行目标由 `env.toml` profile 描述本地、Docker、Slurm 或云端资源。省略远程参数可在本机运行，`--run` / `--batch` 则依所选执行器附着运行或提交；不是仅生成“建议”。

最新 Parse 文档用牙科文档参考任务展示 data → SFT → RLVR → held-out eval，并保存数据、基础 / SFT / RLVR 模型的 lineage。它区分通用训练骨架和牙科专属数据、奖励、评估；不把示例任务效果外推为通用文档解析能力。

## 价值

这个入口的工程价值在于可以追踪数据、训练配置、模型转换和评估之间的依赖，而不只获取权重和一句启动命令。分阶段项目、锁文件、固定镜像摘要与 artifact 身份给复现提供了明确检查点。

Parse 文档还直接披露了显存失败、尚待验证的资源建议和恢复限制。这些具体边界比 README 的“可复现”“高效”概括更适合作为选型依据；本轮没有生成新的训练结果。

## 风险边界

| 议题 | 已核事实与边界 |
| --- | --- |
| 版本身份 | 主线仍标 package version 0.2.0，但 SHA 晚于 v0.2.0；版本字符串相同不能证明配方、依赖或制品相同。 |
| 许可差异 | 根 LICENSE / README / API 为 Apache-2.0，`pyproject.toml` 却写 MIT 和 MIT classifier。记录这一元数据矛盾，复用前按实际文件和目标组件核对；模型、数据也有各自协议。README 数据表已列出 NVIDIA Data Agreement、CC-BY、ODC-BY 等不同条件。 |
| 锁定范围 | Parse 本地和 isolated 数据 / RLVR 容器应用完整阶段锁文件；SFT / eval 容器继承镜像框架栈，再解析额外包，不能笼统写成所有路径都严格使用完整 lock。 |
| 硬件与 tiny | Parse 当前为单 controller / 单 GPU 训练评估；默认 batch=4 曾超出 RTX A6000 的 48 GB。文档建议至少 80 GB，但明确尚待当前默认完整验证，非实测最低值。tiny 减少更新数，仍保留默认 SFT batch，不保证低显存可跑。 |
| 存储与恢复 | 三种不同 amd64 容器镜像合计约 88 GB 是作者给出的 layer sharing 前估算，不是整任务磁盘预算。stage resume / optimizer-state resume 未实现；checkpoint、缓存、输出和持久挂载另计。 |
| 评估边界 | 牙科参考结果用固定 held-out 页和采样协议比较 base / SFT / RLVR；sampled pass@1 与 greedy monitor accuracy 不同，内容正确不保证框位置、类别与全部 markup 正确。 |
| 数据与执行权限 | SDG、云 executor、模型 Hub、实验记录和 Claude Code 各有数据 / 凭据出口。容器 mount 和 artifact 验证不替代集群权限、预算及领域人工核验。 |

## 补充建议

1. 分别固定仓库 SHA、step / recipe、模型 revision、阶段 lock、镜像 digest 与 profile；先对照 `list/show` 检查参数与 artifact。
2. 把控制器安装、配置 dry-run、阶段启动、完整训练、重载和 held-out 评估分别验收。tiny 只用于有限冒烟检查，先重新估算 batch / 输入长度 / 显存。
3. 复用 Parse 时替换牙科数据、奖励和独立测试集；保留图像哈希、模型 lineage 与生成协议，比较匹配条件下的提升。
4. 先核路径挂载、失败输出和恢复策略，再安排计算；资源建议和作者实验都不当作本地已验证结果。

## 参考资料

- [仓库 API](https://api.github.com/repos/NVIDIA-NeMo/Nemotron)、[v0.2.0 发行](https://github.com/NVIDIA-NeMo/Nemotron/releases/tag/v0.2.0)、[固定 README](https://raw.githubusercontent.com/NVIDIA-NeMo/Nemotron/4bdc0d7bcf304675232955208393273b2fdd0e76/README.md)。
- [Python 与许可元数据](https://raw.githubusercontent.com/NVIDIA-NeMo/Nemotron/4bdc0d7bcf304675232955208393273b2fdd0e76/pyproject.toml)、[根 LICENSE](https://raw.githubusercontent.com/NVIDIA-NeMo/Nemotron/4bdc0d7bcf304675232955208393273b2fdd0e76/LICENSE)、[Steps 入门](https://raw.githubusercontent.com/NVIDIA-NeMo/Nemotron/4bdc0d7bcf304675232955208393273b2fdd0e76/docs/steps/getting-started.md)、[Steps / 配置 / profile](https://raw.githubusercontent.com/NVIDIA-NeMo/Nemotron/4bdc0d7bcf304675232955208393273b2fdd0e76/docs/steps/basics.md)。
- [Parse 环境与依赖](https://raw.githubusercontent.com/NVIDIA-NeMo/Nemotron/4bdc0d7bcf304675232955208393273b2fdd0e76/docs/nemotron/parse/environments.md)、[Parse 资源 / dry-run / 挂载](https://raw.githubusercontent.com/NVIDIA-NeMo/Nemotron/4bdc0d7bcf304675232955208393273b2fdd0e76/docs/nemotron/parse/runtime.md)、[Parse 训练 / lineage / 评估协议](https://raw.githubusercontent.com/NVIDIA-NeMo/Nemotron/4bdc0d7bcf304675232955208393273b2fdd0e76/docs/nemotron/parse/workflow.md)、[插件技能说明](https://raw.githubusercontent.com/NVIDIA-NeMo/Nemotron/4bdc0d7bcf304675232955208393273b2fdd0e76/skills/nemotron-customize/SKILL.md)。
