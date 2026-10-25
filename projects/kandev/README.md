<!-- markdownlint-disable MD013 -->

# Kandev：以看板、执行器和审阅关卡编排多种编码 Agent

- 主上游：[kdlbs/kandev](https://github.com/kdlbs/kandev)；repository ID `1131388506`。
- 采样日期：2026-10-26（Asia/Shanghai）；分类：Coding Agents 与终端助手。
- API 累计快照：1,014 stars / 167 forks / 222 open issues（含 PR 口径）；与榜单日增分开。
- 默认分支 `main`，本页静态依据固定在 `f33e6ef287d53c93b19f95c7054feb7080ec77b0`。发行 API 首项 [v0.98.0](https://github.com/kdlbs/kandev/releases/tag/v0.98.0)，UTC 2026-10-23T13:16:01Z，正式发行。
- 核验层级：读取上游文档、许可、元数据及所列部分实现；未安装运行上游、调用模型或复现实验。

## 定位

Kandev 是可本机运行或自托管的编码 Agent 工作台，用看板和流水线管理任务，集中展示对话、编辑器、终端、浏览器预览与 Git 差异。它可以接入多种现有 CLI，而非自带统一模型。常规 Kanban 自动化与实验性 Office 持续团队是不同功能层。

## 用法

上游 Homebrew 入口与显式本机监听示例为以下形式，本轮未安装或启动：

```bash
brew install kdlbs/kandev/kandev
KANDEV_SERVER_HOST=127.0.0.1 KANDEV_BACKEND_PORT=38429 kandev
```

原生 Go 二进制已嵌入前端，不要求应用服务器另装 Node；npm / npx 启动器仍需要 Node 环境。配置 provider CLI、执行器及测试仓库，再建立一个有限任务。默认数据目录为 ~/.kandev；升级前应备份数据库和 worktree。源码构建的 Go 1.26.0、Node 24、pnpm 9.15.9 不应误写成所有分发包的运行依赖。

## 原理

Go 后端管理任务、会话、生命周期和实时通信，前端提供审阅工作台。多数结构化 Agent 通过 ACP 接入，Codex app-server 另属实验性原生集成，纯 TUI 也可通过 PTY 运行。worktree 分开各任务的代码副本；Local Process、Docker、SSH、Kubernetes、Sprites 等执行器决定进程实际在哪运行。工作流关卡控制任务推进，不能独立证明执行器已被缩权。

## 价值

适合对多个任务、多个 provider、多个仓库进行统一调度与审阅，尤其是需要将执行移到远端而继续在本机或手机审阅的场景。可移植工作流与每任务差异能改善交接，但同时运行更多 Agent 会增加计算、模型费用及审阅负担，不能以并发数代替吞吐和质量测量。

## 风险边界

- **认证在所有出厂 profile 中默认关闭，认证本身仍是实验性开关。** 当前文档明确：未启用认证时，任何可达客户端共享合成管理员身份。私有网络、TLS 代理与应用账号是不同边界；多人或不可信设备接入需单独配置认证。
- worktree 不隔离文件系统与网络；本机、容器、SSH 和云端执行器各有凭据、挂载与外发范围。对工具、任务间 MCP、插件和外部 MCP 都要审阅权限。
- Office 在生产默认关闭且尚非稳定契约；一轮 Agent 成功不代表任务已通过 Review / Approval 并进入 Done。
- README 宣称无遥测，本轮未做全仓数据流或实际流量验收。debug 文档明确日志可包含 prompt、工具调用、路径和上下文；任务快照可发布为 secret GitHub Gist，分享前仍需检查脱敏、可达范围与撤销。
- v0.98.0 发行警告桌面安装器是未签名开发制品；校验和不等于发布者签名。本轮不执行绕过系统安全机制的命令。代码为 AGPL-3.0，修改后提供网络服务须核相应义务。

## 补充建议

先用单一 provider、单任务、本机监听验证关卡是否真的阻止推进，并检查失败恢复和数据库备份。远端试用按“谁可访问控制台、谁可使用执行器、进程持有哪些凭据”分别验收；用人工构造的敏感占位串检查日志和分享预览。Office 团队与例行任务在小规模费用和暂停机制验收后再扩大。

## 参考资料

- [README.md](https://github.com/kdlbs/kandev/blob/f33e6ef287d53c93b19f95c7054feb7080ec77b0/README.md)。
- [LICENSE](https://github.com/kdlbs/kandev/blob/f33e6ef287d53c93b19f95c7054feb7080ec77b0/LICENSE)。
- [docs/public/authentication.md](https://github.com/kdlbs/kandev/blob/f33e6ef287d53c93b19f95c7054feb7080ec77b0/docs/public/authentication.md)。
- [docs/public/mobile-remote-access.md](https://github.com/kdlbs/kandev/blob/f33e6ef287d53c93b19f95c7054feb7080ec77b0/docs/public/mobile-remote-access.md)。
- [docs/public/office.md](https://github.com/kdlbs/kandev/blob/f33e6ef287d53c93b19f95c7054feb7080ec77b0/docs/public/office.md)。
- [docs/debug-logs.md](https://github.com/kdlbs/kandev/blob/f33e6ef287d53c93b19f95c7054feb7080ec77b0/docs/debug-logs.md)。
- [仓库 API](https://api.github.com/repos/kdlbs/kandev)、[发行 API](https://api.github.com/repos/kdlbs/kandev/releases?per_page=1)；动态元数据仅代表本轮采样。
- 事实来源为以上一手材料；价值、风险评估和建议为本库工程判断，未当作上游实测结果。
