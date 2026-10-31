<!-- markdownlint-disable MD013 -->

# pr-agent

- 上游：[The-PR-Agent/pr-agent](https://github.com/The-PR-Agent/pr-agent)；分类：Coding Agents 与终端助手。
- 核读：2026-11-01（Asia/Shanghai）；固定主线 `7bb7a68b451097d79dbc1c470e849b78dcf07eed`。
- [仓库 API](https://api.github.com/repos/The-PR-Agent/pr-agent) 快照：13,845 stars / 2,031 forks / 47 open issues（含 PR）；发行首项 [v0.49.0](https://github.com/The-PR-Agent/pr-agent/releases/tag/v0.49.0)，2026-10-25 UTC。发行与主线分别看。
- 证据：上游文档及指定文件静态核读；本轮未安装运行、调用模型或复现作者实验。

## 定位

社区维护的 AI PR 审查工具，提供 review、describe、improve、ask 等入口，可用 CLI、Actions、webhook 或自托管服务接入多个 Git 平台。当前 README 明确它是 Qodo 的历史开源项目，与 Qodo 面向开源项目的产品方案不同。官方 Python daily 榜本轮显示 +118 stars。

## 用法

需要 Python ≥3.12。首测可选 plain-diff 模式，只向本地文件输出审查结果：

```bash
python -m pip install 'pr-agent[github]==0.49.0'
git diff --no-ext-diff > change.diff
pr-agent --diff-file change.diff --output review.md --json-output review.json review
```

预先按所选 provider 配置模型与凭证；默认模型为 `gpt-6.1-sol`，fallback 为 `gpt-6-luna`，需有相应可用权限。这条命令仍会把 diff 交给配置的模型，不能把“本地 diff”理解为离线模型。

接入真实 PR 后，`pr-agent --pr_url <PR_URL> review` 默认会发布结果；先限定测试仓库、token 权限、触发者和输出配置。`pr-agent doctor` 会检查并 ping 模型，也不是无网络 dry run。0.34.2+ Docker namespace 已迁到 `pragent/pr-agent`，旧 `codiumai` 镜像不能当作当前发行。

## 原理

Git provider 取得变更、上下文和讨论，压缩 / 分块适配模型预算，经 LiteLLM 调用模型，解析结构化建议后映射到 diff 行并交给输出端。配置来自宿主、环境、组织 / 仓库及命令参数，敏感键有 host-only 限制。plain-diff 切换到本地 provider，仍开启输出以写 stdout / 文件；真实 PR provider 则可产生评论、标签等副作用。

## 价值

提供可定制提示、模型和 Git 平台的审查基础设施；JSON 输出便于统计误报、漏报与未覆盖文件。适合把机械检查与人工审查衔接起来，质量应按已标注缺陷和维护者采纳率评估，不能由评论数量或 stars 推定。

## 风险边界

- `publish_output`、`publish_output_progress` 默认 true；PR 中代码、评论、上下文和技能文本都应视为不可信输入，模型建议仍需测试与人工判断。
- 自托管的隐私文档只明确“用户与所选模型提供方之间”的关系，未承诺模型侧不留存。密钥、diff、日志、外部输出 sink 和可选 observability 要分别检查。
- OpenTelemetry 默认关闭，PR URL / error details 附加字段也默认 false；这不关闭正常模型请求或 Git API 操作。
- v0.49.0 的 polling 仓库 allowlist 默认空，意味着不处理通知；宿主需显式设置。发行同时列出多项配置、路径和输出加固，本轮只核文本与源码，没有复现安全修复。
- 根许可 MIT；README 的“一次调用 / 约 30 秒”是简化描述，当前重试、fallback、分块路径可能增加调用与费用。

## 补充建议

以一组脱敏 diff 和独立缺陷标签比较模型，单列被过滤 / 截断文件与失败重试。首轮本地输出，确认结果和费用后再打开真实 PR 评论；Actions 使用固定发行 SHA、最小权限，避免把外部 PR 内容执行进含 secrets 的作业。

## 参考资料

- [固定 README / 项目身份与接入](https://github.com/The-PR-Agent/pr-agent/blob/7bb7a68b451097d79dbc1c470e849b78dcf07eed/README.md)。
- [plain-diff 与输出参数](https://github.com/The-PR-Agent/pr-agent/blob/7bb7a68b451097d79dbc1c470e849b78dcf07eed/pr_agent/cli.py)。
- [默认模型、发布、polling 与 OTEL](https://github.com/The-PR-Agent/pr-agent/blob/7bb7a68b451097d79dbc1c470e849b78dcf07eed/pr_agent/settings/configuration.toml)。
- [遥测初始化](https://github.com/The-PR-Agent/pr-agent/blob/7bb7a68b451097d79dbc1c470e849b78dcf07eed/pr_agent/telemetry/config.py)。
- [宿主配置边界](https://github.com/The-PR-Agent/pr-agent/blob/7bb7a68b451097d79dbc1c470e849b78dcf07eed/pr_agent/config_security.py)。
- [自托管数据边界](https://github.com/The-PR-Agent/pr-agent/blob/7bb7a68b451097d79dbc1c470e849b78dcf07eed/docs/docs/overview/data_privacy.md)。
- [MIT 许可](https://github.com/The-PR-Agent/pr-agent/blob/7bb7a68b451097d79dbc1c470e849b78dcf07eed/LICENSE)。
