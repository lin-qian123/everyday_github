# codex-hygiene

<!-- markdownlint-disable MD013 -->

## 定位

`codex-hygiene` 是一个面向 Codex Desktop 的社区 skill，用于审计和调优本地 Codex 上下文与工具表面。它关注最近线程 token telemetry、MCP / app / skill 可用性、长线程 replay、插件状态和上下文膨胀问题。

截至 2026-07-13，GitHub API 显示该仓库约 234 stars、7 forks，创建于 2026-07-07，许可证为 MIT。它不是通用 agent 框架，而是 Codex 本地环境诊断工具。

## 用法

安装到用户级 skills 目录：

```bash
mkdir -p "$HOME/.agents/skills"
git clone https://github.com/sunflower-of-parchman/codex-hygiene.git \
  "$HOME/.agents/skills/codex-hygiene"
```

在 Codex 中调用：

```text
$codex-hygiene
```

从 shell 做快速测量：

```bash
SKILL_DIR="$HOME/.agents/skills/codex-hygiene"
"$SKILL_DIR/scripts/measure_codex_context.sh"
```

## 原理

codex-hygiene 通过只读 SQLite 查询和本地缓存检查，统计 Codex Desktop 最近的工具列表、线程 token、MCP / app / plugin 表面，并区分“可用工具多”和“实际调用多”。它强调先测量，再给出可逆的清理建议。

## 价值

- 直接面向 Codex Desktop 用户的真实痛点：长线程、工具面过大、插件状态复杂、上下文 replay 变慢。
- 读本地 telemetry，但避免打印完整日志、schema、密钥或 `.env`。
- 有助于把“Codex 为什么变慢 / token 为什么高”从猜测变成可复核数据。
- 与 `contextvc`、`ditto`、`brain0` 共同指向 agent 本地工作台的可维护性问题。

## 风险边界

- 依赖 Codex Desktop 本地数据库和缓存布局，版本变化可能导致脚本失效。
- 统计结果不是账单，也不是模型实际推理成本的完整来源。
- 虽然默认只读，用户仍需谨慎执行任何删除、禁用或配置修改建议。
- 社区 skill 不是 OpenAI 官方工具，安全和兼容性需要自行审查。

## 补充建议

- 适合在 Codex 使用异常变慢、工具列表膨胀或长任务上下文异常时运行。
- 团队内部可借鉴它的“先测量工具面，再做可逆调整”原则。
- 关注其测试脚本和 remediation 文档是否跟随 Codex 版本更新。

## 参考资料

- GitHub 仓库：<https://github.com/sunflower-of-parchman/codex-hygiene>
- Codex Skills 文档：<https://developers.openai.com/codex/skills>
- Codex 配置参考：<https://developers.openai.com/codex/config-reference>
