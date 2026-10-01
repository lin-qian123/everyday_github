<!-- markdownlint-disable MD013 -->

# Awesome Codex & ChatGPT Plugins（hashgraph-online/awesome-codex-plugins）

> 上游仓库：<https://github.com/hashgraph-online/awesome-codex-plugins> · 归类：Agent 框架与技能生态 · 本页基于 2026-10-02 的 GitHub API、README、marketplace、scanner guide、security policy 与 LICENSE 静态整理，未安装目录中的任何 plugin，也未独立复跑集中扫描。

- 抓取快照：1,139 stars、323 forks、25 open issues。
- 热度信号：GitHub Python Trending 抓取时约 +19 当日 stars。
- 版本与许可：仓库为 Apache-2.0；无 GitHub Release / tag；`plugins.json` 标为 `1.0.0`、2026-10-01 更新并记录 250 个条目。

## 定位

这是面向 Codex / ChatGPT plugin、Skill 与相关资源的社区目录，同时提供可被 Codex 添加为来源的仓库型 marketplace。与只列链接的 awesome list 不同，它把入选项目镜像为仓库内可安装 bundle，并在 `.agents/plugins/marketplace.json` 中描述来源、展示名、策略和分类。

## 用法

Codex CLI 可把仓库 URL 作为 marketplace source 添加，再用来源名列出和安装 plugin；桌面端 / IDE 也可在插件设置中添加同一仓库。维护者建议提交前运行 `plugin-scanner lint` / `verify`，目录准入依赖集中扫描的数值分数至少达到 80 / 130；源仓库自行运行 scanner CI 只是推荐项。

## 原理

目录通过 `plugins.json` 维护上游元数据，由构建脚本生成 marketplace，并把可安装内容镜像进 `plugins/<owner>/<repo>`。集中扫描检查 manifest、已知 secret 形态、远端 MCP 配置、SECURITY / LICENSE 和操作风险等规则；安装时 Codex 从当前仓库 clone 指定路径，而不是临时再抓取每个上游。

## 价值

统一目录降低了跨仓库发现、格式适配与安装摩擦；镜像 bundle 让某一目录 commit 可被审阅、固定和复现。对团队试点，marketplace manifest 也比随手复制 Skill 更容易建立 allowlist、版本台账和更新 diff。

## 风险边界

- 80 / 130 是规则扫描阈值，不是恶意代码、数据外发、权限合理性或运行正确性的认证；低危组合、提示注入和运行时下载仍可能绕过静态规则。
- 仓库 `SECURITY.md` 仍称其为“无可执行代码的 curated list”，但当前 checkout 已包含镜像 plugin、构建脚本与可安装 marketplace；安全说明与实际供应链表面存在文档漂移。
- 源仓库 CI 可选，目录集中扫描也可能只覆盖某个快照；上游更新、镜像更新与本地已安装版本必须分别固定。
- Apache-2.0 覆盖目录仓库本身，不自动覆盖每个 plugin 的代码、Skill 内容、MCP 服务、模型、素材或第三方依赖。
- 目录无 Release / tag；直接跟随 `main` 会让安装内容随提交变化，不能把 stars、awesome 标签或“curated”当作发布签名。
- plugin 可同时携带 Skill、hook、MCP、app 与外部认证，安装后可能获得文件、shell、网络和第三方账号权限。

## 补充建议

只从固定 commit 添加 marketplace；安装前审查目标 bundle 的 manifest、hook、Skill、MCP / app、认证与网络端点，并与上游原仓库 commit 对照。把集中扫描结果当作初筛，再在无 secret、低权限、可丢弃 workspace 中做动态测试；升级时重新审查 diff、许可证和权限，不批量默认信任 250 个条目。

## 参考资料

- [GitHub 仓库](https://github.com/hashgraph-online/awesome-codex-plugins)
- [GitHub REST API](https://api.github.com/repos/hashgraph-online/awesome-codex-plugins)
- [README 与安装说明](https://github.com/hashgraph-online/awesome-codex-plugins/blob/main/README.md)
- [Marketplace manifest](https://github.com/hashgraph-online/awesome-codex-plugins/blob/main/.agents/plugins/marketplace.json)
- [Plugin Quality / Scanner Guide](https://github.com/hashgraph-online/awesome-codex-plugins/blob/main/SCANNER_GUIDE.md)
- [结构化目录数据](https://github.com/hashgraph-online/awesome-codex-plugins/blob/main/plugins.json)
- [SECURITY](https://github.com/hashgraph-online/awesome-codex-plugins/blob/main/SECURITY.md)
- [LICENSE](https://github.com/hashgraph-online/awesome-codex-plugins/blob/main/LICENSE)
