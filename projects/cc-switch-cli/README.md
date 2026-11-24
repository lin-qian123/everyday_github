<!-- markdownlint-disable MD013 -->

# CC-Switch CLI：多种 AI 终端工具的配置与会话管理面

- 上游：[SaladDay/cc-switch-cli](https://github.com/SaladDay/cc-switch-cli)，仓库 ID `1102384337`；本页新增于 2026-11-25。
- 快照：5,573 stars / 383 forks / 86 open issues（GitHub API 累计，含 PR）；Rust daily 显示 +8 stars。
- 最新发行：`v5.11.4`，2026-11-17 08:09 UTC；本轮主线 `c81e88ecf9c4704d8dbfbea3d4f4b6ff0b162ac5`，提交时间 2026-11-24 17:12 UTC。**主线 schema 27 修复尚未进入该发行版。**
- 证据范围：固定文档、局部源码与发行说明静态核读；未安装、切换账户、同步数据库、启动代理或调用模型。

## 定位

这是桌面项目 `farion1231/cc-switch` 的 CLI 分支，通过 Rust TUI 与命令管理 Claude Code、Codex、Gemini、OpenCode、Hermes、OpenClaw、Pi 的 provider、提示词、MCP、技能和会话。它统一的是配置与调度入口；不同工具的凭据、原生配置和功能支持仍有差异。

适合多终端、多 provider、远程主机上的配置管理。它不是新的推理模型，也不因能够切换 provider 就保证对方服务的模型身份、价格或可用性；README 中赞助商的宣传与本页技术事实分开。

## 用法

先从官方发行页选择匹配系统的版本，核对制品与原有配置备份。以下是**已安装可信版本后的命令示例**，本轮没有执行；程序启动可能初始化本地状态。

```bash
cc-switch --help
cc-switch config path
cc-switch --app claude provider list
cc-switch --app codex provider list
cc-switch proxy show
```

需要改动时，先运行 `cc-switch config backup --name before-switch`，再在 TUI 中逐项检查目标 provider。`provider switch <id>` / `use <id>` 改变全局 provider；`start claude <id>` 或 `start codex <id>` 为新启动的会话选择 provider。README 的 `start ... --dry-run` 是启动预览，不应由命令名推定整个进程没有文件副作用。

macOS / Linux 的 `start codex <id> --shared-sessions` 会共享会话、归档会话与 SQLite 历史索引，并保留 `.cc-switch-launches/` 下的 provider 目录；已有会话记录会引用这些路径，不宜随意清除。跨 provider 恢复还取决于目标服务接受旧对话内容，包括加密推理字段。

发行说明特别指出：受管理的 ChatGPT 账户不支持 `start`、TUI 临时启动或 `--shared-sessions`；须先切到绑定的官方 provider，再启动原生 Codex。不能把普通 API provider 的启动方式直接套到此路径。

## 原理

- **统一状态与原生配置适配。** 默认 SQLite 为 `~/.cc-switch/cc-switch.db`，技能源为 `~/.cc-switch/skills/`；`CC_SWITCH_CONFIG_DIR` 可改变管理目录，但不构成对宿主文件或子进程的隔离。
- **配置切换与进程启动分开。** 全局切换写入各客户端配置；临时 / 共享会话启动使用独立目录或设置，同时仍可能保存登录变化、共享历史与锁。
- **可选代理与协议适配。** 代理可按 app 启用、计量和转发。主线 `ProxyConfig::default` 监听 `127.0.0.1:15721`、`enable_logging=true`；数据库建表同时将代理启用标志默认置为 0。日志开关默认开不等于代理默认运行，也不证明日志不含敏感信息。
- **同步与数据库迁移。** WebDAV / S3 可上传或恢复快照。主线新增 26→27 兼容，保存 skill repository 的 host 字段，并避免将非 GitHub 项目误当 GitHub 更新；这不等于 CLI 新增 GitLab 技能仓库管理。

## 价值

它把 provider 切换、会话定位、MCP / 技能分发和用量入口放在一个可脚本化界面中，适合比较多个客户端配置并减少手工编辑。发行版还修复了 Codex 截断流被误作完成、Claude 缓存前缀与配置冲突等问题；这些是上游修复声明，本轮未复现。

对已有桌面 CC Switch 的用户，最有价值的检查项是数据库兼容与配置差异，而不是仅看“同步兼容”字样。此仓库是独立分支，版本号不能直接与桌面版比较。

## 风险边界

| 议题 | 已核事实与使用边界 |
| --- | --- |
| 发行与主线 | 5.11.4 支持到 schema 26；当前主线支持 27，对应桌面 4.0.34–4.0.40。不要用主线修复承诺已下载的 5.11.4 能打开 schema 27。更高 schema 仍拒绝。 |
| 迁移与恢复 | 升级后旧 CLI 可能无法打开新库；备份存在不代表恢复已验收，应在副本验证各设备版本和回退。 |
| 凭据与云同步 | 账户、provider、会话与同步目标形成多个数据出口；可选同步不等于端到端加密或最小权限已经成立，本轮未全面核验加密和脱敏。 |
| 启动与历史 | “isolated launch”描述配置启动路径，不证明 OS 沙箱。共享历史会扩大跨 provider 的可见内容，路径 / 锁 / 原生参数限制应逐项核验。 |
| 代理与费用 | loopback 默认值不是所有部署的认证保证；转换、重试、日志和价格种子需用真实 trace / 账单核对。 |
| 系统差异 | daemon 代理依赖 Unix socket supervisor，仅 macOS / Linux；Windows 使用前台代理入口，不能照搬 daemon 命令。 |

代码为 MIT；该许可不授予第三方服务、账户或模型权利。

## 补充建议

1. 先在测试用户与配置副本核 provider 列表、启动差异、会话锁和恢复路径，再迁移真实工作环境。
2. 同步前记录每台设备的 CLI / desktop / schema 版本；旧版本不兼容时，不靠反复下载快照解决。
3. 用 mock endpoint 验证流式截断、重试与计费记录，分开评估代理转换和模型实际输出。
4. 技能、MCP 与云同步分别检查安装目标、执行权限和敏感数据范围；不要把配置目录变量当安全边界。

## 参考资料

- [仓库 API](https://api.github.com/repos/SaladDay/cc-switch-cli)、[v5.11.4 发行说明](https://github.com/SaladDay/cc-switch-cli/releases/tag/v5.11.4)。
- [固定 README：命令、路径与平台限制](https://github.com/SaladDay/cc-switch-cli/blob/c81e88ecf9c4704d8dbfbea3d4f4b6ff0b162ac5/README.md)、[固定 CHANGELOG：Unreleased 与 5.11.4](https://github.com/SaladDay/cc-switch-cli/blob/c81e88ecf9c4704d8dbfbea3d4f4b6ff0b162ac5/CHANGELOG.md)。
- [数据库 schema](https://github.com/SaladDay/cc-switch-cli/blob/c81e88ecf9c4704d8dbfbea3d4f4b6ff0b162ac5/src-tauri/src/database/schema.rs)、[代理默认配置](https://github.com/SaladDay/cc-switch-cli/blob/c81e88ecf9c4704d8dbfbea3d4f4b6ff0b162ac5/src-tauri/src/proxy/types.rs)。
- [WebDAV 技能归档局部实现](https://github.com/SaladDay/cc-switch-cli/blob/c81e88ecf9c4704d8dbfbea3d4f4b6ff0b162ac5/src-tauri/src/services/webdav_sync/archive.rs)、[S3 CLI 入口](https://github.com/SaladDay/cc-switch-cli/blob/c81e88ecf9c4704d8dbfbea3d4f4b6ff0b162ac5/src-tauri/src/cli/commands/config_s3.rs)、[MIT LICENSE](https://github.com/SaladDay/cc-switch-cli/blob/c81e88ecf9c4704d8dbfbea3d4f4b6ff0b162ac5/LICENSE)。
