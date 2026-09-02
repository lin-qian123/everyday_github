<!-- markdownlint-disable MD013 MD034 -->

# agent-browser：面向 AI agents 的 Rust 浏览器自动化 CLI

## 项目概览

- 上游仓库：https://github.com/vercel-labs/agent-browser
- GitHub API 快照（2026-09-03）：41,801 stars、2,786 forks、677 个开放 issue
- 当前 release：`v0.36.0`
- 主要技术：Rust CLI / daemon、Chrome DevTools Protocol、accessibility tree、WebMCP、MCP server
- 许可证：Apache-2.0

## 定位

agent-browser 为 coding agents 提供命令行浏览器控制：打开页面、生成带引用的 accessibility snapshot、点击/填写、截图、读取文本、连接 CDP，并可作为 MCP server 暴露核心工具。

它是浏览器执行器，不是事实核验器、账户权限系统或自动化业务审批层。`v0.36.0` 新增的 WebMCP 仍标为 experimental。

## 用法

上游支持 npm、Homebrew、Cargo 与源码构建。全局安装后需执行 `agent-browser install` 下载 Chrome for Testing：

```bash
npm install -g agent-browser
agent-browser install
agent-browser open https://example.com
agent-browser snapshot
agent-browser click @e2
agent-browser close
```

生产接入前应固定 release，使用专用 browser profile 和测试账号，不要直接复用日常浏览器的 cookies、下载目录或管理员会话。

## 原理

Rust CLI 与常驻 daemon 控制 Chrome / Chromium，优先把 accessibility tree 转成适合 agent 使用的稳定引用，再将 click、fill、read、screenshot 等动作映射到浏览器。也支持传统 selector、CDP 连接、批处理与实时 stream。

WebMCP 允许页面注册可发现工具。上游明确提示：页面提供的 description、schema、annotation 和结果都不可信；最终授权仍属于执行器和 agent host，后果性动作需要确认。

## 价值

- 用单一 CLI 覆盖浏览、抽取、截图、表单、tab、下载和状态等待。
- accessibility refs 比坐标点击更容易审阅和重放。
- 原生 Rust CLI / daemon 降低每条命令的启动开销，并支持 batch。
- 可从 CLI、MCP 或现有 agent harness 复用同一浏览器能力。

## 风险边界

- 浏览器自动化可直接发帖、下单、上传和修改账号数据；命令成功不代表业务动作正确或获授权。
- 页面内容、DOM、WebMCP schema 与下载文件均可能包含提示注入或恶意负载。
- CDP、stream、持久 session 与远程调试端口若暴露，会形成高权限控制面。
- accessibility snapshot 不能覆盖 canvas、复杂 iframe、反自动化和视觉语义的全部状态。
- 安装会下载浏览器二进制；升级命令会改变运行环境，需固定版本、校验来源并保留回滚。
- 本页依据上游 README、changelog、release 与 API，未安装，也未实测兼容性、性能或安全性。

## 补充建议

1. 用专用 profile、低权限测试账号和 allowlist 域名建立最小回归套件。
2. 对发帖、支付、删除、上传、OAuth 和下载执行前后双重确认，保存截图与响应证据。
3. 默认关闭 experimental WebMCP；启用时对 tool schema、origin、参数与输出做独立校验。
4. 将 CDP / stream 绑定在本机并限制进程访问，检查 session、截图和下载的保留期。
5. 固定 `v0.36.0`，分别测试 accessibility ref 失效、遮挡、iframe、登录过期与网络中断。

## 参考资料

- 仓库与 README：https://github.com/vercel-labs/agent-browser
- Releases：https://github.com/vercel-labs/agent-browser/releases
- 官方文档：https://agent-browser.dev/
- Changelog：https://agent-browser.dev/changelog
- WebMCP 说明：https://github.com/vercel-labs/agent-browser#webmcp-experimental
