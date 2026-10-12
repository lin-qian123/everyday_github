<!-- markdownlint-disable MD013 -->

# Token Monitor（Javis603/token-monitor）中文解读

> 上游仓库：<https://github.com/Javis603/token-monitor> · 归类：Coding Agents 与终端助手 · 本页基于 2026-10-13 的 README、隐私 / 配置 / API 文档、Release、manifest、许可证与 GitHub REST API 静态整理；未读取本机 Agent transcript、provider 凭据、费用或账户限额。

## 定位

Token Monitor 是本地优先的 Electron 桌面组件，用于从 44+ AI coding tools 的本地日志、数据库或 provider 限额接口中汇总 token、cache hit、成本、会话、项目和配额窗口，并可通过自托管 Hub、Cloudflare Worker 或 iCloud 在多设备间同步摘要。

## 用法

macOS 可通过 Homebrew Cask 安装，其他平台从 Release 获取签名 / 打包产物，也可用 Node.js 22.15+ 源码构建。单机默认无需服务器；多设备模式需要显式选择 Hub / Worker / iCloud，并配置共享 secret。headless agent 适合服务器、SSH 主机和 WSL，但应只指向受控 hub。

## 原理

- Electron widget 调用固定版本 `tokscale` 解析各工具本地 usage 数据，并按 tool / model / session / project 聚合。
- provider 限额模块可探测本地 CLI 或保存的账户集；详细 prompt / response 仅按需从本机读取，默认同步的是统计摘要。
- Hub 通过 HTTP + SSE 聚合设备快照；Worker 支持公网同步，iCloud 以每设备原子快照做最终一致聚合。
- 可选 archive 会长期保存已经观察到的每日使用量，避免源工具清理 transcript 后趋势消失。

## 价值

- 把 token、缓存、限额和真实订阅成本放到同一视图，适合做多工具用量核算与容量预警。
- 本地、LAN、自托管 Worker 和 iCloud 四种模式让用户能按数据敏感度选择同步边界。
- v0.69.0 提供测试、lint、打包与多平台发行链路，且文档明确说明网络功能和数据保留选项。

## 风险边界

- 工具需要扫描 `~/.claude`、`~/.codex` 等会话位置，并可能保存 provider key、cookie 或 token；本地优先不等于这些高价值凭据已被硬件隔离。
- `TOKEN_MONITOR_SECRET` 可留空而使 hub 无认证；公网 Worker、LAN Hub 和 headless agent 必须使用强 secret、TLS 和网络访问控制。
- 可选 session-title 同步、Discord Rich Presence、汇率 / 状态 / 更新检查和 provider limits 都会产生额外网络或元数据暴露，应逐项 opt-in。
- 本地永久 archive 与 370 天同步窗口会改变原工具的删除预期；项目名、模型、活动时间和费用本身也可能敏感。
- token / cost 解析依赖工具格式与价格表，不是供应商账单；结果应和原始 usage / invoice 抽样对账。

## 补充建议

- 先在单机本地模式运行，抽样把同一会话与 provider usage 对账，再逐步启用限额、archive 和同步。
- Hub 只绑定受控接口，配置随机 secret、TLS / VPN、最短保留期，并禁止同步标题和不必要账户字段。
- 对 release 签名、自动更新、vendored tokscale 和 Worker 部署分别做版本固定与供应链复核。

## 参考资料

- GitHub 仓库：<https://github.com/Javis603/token-monitor>
- GitHub REST API：<https://api.github.com/repos/Javis603/token-monitor>
- `v0.69.0` Release：<https://github.com/Javis603/token-monitor/releases/tag/v0.69.0>
- 隐私说明：<https://github.com/Javis603/token-monitor/blob/main/docs/privacy.md>
- 配置说明：<https://github.com/Javis603/token-monitor/blob/main/docs/configuration.md>
- Hub API：<https://github.com/Javis603/token-monitor/blob/main/docs/API.md>
- LICENSE：<https://github.com/Javis603/token-monitor/blob/main/LICENSE>
