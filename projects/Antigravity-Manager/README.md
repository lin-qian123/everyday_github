<!-- markdownlint-disable MD013 -->

# Antigravity-Manager：账户管理、模型路由与协议代理

- 上游：[lbjlaq/Antigravity-Manager](https://github.com/lbjlaq/Antigravity-Manager)，仓库 ID `1104535633`；本页新增于 2026-11-26。
- 快照：34,039 stars / 3,604 forks / 1,711 open issues（累计，含 PR）；Rust daily +134。
- 版本：稳定 `v5.0.4`（2026-11-20 16:25 UTC），与默认 main SHA `9b6dfc107df6076f114ad2bb516ba54c69aea784` 相同；另有 `v5.0.5-beta.2`（11-25 07:45 UTC），SHA `c4468142eea3f92b8c3a40768e7ae3d5b36d343b`。API pushed_at 更新不代表默认分支已包含 beta 修复。
- 范围：README、发行说明与指定源码静态核读；未安装、读取用户凭据、切换账户、启动代理或调用模型。

## 定位

项目在界面中称 Antigravity Tools，以 Tauri / Rust 后端和 React 前端统一账户、配额、客户端切换及 OpenAI / Anthropic / Gemini 协议入口。它适合研究多客户端适配与请求调度，提供的是账户和协议管理层，不是新的模型。

README 描述将已有会话接入本地代理；协议兼容、账户服务授权和模型真实身份应分别确认。赞助链接中的价格和渠道宣传不是本轮验证结果。

## 用法

先选稳定或预发行通道，核对 tag、制品来源和原账户配置备份，再阅读官方安装步骤。本轮没有执行安装脚本、关闭系统安全检查或导入 token。

建议先在专用测试用户中查看账户和路由配置，明确是否启用代理及日志；尚未需要代理时保持关闭。客户端接入必须使用当前配置中的实际地址和 key，不能照抄 README 的演示凭据。

已自行启动并核对监听范围后，可从健康检查开始；以下仅为示意，未执行：

```bash
curl --fail http://127.0.0.1:8045/healthz
```

健康响应只证明该端点可达。Docker 文档将 `API_KEY` 用于模型请求，独立 `WEB_PASSWORD` 用于管理后台；未设置后者时可回退到 API key。容器发布端口、宿主防火墙与应用的 LAN / auth 开关须一同检查。

## 原理

- **账户与配额。** 账户池维护 token、配额与异常状态，调度器选择账户并处理重试。重试、换号和配额百分比不保证请求只执行一次或最终账单正确。
- **协议与模型映射。** 同一入口可转换客户端协议并重新映射模型 ID，后台任务还可降档。客户端显示的模型名不能独立证明实际模型、上下文或输出约束。
- **本机代理。** 稳定版 `ProxyConfig::default` 为 `enabled=false`、`auto_start=false`、`allow_lan_access=false`、端口 8045、`auth_mode=auto`。文档定义 auto 在本机模式等效 off，LAN 模式等效 all_except_health；随机生成 key 不代表每种模式都会校验 key。
- **状态与审计。** 稳定版账户路径读取 `accounts/{id}.json`；`Account` 包含 `TokenData`，后者直接含 access / refresh token 字符串。保存路径将对象序列化为 JSON，再交给原子文件写入函数。这条已查路径未见应用层加密；原子写入用于完整性，不提供加密。

## 价值

工程价值在于统一账户状态、协议差异、故障恢复和模型路由的观察入口。稳定发行说明涉及截断与结束标志、调度和客户端状态同步，适合据此建立可复现的失败案例。

上游关于“消除降智”“完全兼容”“稳定交付 JSON”的措辞仍属作者声明；协议转换是否保留工具调用、缓存与终止语义，要用目标客户端的固定请求核对。

## 风险边界

| 议题 | 已核事实与边界 |
| --- | --- |
| 修复所在版本 | beta.2 发行说明列出静态资源后缀鉴权绕过、OAuth 状态 / HTML 转义和 URL 凭据脱敏修复。稳定版 auth 文件仍有后缀静态资源判断，并将其纳入健康豁免；beta 文件已移除此判断。不能把 beta 修复归入 v5.0.4；本轮未做路由利用或安全复测。 |
| 凭据说明漂移 | README 声称账户加密存于 SQLite，但所查稳定路径为包含 token 的 JSON 原子写入。不要据宣传认定所有账户文件加密；应检查目标版本的目录权限、备份与系统磁盘保护。 |
| 日志与保留 | 稳定版 `enable_logging=true`；实验配置默认 payload 模式 simple、日志 30 天、thinking store 开启且保留 15 天。开关不证明所有请求均落盘，也不证明已脱敏；实际内容和清理需另验。 |
| 本机与共享部署 | 默认代理关闭；启用后 auto + 本机模式不要求请求 key，管理面另有规则。反向代理、端口发布与共享主机不能仅靠界面中的“本地”描述判断隔离。 |
| 账户与服务 | 软件许可不授予第三方服务账户、会话转 API 或再分发权限；连接前核自己的授权与服务约定，不把配额轮换当服务承诺。 |
| 许可 | API 标 NOASSERTION，实际 LICENSE 为 CC BY-NC-SA 4.0，包含非商业及相同方式共享条件；不能按 MIT 或无限制商业软件选型。 |

## 补充建议

1. 固定稳定 / beta tag 与客户端版本，在配置副本中记录导入、切换、重启、回退前后的文件差异。
2. 用模拟上游检查 401 / 429、截断、重复重试、JSON 与工具调用；将网关 token 统计与真实账单分开。
3. 共享使用前独立验证管理密码、请求 key、拒绝路径、日志脱敏与删除周期；beta 修复声明需要目标部署复验。
4. 把账户 token、同步导出与备份视为凭据材料，先核落盘格式和访问者，再决定接入范围。

## 参考资料

- [仓库 API](https://api.github.com/repos/lbjlaq/Antigravity-Manager)、[稳定 v5.0.4](https://github.com/lbjlaq/Antigravity-Manager/releases/tag/v5.0.4)、[预发行 beta.2](https://github.com/lbjlaq/Antigravity-Manager/releases/tag/v5.0.5-beta.2)。
- [固定中文 README](https://raw.githubusercontent.com/lbjlaq/Antigravity-Manager/9b6dfc107df6076f114ad2bb516ba54c69aea784/README_ZH.md)、[认证模式](https://raw.githubusercontent.com/lbjlaq/Antigravity-Manager/9b6dfc107df6076f114ad2bb516ba54c69aea784/docs/proxy/auth.md)、[Docker 文档](https://raw.githubusercontent.com/lbjlaq/Antigravity-Manager/9b6dfc107df6076f114ad2bb516ba54c69aea784/docker/README.md)。
- [稳定配置默认值](https://raw.githubusercontent.com/lbjlaq/Antigravity-Manager/9b6dfc107df6076f114ad2bb516ba54c69aea784/src-tauri/src/proxy/config.rs)、[稳定鉴权](https://raw.githubusercontent.com/lbjlaq/Antigravity-Manager/9b6dfc107df6076f114ad2bb516ba54c69aea784/src-tauri/src/proxy/middleware/auth.rs)、[beta.2 鉴权](https://raw.githubusercontent.com/lbjlaq/Antigravity-Manager/c4468142eea3f92b8c3a40768e7ae3d5b36d343b/src-tauri/src/proxy/middleware/auth.rs)。
- [账户写入](https://raw.githubusercontent.com/lbjlaq/Antigravity-Manager/9b6dfc107df6076f114ad2bb516ba54c69aea784/src-tauri/src/modules/account.rs)、[Account 数据结构](https://raw.githubusercontent.com/lbjlaq/Antigravity-Manager/9b6dfc107df6076f114ad2bb516ba54c69aea784/src-tauri/src/models/account.rs)、[TokenData](https://raw.githubusercontent.com/lbjlaq/Antigravity-Manager/9b6dfc107df6076f114ad2bb516ba54c69aea784/src-tauri/src/models/token.rs)、[原子写入](https://raw.githubusercontent.com/lbjlaq/Antigravity-Manager/9b6dfc107df6076f114ad2bb516ba54c69aea784/src-tauri/src/utils/fs.rs)、[LICENSE](https://raw.githubusercontent.com/lbjlaq/Antigravity-Manager/9b6dfc107df6076f114ad2bb516ba54c69aea784/LICENSE)。
