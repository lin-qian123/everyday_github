<!-- markdownlint-disable MD013 -->

# agent-browser：用快照引用驱动浏览器的 Rust CLI

- 上游：[vercel-labs/agent-browser](https://github.com/vercel-labs/agent-browser)；仓库 ID：`1132001614`。
- 快照：2026-11-08（Asia/Shanghai）；stars / forks / open issues（含 PR）：46,780 / 3,207 / 500；官方 daily 榜 综合 / Rust +180，不是自然日结算。
- 分类：Agent 框架与技能生态；最新发行：[v0.41.2](https://github.com/vercel-labs/agent-browser/releases/tag/v0.41.2)（UTC 2026-11-03 23:46:27，非预发行标记）。
- 核读基线：`main@370d41db67a198944bcee2c96cc454594e7d56c6`。以下为文档与抽样源码核读，作者声明与本轮运行验证分开。

## 定位

agent-browser 让 Agent 从 Shell 打开网页、取得 accessibility snapshot，并按 `@e1` 一类引用操作元素；也提供 stdio MCP、技能和其他引擎 / provider。它是浏览器执行器，页面上的授权、数据真实性与业务动作结果仍由宿主工作流判断。本页以稳定 0.41.2 与当前主线文档为基线。

## 用法

在专用环境固定版本，首次安装浏览器后再操作无账号测试页面：

```bash
npm install -g agent-browser@0.41.2
agent-browser install
agent-browser --session demo open https://example.com
agent-browser --session demo snapshot -i
agent-browser --session demo get url
agent-browser --session demo close
```

click / fill 使用刚取得的引用；导航或 DOM 改变后重新 snapshot。每条命令显式传同一 session。CLI 内置 `skills get core`，0.41.2 支持 `skills get core --ref commands` 按需取参考；MCP 工具和客户端须核对对应版本。本轮没有安装或实际控制浏览器。

## 原理

CLI 把命令发给按 session 独立运行的 daemon，daemon 通过 CDP 控制浏览器并在命令间保留页面。快照将当时的可访问性结构压缩为文本与元素引用；引用不是永久 locator。引擎、CDP 附着、iOS 和云浏览器有不同控制能力，不能把某一 Chromium 路径的保证套到所有 provider。

## 价值

适合把浏览、读取、表单、截图、下载和等待组织成可审阅命令，并让 Agent 按读取结果继续。0.41.2 修复 timeout 导致的 session 重启、裸 open 丢 profile 等问题；0.41.0 修复 MCP 参数夹带全局 flag 的路径，并调整 eve 工具名。旧集成应先看迁移，不直接替换二进制就宣告兼容。

## 风险边界

- 主线安全文档明确：导航、动作与输出限制默认需主动开启；自动发现的项目配置则只允许安全键子集。浏览器登录态仍能执行发布、上传、支付或删除等实际操作。
- `--allowed-domains` 约束浏览器路径，不是 OS 防火墙；与 CDP / auto-connect、profile、状态恢复及 iOS / Safari 等组合会被拒绝。需要白名单时用受支持的独立 Chromium session，并核对实际配置组合。
- 页面内容 / WebMCP 工具和下载文件仍不可信，content boundary 依赖宿主正确处理；WebSocket / EventSource 部分阻断为 best-effort，eval 会扩大能力。
- 凭据插件是本地可执行程序，未被 sandbox；云 provider 还有独立数据出口与启动时机。会话、截图、下载、auth vault 与本地加密 key 都需保护。
- 0.41.2 新增 Chrome CVE 提醒，但不阻断命令、云 provider 不检查；联网失败可能无提醒，可用 `AGENT_BROWSER_NO_VERSION_CHECK=1` 关闭该检查请求。无 warning 不表示浏览器安全。
- 根许可 Apache-2.0；当前 main 的安全说明与具体发行功能须分别验证。未执行兼容性、策略绕过、真实账号或 WebMCP 测试。

## 补充建议

升级先在测试页面核对 session 连续性、引用失效、遮挡、登录过期、MCP 工具名与参数。按需要设置 action policy、confirmation、内容标记和域名限制，逐项确认 backend 支持；对发帖、付款、删除、上传建立业务授权与动作后证据。记录浏览器版本和实际网络约束，截图 / 快照成功不能替代完整视觉与业务验收。

## 参考资料

- [README.md](https://github.com/vercel-labs/agent-browser/blob/370d41db67a198944bcee2c96cc454594e7d56c6/README.md)
- [docs/content/docs/security.mdx](https://github.com/vercel-labs/agent-browser/blob/370d41db67a198944bcee2c96cc454594e7d56c6/docs/content/docs/security.mdx)
- [LICENSE](https://github.com/vercel-labs/agent-browser/blob/370d41db67a198944bcee2c96cc454594e7d56c6/LICENSE)
- [GitHub API 快照](https://api.github.com/repos/vercel-labs/agent-browser)；[发行列表](https://github.com/vercel-labs/agent-browser/releases)。
- [v0.41.0 工具迁移与 MCP 参数修复](https://github.com/vercel-labs/agent-browser/releases/tag/v0.41.0)。
