<!-- markdownlint-disable MD013 -->

# Claude Plugins Community（anthropics/claude-plugins-community）

> 上游仓库：<https://github.com/anthropics/claude-plugins-community> · 归类：Agent 框架与技能生态 · 本页基于 2026-10-07 的 GitHub API、README、marketplace registry 与根 LICENSE 静态整理，未安装任何社区插件、连接 Claude 账号或复验上游内部审核。

- 抓取快照：4,517 stars、324 forks、62 open issues。
- 热度信号：GitHub JavaScript Trending 抓取时约 +25 当日 stars；最后 push 为 2026-10-05。
- 版本与许可：仓库无 GitHub Release / tag；根仓库 Apache-2.0；抓取时 `.claude-plugin/marketplace.json` 含 2,284 个条目；本页固定审计 commit `f60f0454df30`。

## 定位

这是 Anthropic 的 Claude Cowork / Claude Code 社区插件市场只读镜像。仓库公开经过提交与内部流水线后进入目录的 registry，并放置少量本地插件；它是发现、分发与固定来源的清单，不是所有插件源码都由 Anthropic 在本仓库维护。

## 用法

Claude Cowork 用户从官方插件界面安装；Claude Code 可先运行 `claude plugin marketplace add anthropics/claude-plugins-community`，再以 `<plugin-name>@claude-community` 安装单个插件。实际采用时不应批量安装，需先从 registry 记录目标 source、ref / SHA、作者、权限、MCP / hook / script 与许可证，再在专用 profile 或测试仓库逐个试用。

## 原理

README 称 registry 每晚从 Anthropic 内部审核流水线同步；每个条目描述名称、能力与来源，常见 source 指向外部 Git 仓库或子目录并固定 SHA，少量 source 指向本仓库路径。Claude 客户端读取 marketplace metadata 后再取得目标插件，因此本仓库既是目录入口，也是供应链路由表。

## 价值

集中 registry 让社区能力更易发现，固定 SHA 比只给浮动仓库 URL 更利于复查和回滚；只读同步也把“提交”和“分发镜像”分开。对团队选型，它提供了可机器读取的插件清单和统一安装标识。

## 风险边界

- 上游声称条目通过自动安全扫描和分发审批，但扫描 / 上架不是安全认证；2,284 个第三方插件不可能据根仓库声誉自动继承可信度。
- 插件可包含 prompts、skills、hooks、脚本、MCP、OAuth 与外部服务，可能读取仓库 / 个人数据、执行命令、发送消息、投放广告、交易或修改生产系统。
- registry 固定 source SHA 只标识取得的字节，不证明源码无恶意、依赖可复现、二进制同源、权限最小或运行结果正确。
- 根 Apache-2.0 不能自动覆盖所有外部插件、素材、模型、数据、API 与商业服务条款；必须逐条读取目标来源许可。
- 夜间同步会改变清单和可安装目标；仓库没有 Release / tag，生产团队需自行保存 registry 快照和已批准插件版本。
- 插件描述是作者 / 市场元数据，不等于功能、合规、准确率、费用或回滚能力已独立验证。

## 补充建议

建立 allowlist，记录插件名、source SHA、许可证、权限、外发域名、凭据、写操作、费用与负责人；安装前静态扫描，安装后在无秘密测试仓库以 deny-by-default 工具权限运行。对更新做 registry diff，只允许人工批准的 SHA 前进，并准备卸载、配置恢复和审计日志留存流程。

## 参考资料

- [GitHub 仓库](https://github.com/anthropics/claude-plugins-community)
- [GitHub REST API](https://api.github.com/repos/anthropics/claude-plugins-community)
- [README 与审核说明](https://github.com/anthropics/claude-plugins-community/blob/main/README.md)
- [Marketplace registry](https://github.com/anthropics/claude-plugins-community/blob/main/.claude-plugin/marketplace.json)
- [本仓库插件目录](https://github.com/anthropics/claude-plugins-community/tree/main)
- [Apache-2.0 License](https://github.com/anthropics/claude-plugins-community/blob/main/LICENSE)
- [官方插件仓库](https://github.com/anthropics/claude-plugins-official)
- [插件提交入口](https://clau.de/plugin-directory-submission)
