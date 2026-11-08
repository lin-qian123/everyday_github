<!-- markdownlint-disable MD013 -->

# Colab CLI（googlecolab/google-colab-cli）中文解读

> 上游：[googlecolab/google-colab-cli](https://github.com/googlecolab/google-colab-cli) · 分类：模型、训练与推理基础设施 · 核验：2026-11-09，仓库 ID 1213901015，主线 SHA `d2d97794941723ab806c0f3642416691a951ec7d`。本页为文档与抽样源码静态核读，未安装运行、登录或调用模型 / 云资源。

## 定位

Google Colab 的官方终端接口，可申请 CPU / GPU / TPU runtime，远程执行本地 Python / notebook，管理文件并接入自动化。适合把已有终端工作流延伸到 Colab；不是本地 GPU，也不同于面向 notebook 的 Colab MCP Server。

## 用法

主线要求 Python 3.12+，README 明确目前支持 Linux / macOS，不支持 Windows。PyPI 快照为 0.7.5，GitHub releases 列表为空；发布包与下列主线文档需分别核对，可先用 `pip install google-colab-cli==0.7.5` 并检查 `colab --help`。

完成账户认证后，典型流程是 `colab new -s test` → `colab exec -s test -f script.py` → 按需 `colab download` → `colab stop -s test`。这些操作会创建真实云资源并上传代码，本轮仅核读，没有执行。

## 原理

通过 Colab API 分配 endpoint，维护本地 session 状态，再经远端 Jupyter kernel / Contents API 与 WebSocket 执行代码、访问文件。默认认证策略为 ADC；可选 OAuth2，主线将 OAuth token 写入 OS keyring，成功迁移后删除旧明文 token 文件。

`colab run` 将创建、执行和清理组合起来；主线 `--timeout` 默认 30 秒，是无输出的空闲超时，0 为不限。结束后进入 finally 清理，`--keep` 会保留 VM。

## 价值

可复用脚本、依赖和 CLI 日志组织小型加速计算与教学实验，减少在浏览器逐格操作。显式 session 名与下载步骤也便于把云任务纳入可复现流程。

## 风险边界

- GPU / 高内存可用性受账号权益、配额和后端资源约束；视频的“Free GPU”标题不保证任何硬件免费或随时可用。计算单位、订阅与任务总费用要独立核对。
- OAuth scopes 包含 cloud-platform、colaboratory 和 drive.file 等；`drivemount` / `auth` 又会扩展 VM 能访问的数据。只向受信脚本开放必要资料。
- OAuth token 的 keyring 与 `sessions.json` 中的 runtime token 是不同状态；会话文件、历史代码和输出也需控制权限、备份与保留期。
- finally 是尽力清理，不能保证断网、强杀或后端失败后没有存活资源；完成后仍核 `colab sessions` 和用量。默认静默超时可能终止长时间不打印的任务，VM 清理前先保存制品。
- 主线代码没有在 `run` 中实现通用“所有输出文件自动下载”；重要文件应显式下载或可靠持久化。根代码 Apache-2.0，服务使用另受 Colab 条款与隐私政策约束。

## 补充建议

以无敏感数据的 CPU 短任务验证认证、返回码、超时、下载和清理，再扩大到 GPU。固定包 / 依赖和硬件，保存输入与产物哈希；记录运行总耗时与 compute-unit 变化。自动化中明确 session、预算、checkpoint 和失败后的资源核查。

## 参考资料

- [上游](https://github.com/googlecolab/google-colab-cli)、[仓库 API](https://api.github.com/repos/googlecolab/google-colab-cli)、[发行列表](https://github.com/googlecolab/google-colab-cli/releases)、[PyPI JSON](https://pypi.org/pypi/google-colab-cli/json)。
- [README](https://github.com/googlecolab/google-colab-cli/blob/d2d97794941723ab806c0f3642416691a951ec7d/README.md)、[Python 与依赖](https://github.com/googlecolab/google-colab-cli/blob/d2d97794941723ab806c0f3642416691a951ec7d/pyproject.toml)、[认证实现](https://github.com/googlecolab/google-colab-cli/blob/d2d97794941723ab806c0f3642416691a951ec7d/src/colab_cli/auth.py)、[session 存储](https://github.com/googlecolab/google-colab-cli/blob/d2d97794941723ab806c0f3642416691a951ec7d/src/colab_cli/state.py)。
- [run 设计及超时变更](https://github.com/googlecolab/google-colab-cli/blob/d2d97794941723ab806c0f3642416691a951ec7d/docs/05_run_command.md)、[run 实现与清理](https://github.com/googlecolab/google-colab-cli/blob/d2d97794941723ab806c0f3642416691a951ec7d/src/colab_cli/commands/run.py)。
