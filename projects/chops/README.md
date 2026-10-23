<!-- markdownlint-disable MD013 -->

# chops

- 主上游：[Shpigford/chops](https://github.com/Shpigford/chops)
- 分类：Agent 框架与技能生态。
- 核验日期：2026-10-24（Asia/Shanghai）；默认分支 `main` 快照 `9d379d582c8b`。
- [API](https://api.github.com/repos/Shpigford/chops) 快照：2,067 stars / 132 forks / 11 open issues；发行列表首项 [v1.16.0](https://github.com/Shpigford/chops/releases/tag/v1.16.0)（UTC 2026-08-23，正式）。累计量不是今日增长，主线也不等于发行版。

## 定位

Chops 是 macOS 原生技能 / Agent 文件管理器，用一套界面发现、搜索、编辑和组织 Claude Code、Cursor、Codex、Windsurf、Amp 等工具的配置文件，还支持远程目录与技能注册表。它管理能影响 Agent 行为的文件，不为技能内容提供可信认证。 [README.md](https://github.com/Shpigford/chops/blob/9d379d582c8b1f77491df6aabf1049e578373845/README.md)

## 用法

普通使用下载正式发行 DMG；源码构建要求 macOS 15+、Xcode 与 xcodegen，按 README 生成工程后运行。初次先配置一个可恢复的测试技能目录，再核扫描来源、编辑 / 保存与多工具链接关系。README 的 `~/.codex/skills/` 等为上游约定，实际路径以本机工具配置为准。 [README.md](https://github.com/Shpigford/chops/blob/9d379d582c8b1f77491df6aabf1049e578373845/README.md)、[Chops/Models/ToolSource.swift](https://github.com/Shpigford/chops/blob/9d379d582c8b1f77491df6aabf1049e578373845/Chops/Models/ToolSource.swift)

## 原理

SwiftUI / SwiftData 保存索引与集合，解析 frontmatter / Cursor MDC，FSEvents 触发文件变化重扫；按解析后的符号链接路径去重。同一个底层文件可属于多个工具，编辑时应理解它们共享内容。远程功能通过系统 SSH 读取或写入文件。 [README.md](https://github.com/Shpigford/chops/blob/9d379d582c8b1f77491df6aabf1049e578373845/README.md)、[Chops/Services/SSHService.swift](https://github.com/Shpigford/chops/blob/9d379d582c8b1f77491df6aabf1049e578373845/Chops/Services/SSHService.swift)

## 价值

适合解决多个编码工具下技能分散、重复副本难同步的问题，便于检索和人工检查。集合管理和文件扫描本身不证明技能正确、安全或与宿主版本兼容。

## 风险边界

- 应用明确关闭 macOS App Sandbox，以读取用户目录下工具配置；entitlements 中 sandbox 为 false。权限范围需要结合真实可访问目录判断，不能因原生 UI 认为有系统沙箱。 [README.md](https://github.com/Shpigford/chops/blob/9d379d582c8b1f77491df6aabf1049e578373845/README.md)、[Chops/Chops.entitlements](https://github.com/Shpigford/chops/blob/9d379d582c8b1f77491df6aabf1049e578373845/Chops/Chops.entitlements)
- SSHService 使用系统 `/usr/bin/ssh`，包含远程写文件能力，连接参数为 `BatchMode=yes`、`StrictHostKeyChecking=accept-new`；首次主机身份仍需外部可信核对。符号链接去重可能扩大一次编辑对多工具的影响。 [Chops/Services/SSHService.swift](https://github.com/Shpigford/chops/blob/9d379d582c8b1f77491df6aabf1049e578373845/Chops/Services/SSHService.swift)
- 下载注册表技能、Sparkle 更新和远程 SSH 是不同外部路径，管理器不替代逐个审阅技能及其脚本。上游 README 明示没有自动测试套件。 [README.md](https://github.com/Shpigford/chops/blob/9d379d582c8b1f77491df6aabf1049e578373845/README.md)
- 根许可为 FSL-1.1-MIT，当前版本限制竞争性商业提供；每一版本在发布满两周年后有未来 MIT 授权。不能简称当前就是 MIT 开源许可。 [LICENSE](https://github.com/Shpigford/chops/blob/9d379d582c8b1f77491df6aabf1049e578373845/LICENSE)

## 补充建议

用临时技能、符号链接和损坏 frontmatter 测发现 / 去重 / 保存，再核远程只读账号与拒绝写入、更新回滚及备份恢复。接入真实技能前先观察实际写入路径。本轮未下载 DMG、构建应用、连接远程机或更改技能文件。

## 参考资料

- [README.md](https://github.com/Shpigford/chops/blob/9d379d582c8b1f77491df6aabf1049e578373845/README.md)（固定 commit）。
- [Chops/Chops.entitlements](https://github.com/Shpigford/chops/blob/9d379d582c8b1f77491df6aabf1049e578373845/Chops/Chops.entitlements)（固定 commit）。
- [Chops/Services/SSHService.swift](https://github.com/Shpigford/chops/blob/9d379d582c8b1f77491df6aabf1049e578373845/Chops/Services/SSHService.swift)（固定 commit）。
- [Chops/Models/ToolSource.swift](https://github.com/Shpigford/chops/blob/9d379d582c8b1f77491df6aabf1049e578373845/Chops/Models/ToolSource.swift)（固定 commit）。
- [LICENSE](https://github.com/Shpigford/chops/blob/9d379d582c8b1f77491df6aabf1049e578373845/LICENSE)（固定 commit）。
- [发行列表](https://github.com/Shpigford/chops/releases)、[仓库 API](https://api.github.com/repos/Shpigford/chops)（动态状态）。
