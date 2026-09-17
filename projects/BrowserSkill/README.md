<!-- markdownlint-disable MD013 MD034 -->

# BrowserSkill：把 Agent 接到已登录浏览器的本地桥接层

> 上游仓库：https://github.com/Tencent/BrowserSkill · 归类：Agent 框架与技能生态 · 本页基于 2026-09-18 的 README、CHANGELOG、extension manifest、release、LICENSE、GitHub Trending 与 REST API 静态整理；未安装扩展，也未让 Agent 操作真实账号。

## 定位

BrowserSkill 由 `bsk` CLI / daemon、Chrome / Edge 扩展和一份 agent skill 组成。它让任何能调用 shell 的 Agent 在单独的可见 Agent Window 中操作浏览器，并可在显式借用后使用用户已有的登录态标签页。

2026-09-18 的 GitHub 官方综合 / TypeScript Trending 抓取显示约 `+1,350 stars today`；REST API 快照为 `4,070 stars / 288 forks / 51 open issues`，MIT，最新 CLI release 为 `cli-v0.3.0`（9 月 17 日），扩展 release 为 `ext-v0.3.0`（9 月 16 日）。

## 用法

上游提供浏览器商店扩展与安装脚本。正式环境应先审计脚本和 release，再分步安装：

```sh
curl -fsSL https://raw.githubusercontent.com/Tencent/BrowserSkill/main/install.sh | sh
bsk --version
bsk install-skill --harness codex --json
bsk doctor
```

随后以 `bsk session start` 建立专用窗口，用 `observe`、`click`、`fill`、`screenshot` 等命令完成任务，最后停止 session。借用普通用户标签页默认需要浏览器侧确认。

## 原理

- Agent 调用本地 `bsk`；daemon 通过 loopback WebSocket 与 Manifest V3 扩展通信。
- 扩展用 Chrome DevTools Protocol 与 WebExtension API 执行操作，专用 Agent Window 和 session 隔离引用与任务状态。
- 观察层把页面文本、控件和 `@eN` 引用转成结构化结果，避免每一步都回传完整 DOM。
- `request-help` 把登录、验证码或确认步骤交还给人；0.3.0 将借用确认与人类协助开关收回浏览器设置，旧 CLI 参数不能覆盖。
- 扩展 manifest 仍申请 `debugger`、`tabs`、`scripting`、`downloads`、`webNavigation` 与 `<all_urls>` 等广泛权限。

## 价值

- 不必为每个站点重建测试账号，可在明确借用范围内复用真实登录态。
- CLI + skill 的接口可接入多种 Agent，而不是绑定单一模型或 MCP host。
- 专用窗口、借还模型、浏览器侧开关和本地 eval corpus 提供了比无边界 CDP 脚本更清楚的执行面。
- 0.3.0 增加全页截图、远程连接、审计选项和 host-managed daemon，覆盖本地与沙箱型 Agent。

## 风险边界

- 复用真实登录态会把错误点击、恶意网页 prompt injection、越权读写和不可逆提交直接带到真实账号；“单独窗口”不是账号或权限隔离。
- `<all_urls>` 与 `debugger` 权限技术上能看到高敏感页面。skill 中“不要提取 secret”的文字约束不能替代浏览器 profile、站点账号和数据最小化。
- 关闭借用确认或启用远程 daemon 会扩大爆炸半径；设备配对、TLS、撤销、日志、端口暴露和凭据生命周期都需独立审计。
- 直接把远程 `AGENT_INSTALL.md` 或 installer 交给 Agent 执行属于高信任供应链操作，应固定 commit、校验产物并审查写入的 skill。
- 本页未运行 0.3.0，也未验证 tab 归还、扩展商店构建、远程认证、prompt injection 防护或跨浏览器兼容性。

## 补充建议

1. 新建无支付、无管理权限、无敏感 cookie 的专用浏览器 profile，并以测试账号做首轮验收。
2. 保持借用确认和人工协助开关开启，只对白名单域名与可逆动作授权；付款、发布、删除和权限变更始终人工执行。
3. 固定 CLI、extension 与 skill 版本，检查 `bsk doctor`、实际安装路径和 manifest 权限，更新后重新跑借还与停止测试。
4. 用恶意页面文本、跨标签跳转、下载、上传和 session 中断构造对抗用例，并验证操作审计不记录输入值或敏感正文。

## 参考资料

- 上游 README：https://github.com/Tencent/BrowserSkill
- 中文 README：https://github.com/Tencent/BrowserSkill/blob/main/README.zh-CN.md
- `v0.3.0` CLI release：https://github.com/Tencent/BrowserSkill/releases/tag/cli-v0.3.0
- 扩展 manifest：https://github.com/Tencent/BrowserSkill/blob/main/apps/extension/wxt.config.ts
- 架构说明：https://github.com/Tencent/BrowserSkill/blob/main/docs/architecture.md
- GitHub REST API：https://api.github.com/repos/Tencent/BrowserSkill
- LICENSE：https://github.com/Tencent/BrowserSkill/blob/main/LICENSE
