<!-- markdownlint-disable MD013 MD034 -->

# claude-code-templates：Claude Code 组件目录、安装器与会话工具箱

> 上游仓库：https://github.com/davila7/claude-code-templates · 归类：Coding Agents 与终端助手 · 本页基于 2026-09-22 的 README、站点、release、许可证与 REST API 静态整理；未运行 `npx`、安装模板 / MCP、读取本地会话或打开 tunnel。

## 定位

`claude-code-templates` 将 agents、commands、settings、hooks、MCP、skills 和 project templates 做成可浏览目录与 CLI 安装单元，并附带 analytics、conversation monitor、health check 与 plugin dashboard。它是第三方 Claude Code 生态工具，不是 Anthropic 官方组件商店或安全审查认证。

2026-09-22 的 GitHub 官方 Python Trending 抓取显示约 `+45 stars today`；REST API 快照为 `30,891 stars / 3,521 forks / 261 open issues`，MIT，最新 release 为 `v1.29.6`（9 月 17 日）。

## 用法

建议先在空目录查看帮助和选择单一低权限组件，避免把 `latest` 与 `--yes` 直接用于真实仓库：

```sh
npx claude-code-templates@1.29.6
npx claude-code-templates@1.29.6 --agent development-tools/code-reviewer
npx claude-code-templates@1.29.6 --health-check
```

上游也提供 `--analytics`、`--chats`、`--plugins` 与 `--chats --tunnel`。这些模式可能读取会话、启动本地服务或建立 Cloudflare Tunnel，必须在运行前审计监听地址、认证和数据范围。

## 原理

- Web catalog / Stack Builder 按类别展示组件，由 CLI 解析选项并写入 Claude Code 项目或用户配置。
- agent、command、setting、hook、MCP 与 skill 分别映射到 Claude Code 的扩展点，可一次组合多个单元。
- analytics 观察本地 Agent 会话状态，conversation monitor 提供移动端浏览 / resume 入口。
- health check 检查安装和配置，plugin dashboard 汇总 marketplace、已装插件与权限。
- 仓库同时聚合官方与社区来源，并在 README 列出部分归属；每个组件的真实代码、版本和许可仍需单独检查。

## 价值

- 统一搜索、预览和组合分散的 Claude Code 配置，降低手工复制路径和 JSON 的成本。
- 把 hooks、settings 与 MCP 放进同一可发现界面，便于团队形成可复用配置集合。
- 固定 CLI release 后可以在测试仓库记录安装 diff，并将选择的 stack 纳入评审。
- analytics / health 工具为配置排障和会话观察提供入口，不必完全依赖黑盒行为。

## 风险边界

- 一条安装命令可能写入 agent、hook、MCP 和 settings；这些单元可执行命令、读取仓库、访问网络或持有第三方凭据。
- 聚合目录与 MIT 主仓库不代表所有内含组件都同许可、同作者或经过同等级安全审核。
- `npx ...@latest --yes` 会同时放弃版本固定和交互复核，放大供应链、typosquat 和配置覆盖风险。
- analytics / chats 会读取本地会话；`--tunnel` 把服务暴露到远端，local view 不再等于本地数据边界。
- 模板数量、下载量和 stars 是采用信号，不是 prompt 正确性、MCP 权限安全或产出质量证明。

## 补充建议

1. 固定精确版本，在空仓库与隔离 `CLAUDE_CONFIG_DIR` 中安装，保存前后 diff 和卸载路径。
2. 对每个 hook / MCP / skill 查看上游、commit、许可证、命令、网络目标、secret 和 write scope，不按目录品牌批量信任。
3. 默认关闭 tunnel 与会话远程查看；确需启用时增加强认证、短 TTL、最小监听和访问日志。
4. 团队只维护一份审核通过的 allowlist / lockfile，不让个人临时 stack 自动进入生产仓库。

## 参考资料

- 上游 README：https://github.com/davila7/claude-code-templates
- 组件目录：https://aitmpl.com
- 文档：https://docs.aitmpl.com
- `v1.29.6` release：https://github.com/davila7/claude-code-templates/releases/tag/v1.29.6
- GitHub REST API：https://api.github.com/repos/davila7/claude-code-templates
- LICENSE：https://github.com/davila7/claude-code-templates/blob/main/LICENSE
