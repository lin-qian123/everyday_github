# VibeTunnel

概览
VibeTunnel 是一个将任意终端在 Web 上“安全暴露”的工具。它会在本地启动一个 Web 客户端并通过隧道连接，让你在浏览器里访问本地终端，适合远程操作与临时分享。

核心能力
- 本地终端 -> Web：将本地终端映射为可访问的 Web UI。
- 安全隧道：通过隧道降低公网暴露风险。
- 轻量部署：安装后即可启动。

原理与架构（基于公开说明的归纳）
VibeTunnel 在本地启动终端代理与 Web 服务器，通过隧道层完成端到端连接，使浏览器访问与本地终端会话保持同步。

快速上手
- 安装：
  - `brew install vibetunnel`
- 启动：
  - `vibetunnel`

使用场景
- 远程终端访问与演示。
- 临时共享本地终端给协作者。

参考链接
- https://github.com/steipete/vibetunnel
- https://vt.sh/
