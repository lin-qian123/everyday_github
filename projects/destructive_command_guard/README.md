<!-- markdownlint-disable MD013 MD034 -->

# destructive_command_guard：在 Coding Agent 执行前拦截破坏性命令

> 上游仓库：https://github.com/Dicklesworthstone/destructive_command_guard · 归类：Coding Agents 与终端助手 · 本页基于 2026-09-22 的 README、配置 / integration 文档、release、自定义许可证与 REST API 静态整理；未安装 hook、扫描真实命令或验证跨 Agent 协议。

## 定位

Destructive Command Guard（`dcg`）是一个 Rust hook，在 Claude Code、Codex CLI、Gemini CLI、Copilot、Cursor、OpenCode 等 Agent 执行 shell / git 命令前做规则匹配，阻止高风险删除、历史改写、数据库 / 云 / 容器操作，并给出解释与替代建议。它是额外的策略层，不是 OS sandbox、备份或完整安全边界。

2026-09-22 的 GitHub 官方 Rust Trending 抓取显示约 `+11 stars today`；REST API 快照为 `6,032 stars / 246 forks / 11 open issues`，API 为 `NOASSERTION`，最新 release 为 `v0.14.4`（9 月 16 日）。根许可证是“MIT License (with OpenAI/Anthropic Rider)”，明确排除 OpenAI、Anthropic 及其关联 / 代表方，不能简称为标准 MIT 或 OSI 开源许可。

## 用法

由于安装器会修改多个用户级 Agent hook，建议下载 release、核对 checksum / signature，并先在临时配置目录测试；上游 quick install 为：

```sh
curl -fsSL "https://raw.githubusercontent.com/Dicklesworthstone/destructive_command_guard/main/install.sh" | bash -s -- --easy-mode
dcg explain "git reset --hard HEAD~5"
dcg packs --verbose
```

默认无配置时主要启用 `core.filesystem`、`core.git` 与 `system.disk`；数据库、Kubernetes、cloud、Docker 等多数 pack 需要显式打开。

## 原理

- Agent 的 pre-tool / Bash hook 把待执行命令交给 `dcg`，后者先做快速安全分类，再用 pack 规则、上下文分类和 allowlist 判断。
- heredoc、inline Python / shell 等嵌套内容会继续扫描，降低只检查首个 token 的绕过面。
- deny 通过各 Agent 要求的协议返回；Codex 路径需要最小 `hookSpecificOutput`，人类提示与机器 stdout 分离。
- `warn`、`log`、`ask`、per-rule policy、agent profile 与 allow-once code 允许逐层放宽；`DCG_BYPASS=1` 可整次绕过。
- scan mode 可在 pre-commit / CI 检查仓库中的危险命令，但与运行时 hook 是不同证据面。

## 价值

- 为多个 coding-agent 宿主提供一致的最后一道命令检查，降低误执行 `rm -rf`、`git reset --hard` 等灾难操作的概率。
- `explain`、rule ID、pack 与 JSON 输出有利于审计阻断原因和调整 policy。
- 默认 pack 较窄，扩展 pack opt-in，可避免安装后立刻对所有数据库 / 云命令施加未经调优的阻断。
- allow-once 和 agent profile 为紧急操作与不同信任上下文提供可记录的例外机制。

## 风险边界

- 正则 / 解析 / hook 覆盖都会有 false negative；新 shell 语法、编码、间接执行、远端脚本和未接入 hook 的工具可能绕过。
- false positive 或错误 `critical` policy 会阻断合法维护；`DCG_BYPASS=1`、allowlist 与被篡改配置也会使保护失效。
- hook 与 Agent 同用户运行，不能防止宿主进程、恶意依赖、直接系统调用或已获更高权限的攻击者。
- 自定义 rider 对特定公司及极广泛关联方禁止使用、分析、索引、托管等行为；组织采用前必须做法律审查。
- 本页未复现上游 sub-millisecond 性能、50+ packs 覆盖率或各宿主当前协议兼容性。

## 补充建议

1. 先确认组织是否有权使用该许可证；不能把 SPDX `NOASSERTION` 自动映射为 MIT。
2. 用一组 allow / deny / ambiguous / encoded / heredoc 金标命令做回归，记录每次版本升级的误报与漏报。
3. 同时保留版本控制、离线备份、最小权限、容器 / VM 隔离和人工审批，不把 hook 当唯一防线。
4. 对 bypass、allow-once、配置变更和 hook 缺失生成审计事件，并定期验证每个 Agent 仍实际调用它。

## 参考资料

- 上游 README：https://github.com/Dicklesworthstone/destructive_command_guard
- Agent integration：https://github.com/Dicklesworthstone/destructive_command_guard/blob/main/docs/agents.md
- Codex integration：https://github.com/Dicklesworthstone/destructive_command_guard/blob/main/docs/codex-integration.md
- Pack index：https://github.com/Dicklesworthstone/destructive_command_guard/blob/main/docs/packs/README.md
- `v0.14.4` release：https://github.com/Dicklesworthstone/destructive_command_guard/releases/tag/v0.14.4
- GitHub REST API：https://api.github.com/repos/Dicklesworthstone/destructive_command_guard
- 自定义许可证：https://github.com/Dicklesworthstone/destructive_command_guard/blob/main/LICENSE
