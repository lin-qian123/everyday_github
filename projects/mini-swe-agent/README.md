<!-- markdownlint-disable MD013 -->

# mini-swe-agent（SWE-agent/mini-swe-agent）中文解读

> 上游：[SWE-agent/mini-swe-agent](https://github.com/SWE-agent/mini-swe-agent) · 分类：Coding Agents 与终端助手 · 核验：2026-11-09，仓库 ID 1010318950，主线 SHA `04d809ceab9df28f9adaed044884180159172930`。本页为文档与抽样源码静态核读，未安装运行、登录或调用模型 / 云资源。

## 定位

SWE-agent 团队提供的极简软件工程 agent：主要把模型、bash 执行环境与线性消息历史接成循环，适合研究基线、轨迹分析和受控编码任务。当前为 v2，稳定发行 / PyPI 2.4.6；旧 v1 使用者需读迁移说明。

## 用法

需要 Python 3.10+，可 `pip install mini-swe-agent==2.4.6` 后运行 `mini`，初次配置模型与凭据。只在可丢弃项目副本中试用，先检查 `mini --help`、配置及 trajectory 输出位置。

默认入口选 local 环境，默认 mini.yaml 为 `mode: confirm`、`cost_limit: 3.`、`step_limit: 0`；`--yolo` 会去掉确认。新增 `-c` 参数会替代默认配置列表，需显式带上 `mini.yaml` 才能保留它的设置。

## 原理

模型产生 bash action，环境执行并把观察附加到历史；每个命令在新子进程 / subshell 中执行，因此 `cd` 和临时环境变量不会自动延续到下一步。LocalEnvironment 继承宿主环境并调用 subprocess，主线在 POSIX 超时时清理整个进程组。

Docker / Podman、Singularity 等是可替换执行后端；只有约百行的 agent class 不代表完整程序、依赖或隔离实现只有百行。

## 价值

控制流小、轨迹直接，方便比较模型能力、prompt 与执行环境，也便于调试失败样本或构造微调 / 强化学习数据。它减少自定义工具接口带来的变量，但 shell 本身仍能完成复杂操作。

## 风险边界

- 默认 local 的文件、网络与子进程权限来自当前用户，并会继承环境变量；confirm 和 Python virtualenv 都不是 OS sandbox。容器也需审挂载、网络、用户与 secret。
- `step_limit: 0` 不限制步数；成本上限依赖模型适配器计费信息，不等于服务端硬预算。2.4.6 修复了已计费但解析失败的调用计数，仍需独立检查账单。
- README 的 >74% SWE-bench Verified 是作者基准声明，受模型、数据集、步数 / 费用、环境及 harness 影响；不代表任意模型或真实项目成功率。
- 官方文档仍链接 2025-11-19 的 Gemini 3 Pro 成绩帖，作者随后更正迭代长度比较；这不是 2026-11-09 新成绩，未据此做最新模型推荐。
- 轨迹可能含代码、工具输出及敏感内容；本地保存路径和云模型数据政策需分别核。主线排除了 LiteLLM 1.82.7 / 1.82.8，安装仍应固定审计后的依赖。代码 MIT。

## 补充建议

用固定任务、模型、环境和预算比较成功率、回归测试、重试及总费用，保留完整 trajectory。先验证确认、拒绝、超时、limits 和保存路径，再尝试无人值守；只把真实测试通过的补丁交给人工审阅，不凭 agent 自报完成合并。

## 参考资料

- [上游](https://github.com/SWE-agent/mini-swe-agent)、[仓库 API](https://api.github.com/repos/SWE-agent/mini-swe-agent)、[v2.4.6](https://github.com/SWE-agent/mini-swe-agent/releases/tag/v2.4.6)、[PyPI JSON](https://pypi.org/pypi/mini-swe-agent/json)。
- [README 与能力声明](https://github.com/SWE-agent/mini-swe-agent/blob/04d809ceab9df28f9adaed044884180159172930/README.md)、[quickstart](https://github.com/SWE-agent/mini-swe-agent/blob/04d809ceab9df28f9adaed044884180159172930/docs/quickstart.md)、[依赖与 Python](https://github.com/SWE-agent/mini-swe-agent/blob/04d809ceab9df28f9adaed044884180159172930/pyproject.toml)。
- [CLI 入口](https://github.com/SWE-agent/mini-swe-agent/blob/04d809ceab9df28f9adaed044884180159172930/src/minisweagent/run/mini.py)、[默认配置](https://github.com/SWE-agent/mini-swe-agent/blob/04d809ceab9df28f9adaed044884180159172930/src/minisweagent/config/mini.yaml)、[交互确认](https://github.com/SWE-agent/mini-swe-agent/blob/04d809ceab9df28f9adaed044884180159172930/src/minisweagent/agents/interactive.py)、[本地执行](https://github.com/SWE-agent/mini-swe-agent/blob/04d809ceab9df28f9adaed044884180159172930/src/minisweagent/environments/local.py)、[LICENSE](https://github.com/SWE-agent/mini-swe-agent/blob/04d809ceab9df28f9adaed044884180159172930/LICENSE.md)。
