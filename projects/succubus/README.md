# succubus

## 定位

`succubus` 是面向同一仓库多 coding-agent 会话的本地协调 daemon：它以一个数据库保存共享计划、任务、问题与文件租约，并用 MCP、hooks 与 SSE dashboard 把状态分发给 Claude Code、OpenCode、Codex、Gemini 等会话。

截至 2026-07-29，GitHub API 显示其创建于 2026-07-28，约 8 stars、1 fork，采用 MIT；它应视为早期开发者信号，而非已证实的团队协同基础设施。

## 用法

项目提供预编译安装脚本和从源码构建方式。更安全的做法是先下载、审阅并校验安装脚本，再在一个非关键仓库中运行初始化；不要直接把未审阅脚本接进高权限开发环境。

```bash
succubus setup
succubus daemon
```

dashboard 默认在 `http://127.0.0.1:7801`。启用后台服务前，确认 macOS `launchd`、Linux user systemd 或 Windows 用户级 Run key 的持久化行为符合本机策略。

## 原理

每个 agent 获得可恢复身份；任务板与问题区保存协调状态；文件声明以带 TTL 的 advisory lease 避免同时编辑，daemon 失效时 hooks 选择静默降级而非阻断工作。上下文会在会话开始与每个 prompt 注入，以降低 agent 忘记协调状态的概率。

## 价值

- 对多终端、多 agent 并行改同一仓库的冲突提供了可视化、低依赖的协调层。
- 文件租约、任务依赖和未回答问题让人工能检查“谁在改什么、为什么卡住”。

## 风险边界

- 租约是建议式而非版本控制锁，不能代替小提交、测试、rebase 和人工合并审查。
- 持久 daemon、日志与注入上下文可能保存项目路径、任务描述或敏感业务信息；必须检查本地权限与保留周期。
- 支持的 agent/hook 配置会快速变化，自动合并现有配置前应先备份并 review diff。

## 补充建议

先对两个低权限会话试验“任务声明 + 文件 lease + 崩溃过期”三条路径；把强制质量门继续放在 Git、CI 和 code review，而非交给协调面板。

## 参考资料

- GitHub：<https://github.com/enowdev/succubus>
- GitHub API 快照：<https://api.github.com/repos/enowdev/succubus>
