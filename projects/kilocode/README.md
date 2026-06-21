# kilocode（Kilo-Org/kilocode）

- GitHub: https://github.com/Kilo-Org/kilocode
- 官网: https://kilo.ai/
- 记录日期: 2026-06-21 (Asia/Shanghai)

## 定位

`kilocode` 是一个覆盖 VS Code、JetBrains 和 CLI 的开源 coding agent 平台。它的卖点不是只做单一编辑器插件，而是把模型切换、会话执行和多入口开发体验放到同一产品层里。

## 热度信号

1. GitHub API 在 2026-06-21 抓取时显示约 `23.4k stars`、`2.7k forks`，`updated_at` 为 `2026-06-21T01:00:40Z`。
2. GitHub Trending 日榜在 2026-06-21 抓取时出现 `Kilo-Org/kilocode`，说明它仍处在当天公共热点窗口。
3. 官方 README 直接把项目定义为 `The open source coding agent for building with AI in VS Code, JetBrains, or the CLI`，并强调 `500+ models`、`open pricing`、`zero markup`、`No API keys required to start`。

## 用法

### 1) 作为 CLI 使用

官方 README 提供多种安装方式：

```bash
npm install -g @kilocode/cli
# 或
curl -fsSL https://kilo.ai/cli/install | bash
```

安装后在项目目录运行：

```bash
kilo
```

### 2) 作为编辑器插件使用

- VS Code：安装 `Kilo Code` 扩展。
- JetBrains：在插件市场安装 `Kilo Code`。

### 3) 作为模型路由入口使用

README 明确支持在同一工作流里切换 500+ 模型，适合需要按任务类型更换模型的团队。

## 原理

1. 它把 IDE 插件和 CLI 统一到同一个 agent 产品面，而不是各自独立演化。
2. 通过托管账户体系和统一计费层，把“模型接入成本”从用户自己管理 API key 的模式下沉到平台能力。
3. 从 README 的功能描述看，`kilocode` 的目标是让“模型选择、会话继续、编辑器上下文、命令执行”形成一条连续开发链路。

## 价值

- 对已经不满足于单模型单入口的人，`kilocode` 提供了更接近“AI 开发工作台”的体验。
- 对团队试验不同大模型的 coding 能力时，它降低了切换和对比的摩擦。
- 它代表了开源 coding agent 正在往“平台化整合”方向推进，而不是只卷单点补全或聊天。

## 风险边界

- 虽然仓库开源，但其账户体系、模型入口和产品体验并不等于完全本地自治。
- “支持 500+ 模型”不等于每个模型在代码任务里都稳定可用，真实质量仍取决于底层模型和任务类型。
- 当平台承担模型路由和结算时，用户需要额外评估数据路径、成本可预期性和供应商依赖。

## 补充建议

1. 如果你主要关心本地可控性，应把它和 `aider`、`tabby`、`continue`、`codex` 分开比较，不要只看星标增长。
2. 评估时建议重点记录三类任务：跨文件修改、测试回归、长会话续跑，避免只凭第一次演示判断。
3. 若团队已有固定模型采购和审计要求，需要先确认其模型计费与日志边界是否符合内部规范。

## 参考资料

- https://github.com/Kilo-Org/kilocode
- https://kilo.ai/
- https://github.com/trending
