<!-- markdownlint-disable MD013 -->

# Claude Octopus（nyldn/claude-octopus）

> 上游仓库：<https://github.com/nyldn/claude-octopus> · 归类：Agent 框架与技能生态 · 本页基于 2026-10-02 的 GitHub API、README、package / plugin manifests、security policy、Release 与 LICENSE 静态整理，未安装 plugin、配置 provider 或运行多模型 council。

- 抓取快照：4,138 stars、390 forks、31 open issues。
- 热度信号：GitHub Shell Trending 抓取时约 +7 当日 stars。
- 版本与许可：MIT；latest Release / tag 与 package manifest 均为 `v11.9.6`。

## 定位

Claude Octopus 是以 Claude Code 为主要宿主、兼容 Codex / Cursor / OpenCode 等入口的多模型编排 plugin。它把研究、设计、实现、审查、council、adversarial review 与“Dark Factory”长流程组织成显式命令，可连接 Codex、Copilot、Qwen、Ollama、Perplexity、OpenRouter、OpenCode、Grok、Kimi 等十二类外部 provider integration。

## 用法

Claude Code 可添加 `nyldn/plugins` marketplace 后安装 `octo`，再运行 `/octo:setup`；Codex 可用对应 marketplace 安装后重启，通过 `$skill-*` 入口调用。默认普通 prompt 不触发 Octopus，用户显式执行 `/octo:*`；可选 auto router、premium peer check、session memory、compression 与 strategy rotation 都通过环境变量或 profile 开启。

## 原理

工作流把任务分发到 provider-specific adapter 与角色 Agent，收集结构化结果后做 75% consensus、critical veto、quality / cost gate 和阶段交接；council 支持不同人数、目标和 adversarial 风格。plugin 还包含 hooks、MCP server、worktree handoff、capability / doctor / cache check、audit log 与多种 memory integration。

## 价值

显式升级路径允许普通任务留在单一宿主，只有架构、审查或争议任务才增加独立模型视角。统一 provider readiness、budget、输出摘要和失败恢复也比手工复制 prompt 更容易追踪“哪些模型真的参与了结论”。

## 风险边界

- 多模型一致不等于正确：provider 可能共享训练偏差、错误上下文或同一提示注入；75% consensus 不能替代测试、数据和人类责任。
- provider CLI / API 会接触 prompt、代码、结果与凭据，数据保留、地域、费用、速率限制和模型版本分别受各账号条款约束。
- plugin 含大量 shell、hook、MCP 与可选自动路由；显式命令门槛不是 OS sandbox，生成代码和外部 CLI 仍以用户权限运行。
- auto router、premium peer check、Dark Factory、reaction engine 与 worktree handoff 会显著扩大调用、写入和成本面，应保持 opt-in。
- `SECURITY.md` 的 supported-version 表仍停在 9.23.x / 9.22.x，而当前 Release 已到 11.9.6，说明安全文档存在版本漂移；不能据其表格推定当前维护承诺。
- audit log、task files、memory plugin 和 provider cache 可能积累敏感任务元数据；“keys 不写日志”不代表上下文与结果没有持久化。

## 补充建议

固定 `v11.9.6`，从只启用一个低额度 / 本地 provider 开始，检查 plugin hooks、MCP、audit / cache 路径和实际发送内容；默认保持 auto router 关闭。为 council 准备可独立判定的 gold tasks，记录成本、延迟、分歧、实际 provider roster 与最终测试，而不是只看 consensus。升级时同时比对 README、SECURITY、manifest、第三方 notices 与 shell diff。

## 参考资料

- [GitHub 仓库](https://github.com/nyldn/claude-octopus)
- [GitHub REST API](https://api.github.com/repos/nyldn/claude-octopus)
- [README 与安装说明](https://github.com/nyldn/claude-octopus/blob/main/README.md)
- [Plugin 兼容文档](https://github.com/nyldn/claude-octopus/blob/main/docs/PLUGIN-COMPATIBILITY.md)
- [Model routing strategy](https://github.com/nyldn/claude-octopus/blob/main/docs/MODEL-ROUTING-STRATEGY.md)
- [SECURITY](https://github.com/nyldn/claude-octopus/blob/main/SECURITY.md)
- [THIRD_PARTY_NOTICES](https://github.com/nyldn/claude-octopus/blob/main/THIRD_PARTY_NOTICES.md)
- [v11.9.6 Release](https://github.com/nyldn/claude-octopus/releases/tag/v11.9.6)
- [LICENSE](https://github.com/nyldn/claude-octopus/blob/main/LICENSE)
