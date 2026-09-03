<!-- markdownlint-disable MD013 MD034 -->

# Portless：为人和 Agents 提供稳定本地域名的开发代理

## 项目概览

- 上游仓库：https://github.com/vercel-labs/portless
- GitHub API 快照（2026-09-04）：12,046 stars、394 forks、125 个开放 issue
- 当前 release：`v0.15.6`，仍为 pre-1.0
- 主要技术：TypeScript CLI、本地 reverse proxy、`.localhost`、HTTPS/HTTP2、worktree/monorepo 路由
- 许可证：Apache-2.0

## 定位

Portless 用稳定、可命名的本地 URL 替代不断变化的端口，例如把 `localhost:3000` 变成 `https://myapp.localhost`。这既方便人类记忆，也让 browser/coding agents 在重启 dev server 或切换 worktree 后仍可使用稳定地址。

它是本地开发网络层工具，不是 agent 本身、身份认证系统或生产 ingress。

## 用法

可全局或项目内安装：

```bash
npm install -g portless
portless myapp next dev
# https://myapp.localhost
```

Portless 会分配空闲端口、注入 `PORT` 或已知 framework 的端口参数，并通过本地代理转发。monorepo 可用一个 `portless.json` 管理多个 app；linked worktree 默认获得分支名前缀子域名。

## 原理

CLI 启动本地 proxy，把 app 名称注册到随机端口。默认只监听 `127.0.0.1` / `::1`，使用本地 CA 提供 HTTPS 与 HTTP/2；路由按 hostname 选择目标进程。项目、package 和 Git worktree 信息用于推导稳定名称。

可选 LAN、Tailscale、Funnel、ngrok、自定义 TLD 与开机服务会扩大访问面。默认 loopback 边界一旦显式切换共享模式就不再成立。

## 价值

- agent 和测试脚本可引用稳定 URL，减少端口漂移导致的上下文和配置错误。
- worktree 自动子域名降低并行分支 dev server 冲突。
- monorepo 的多个服务可用可读 hostname 组织，而不必维护端口表。
- HTTPS/HTTP2、WebSocket 和常见前端框架适配覆盖现代本地开发场景。

## 风险边界

- 首次启用 HTTPS 会创建并信任本地 CA；证书私钥、信任范围和卸载清理必须核验。
- macOS/Linux 绑定 443 与开机服务可能使用 sudo/root；安装到系统服务不是无副作用操作。
- `--lan`、Tailscale、Funnel、ngrok 或自有域名可把开发服务暴露给更多主体，认证不能由友好 hostname 代替。
- 自动注入端口参数只覆盖已识别命令；复杂 script、env 前缀和自定义 runner 可能保持原端口。
- pre-1.0 状态目录和行为可能变化，团队成员版本不一致会造成路由或信任漂移。
- 本页依据上游 README、release 与 API，没有安装 CA、启动 proxy 或测试跨平台兼容。

## 补充建议

1. 先用 `--no-tls` 或可丢弃 profile 验证路由，再决定是否信任本地 CA。
2. 团队固定 `v0.15.6` 或 package lock，并把 app 名称、TLD 和共享模式写进项目配置。
3. 默认保持 loopback；启用 LAN/Funnel 前增加应用认证、最小防火墙和退出清理测试。
4. 对 OAuth、cookies、CORS、WebSocket 与 worktree 名称做端到端测试，不只看首页能否打开。
5. 记录 `portless clean` / service uninstall 后的证书、hosts、launchd/systemd 和状态目录残留。

## 参考资料

- 仓库与 README：https://github.com/vercel-labs/portless
- Releases：https://github.com/vercel-labs/portless/releases
- 官方站点：https://portless.sh/
- npm 包：https://www.npmjs.com/package/portless
- Git worktree 说明：https://github.com/vercel-labs/portless#git-worktrees
