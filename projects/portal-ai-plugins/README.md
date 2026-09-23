<!-- markdownlint-disable MD013 -->

# portal-ai-plugins（spotify/portal-ai-plugins）

- GitHub：<https://github.com/spotify/portal-ai-plugins>
- 抓取快照：2026-09-24，2,216 stars、176 forks、9 open issues
- 热度信号：GitHub TypeScript Trending 抓取时约 +34 当日 stars
- 版本与许可：Apache-2.0；无 GitHub Release / tag，Portal manifests 为 `0.1.0`，Claude-only `shunt` 为 `0.2.0`

## 定位

这是 Spotify Portal 的官方 coding-agent plugin marketplace，把 Portal CLI 的认证、软件目录 / 技术文档搜索、service briefing、诊断和 action 调用封装成 Claude Code、Codex 与 Cursor 工作流。仓库还包含 Claude Code 专用 `shunt`，把大文件读取和样板生成委派给 Portal 上的 AiKA worker modes。

## 用法

Claude Code 可添加 marketplace 后安装 `portal@portal`；Codex 可添加同一 plugin marketplace 并在 `/plugins` 中安装 Spotify Portal；Cursor 通过 team marketplace 注册仓库。安装后先运行 setup / doctor，确认 `auth`、`actions`、`owner`、`search`、`service` 命令，再在已授权 Portal instance 上查询服务或以 dry-run / confirmation 调用 action。

## 原理

六个 skills 通过 `npx @spotify/portal-cli` 调用 Portal 后端，manifest 声明 Read、Write、CLI 能力。Portal plugin 负责环境探测和结构化工作流；`shunt` 额外用 `PreToolUse` hooks 拦截超大 `Read` / shell 读取，再由固定脚本将文件封装后调用 `aika:invoke-chat`，避免主 Agent 直接吞入完整语料。

## 价值

它把开发者门户中的 ownership、health、incident、docs 与 action 接到 coding-agent 上下文，适合服务定位、交接和受控运维。相较临时拼 shell，固定 CLI、doctor、help、dry-run 和确认步骤更容易审计；多宿主 manifests 也降低了同一企业工作流的重复维护。

## 风险边界

- 插件能读写并调用 CLI / Portal actions；安装官方仓库不等于自动授权所有 service、secret 或生产动作，仍需最小 scope 与人工 gate。
- 认证、搜索和 action 会访问 Portal instance；代码、服务元数据与输入是否进入 hosted Portal / AiKA 取决于组织部署和隐私条款。
- `shunt` 的 82%--94% token savings 是作者在特定 Java monorepo 的报告，本轮未重跑；摘要 / 生成委派也可能丢失细节或引入错误。
- `shunt` 只对 bulk reader 有 hook enforcement，code writer 依赖模型识别；argv payload 还受 `ARG_MAX` 与 timeout 约束。
- 仓库无 Release / tag 且 manifests 版本不同；安装必须锁定 commit 并记录 Portal CLI / instance 兼容矩阵。

## 补充建议

先在只读测试 tenant 使用最低权限账号运行 setup、doctor、search、service；对 actions 建立 allowlist、dry-run 和二次确认。启用 `shunt` 前，用已知答案的大文件集测 omission、行号准确性和成本，把 worker model、Portal instance、payload 上限与失败回退写入运行记录。

## 参考资料

- [GitHub 仓库](https://github.com/spotify/portal-ai-plugins)
- [GitHub REST API](https://api.github.com/repos/spotify/portal-ai-plugins)
- [Portal 插件 README](https://github.com/spotify/portal-ai-plugins#readme)
- [Codex plugin manifest](https://github.com/spotify/portal-ai-plugins/blob/main/.codex-plugin/plugin.json)
- [Claude marketplace manifest](https://github.com/spotify/portal-ai-plugins/blob/main/.claude-plugin/marketplace.json)
- [shunt 说明与 benchmark](https://github.com/spotify/portal-ai-plugins/blob/main/plugins/shunt/README.md)
- [LICENSE](https://github.com/spotify/portal-ai-plugins/blob/main/LICENSE)
