<!-- markdownlint-disable MD013 -->

# Step Code（stepfun-ai/Step-Code）

- GitHub：<https://github.com/stepfun-ai/Step-Code>
- 抓取快照：2026-09-25，392 stars、40 forks、41 open issues
- 热度信号：GitHub TypeScript Trending 抓取时约 +37 当日 stars
- 版本与许可：MIT；无 GitHub Release / tag，根 package manifest 为 `0.1.0`

## 定位

Step Code 是阶跃星辰面向 Step 模型与 Step 账户体系的终端 coding agent，覆盖读代码、修改、运行测试、MCP、Agent Skills、plugins、多 Agent、长任务 `/goal` 和计划任务 `/cron`。它还内置 StepPage，可把本地静态页面发布到可访问 URL。

## 用法

macOS / Linux / WSL 和 Windows 分别使用官方 shell / PowerShell installer；启动 `step` 进入 TUI，或用 `step -p` 执行 headless task。用户通过 Step Plan OAuth 或 Step Platform API key 登录，从当前 Step endpoint 返回的模型中选择；项目可运行 `/init` 生成 `AGENTS.md`，首次启动还会导入 Claude Code / Codex MCP 配置。

## 原理

工具以本地用户权限读取 / 写入 workspace 并执行命令，长任务被拆到隔离上下文的 subagents，再由主会话跟踪目标状态。四种 permission mode 控制交互确认，plugin / MCP / Skill 扩展工具面；StepPage plugin 把本地产物上传到托管静态站点并维护版本 / 回滚。

## 价值

对已经采用 Step provider 的开发者，它把模型登录、终端 agent、长期目标、定时任务和页面交付合并在一个 CLI 中。兼容 MCP、Agent Skills 与大部分 Claude Code plugin，可降低既有工作流迁移成本；源码源自 MIT 的 Pi，便于审计派生关系。

## 风险边界

- 上游安全策略明确说明 Step Code 没有 sandbox，且把不可信仓库 prompt injection、恶意 Skill / extension、模型输出和本地用户可写配置列为边界外；permission mode 不是强隔离。
- 自动导入 MCP 配置、plugins、skills、`AGENTS.md` 和注释都可改变行为；“不修改源配置 / 不内联 secret”不能替代逐项 allowlist 与权限审计。
- `/goal`、`/cron` 与 Autopilot 会扩大无人值守时间；危险命令确认仍可能被误批或绕过业务级限制，需外部容器 / VM 与最小凭据。
- Step provider、OAuth / API key 与 StepPage 发布会离开本机；公开页面、构建产物、日志和模型输入必须按托管服务边界管理。
- 当前无 GitHub Release / tag，manifest 仅为 `0.1.0`；installer 的 `latest` 不足以支撑可复现部署，应固定 commit 与 checksum。

## 补充建议

先从源码或已下载 installer 做静态审计，在无凭据容器、测试仓库和 Read Only / Ask 模式中运行。只导入明确需要的 MCP 与 Skill，禁用 `/cron`、StepPage 和 Autopilot，记录每次命令 / 网络请求；通过注入恶意 `AGENTS.md`、symlink、环境变量和 plugin fixture 验证真实边界后再逐步授权。

## 参考资料

- [GitHub 仓库](https://github.com/stepfun-ai/Step-Code)
- [GitHub REST API](https://api.github.com/repos/stepfun-ai/Step-Code)
- [英文 README](https://github.com/stepfun-ai/Step-Code/blob/main/README.md)
- [中文 README](https://github.com/stepfun-ai/Step-Code/blob/main/README.zh-CN.md)
- [安全策略与明确边界](https://github.com/stepfun-ai/Step-Code/blob/main/SECURITY.md)
- [许可状态](https://github.com/stepfun-ai/Step-Code/blob/main/LICENSE-STATUS.md)
- [第三方声明](https://github.com/stepfun-ai/Step-Code/blob/main/THIRD_PARTY_NOTICES.md)
- [LICENSE](https://github.com/stepfun-ai/Step-Code/blob/main/LICENSE)
