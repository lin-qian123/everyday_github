<!-- markdownlint-disable MD013 -->

# lightpanda-browser

- 上游：[lightpanda-io/browser](https://github.com/lightpanda-io/browser)；分类：前端、UI 与 Agent 交互层。
- 核读：2026-11-01（Asia/Shanghai）；初次收录：2026-03-16；固定主线 `49d717daba2c694ef1f02889ea49ca02fbb881a6`。
- [仓库 API](https://api.github.com/repos/lightpanda-io/browser) 快照：39,197 stars / 1,905 forks / 103 open issues（含 PR）；发行首项 [1.0.2](https://github.com/lightpanda-io/browser/releases/tag/1.0.2)，2026-10-23 UTC。发行与主线分别看。
- 证据：上游文档及指定文件静态核读；本轮未安装运行、调用模型或复现作者实验。

## 定位

从头用 Zig 构建的无头浏览器，组合 V8、libcurl、html5ever 与 DOM，面向 AI Agent 和网页自动化。保留原目录 `lightpanda-browser`，本轮原位刷新 3 月说明。官方综合 daily 榜本轮显示 +929 stars。

当前主线已含 CDP、WebDriver BiDi、原生 Agent、MCP 和 PandaScript。它优先网页操作与数据提取，PNG / PDF dump 的文本渲染不等于 Chromium 的完整视觉结果。

## 用法

当前 README 的 macOS 入口是 Homebrew nightly：

```bash
brew install lightpanda-io/browser/lightpanda
lightpanda version
LIGHTPANDA_DISABLE_TELEMETRY=true lightpanda fetch --obey-robots --dump markdown https://example.com
LIGHTPANDA_DISABLE_TELEMETRY=true lightpanda serve --obey-robots --host 127.0.0.1 --port 9222
```

Puppeteer 用 `browserWSEndpoint: "ws://127.0.0.1:9222"` 接入；原生 MCP 可用 `lightpanda mcp`（stdio），HTTP 示例为 `lightpanda mcp --host 127.0.0.1 --port 9223`。README 的 Docker 当前入口是 `lightpanda/browser`，端口映射到 `127.0.0.1`；原页的旧 GHCR 示例不再作为推荐。

记录实际 binary version 和下载来源。发行首项是 1.0.2，但 Homebrew / latest / nightly 可能跟随不同主线；本页主线功能不能无条件套给 1.0.2。Linux 预编译制品的 glibc 下限，README 当前写 x86_64 2.35、arm64 2.38；Alpine / Android Bionic 不能直接照搬。

## 原理

浏览器自身执行 JS / DOM，通过协议或内置工具控制导航、点击、填表和提取。内置 Agent 用所选模型做决策，`/save` 可导出 PandaScript，再用 `lightpanda run` 重放；脚本无需模型 token，但仍访问网络和处理动态网页，不能保证业务结果每次相同。

HTTP MCP 按 `Mcp-Session-Id` 路由独立浏览会话；相同 ID 可共享 cookies / 页面状态。当前源码拒绝带 Origin 的请求，并检查 Host，但这些浏览器来源防护不是用户认证，session ID 也不是身份凭证。

## 价值

提供从模型探索到可重放脚本的路径，适合抽取、批量操作和确定步骤的自动化。README 展示约 16 倍峰值内存差异、9 倍时间差异，说明对应 AWS m5.large、真实页面抓取基准；这些是作者特定 workload 的数字，本轮没有重跑。

## 风险边界

- CDP / MCP 控制面可操作网页与登录状态；保持 loopback / Unix socket，远程服务需另加认证、网络边界和任务权限。会话隔离不能代替多租户授权。
- 默认发送 usage telemetry；`LIGHTPANDA_DISABLE_TELEMETRY=true` 可关闭。主线源码实际上按环境变量是否存在判定，并在 debug build 中关闭；示例统一显式设 true，避免误解 false 字符串。
- 事件结构包含运行、导航类型、工具来源 / 结果 / 时长、MCP 客户端类型、模型 provider / model 等元数据。关闭此统计不关闭所选云模型或目标网页的请求；本轮未抓包验证。
- 网页 API 与完整视觉兼容性须按目标站点实测；`--obey-robots` 是显式选项，能打开网页不代表被授权采集或执行交易。
- 根许可 AGPL-3.0，嵌入 / 修改 / 提供网络服务时需按实际用法检查义务；主线构建文档要求 Zig 0.17.0，勿套旧版本依赖。

## 补充建议

选 20 个授权目标页，对照 Chromium 核提取字段、表单事件、cookie 隔离、失败恢复和真实资源占用；涉及视觉必须另看截图与交互。把最新 X 的单场景 demo、README 抓取 benchmark 和第三方视频标题分开比较，固定网页、脚本、版本及硬件后再谈加速倍数。

## 参考资料

- [固定 README / 安装、功能与作者基准](https://github.com/lightpanda-io/browser/blob/49d717daba2c694ef1f02889ea49ca02fbb881a6/README.md)。
- [主线配置与监听参数](https://github.com/lightpanda-io/browser/blob/49d717daba2c694ef1f02889ea49ca02fbb881a6/src/Config.zig)。
- [MCP 会话及来源校验](https://github.com/lightpanda-io/browser/blob/49d717daba2c694ef1f02889ea49ca02fbb881a6/src/mcp/HttpServer.zig)。
- [遥测开关与事件定义](https://github.com/lightpanda-io/browser/blob/49d717daba2c694ef1f02889ea49ca02fbb881a6/src/telemetry/telemetry.zig)。
- [遥测发送实现](https://github.com/lightpanda-io/browser/blob/49d717daba2c694ef1f02889ea49ca02fbb881a6/src/telemetry/lightpanda.zig)。
- [AGPL-3.0 许可](https://github.com/lightpanda-io/browser/blob/49d717daba2c694ef1f02889ea49ca02fbb881a6/LICENSE)。
