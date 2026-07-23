# openhub

## 定位

`openhub` 是 Python/Textual 实现的终端 AI 工具、MCP server 与 agent skill 发现和安装中心，使用本地 SQLite 缓存并导出通用 `SKILL.md`。截至 2026-07-24，仓库创建于 2026-07-23，约 9 stars。

## 用法

可用 `pipx install git+https://github.com/24KaratAu/openhub.git` 安装后运行 `openhub`，或在克隆目录执行 `pip install -e .`。在 TUI 中搜索、浏览集合后，先检查来源与安装脚本，再按需将 skill 导出到项目或用户级 agent 目录。

## 原理

程序以 SQLite 缓存目录元数据、后台同步 GitHub 信息，并在本地用模糊检索匹配名称、描述与用途。导出环节将所选能力组织成 agent 可读取的 `SKILL.md` 目录。

## 价值

- 把零散的工具、MCP 与 skills 统一到键盘优先的发现入口。
- 本地缓存能缩短重复浏览的启动时间。
- 以标准目录导出，便于在多个 agent runtime 间复用。

## 风险边界

- “质量评级”和集合策展并非安全审计，不能替代来源、许可证与代码审查。
- 自动安装/导出会影响 agent 可调用的工具表面，可能扩大权限和供应链风险。
- README 的技术文档链接目前指向作者本地 `file://` 路径，外部用户不可访问。

## 补充建议

将其视为发现层而非信任根：安装前固定 commit、审查 `SKILL.md` 和脚本权限；团队可维护允许列表并隔离用户级与仓库级导出。

## 参考资料

- GitHub：<https://github.com/24KaratAu/openhub>
