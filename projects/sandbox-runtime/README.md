<!-- markdownlint-disable MD013 -->

# sandbox-runtime：命令与 MCP 的 OS 文件及网络约束

- 主上游：[anthropics/sandbox-runtime](https://github.com/anthropics/sandbox-runtime)；repository ID `1079560616`。
- 采样日期：2026-10-25（Asia/Shanghai）；分类：Agent 框架与技能生态。
- API 累计快照：6,455 stars / 568 forks / 304 open issues（含 PR 口径）；与榜单日增分开。
- 默认分支 `main`，本页静态依据固定在 `c66fb77b28fdbea8b9788aca72377238ae67ca20`。发行列表首项 `v0.0.81`，发布于 2026-10-20T01:01:41Z（正式）。
- 核验层级：直接读取上游文档、许可、元数据和下列部分实现；未安装运行、调用模型或复现性能。

## 定位

Anthropic Sandbox Runtime（srt）是可作为 CLI 或库使用的进程约束工具，面向 Agent、MCP server 和任意命令。README 仍标为 Beta Research Preview。主线描述 macOS sandbox-exec、Linux bubblewrap / namespace，以及 Windows 专用账户、受限 token / ACL / WFP 路线；各平台不是等价实现。

## 用法

主线 package.json 要求 Node >=22.12.0；Linux 还需按上游说明准备 bubblewrap 等依赖。安装入口和显式配置方式如下，本轮未执行：

```bash
npm install -g @anthropic-ai/sandbox-runtime
srt --settings ./srt-settings.json "pwd"
```

先把配置写到宿主控制的位置，明确 network.allowedDomains、filesystem.denyRead / allowRead、allowWrite / denyWrite；不要直接复制 README 中展示成功的 curl 或敏感文件示例来推断自己机器的默认行为。还应将 srt 安装位置放在被沙箱进程可写目录之外。

## 原理

OS 文件与进程规则配合宿主代理实施网络出口策略，Linux 通过移除网络 namespace 的直接出口迫使进程走代理。读权限默认允许，通过 denyRead 收窄并可局部 allowRead；写与网络主要采用显式允许。CLI 初始列表为空，另有少量运行路径写入例外。Unix socket、DNS 解析地址、TLS 终止与凭据注入分别配置，不能用单一“已沙箱”状态概括。

## 价值

可以把自然语言层面的“不要读取、不要联网”转成可观察的系统拒绝，适合为本地 MCP / shell 建立更小权限面。价值应由允许样本、拒绝样本、实际进程与网络证据验证，不能用安装成功代替隔离验收。

## 风险边界

允许 github.com 等宽域名仍可能外传数据，域名过滤不等于内容过滤。Docker socket、可写 PATH / shell 配置、srt 自身安装路径会扩大权限；Linux 弱嵌套与 macOS 弱网络选项会降低隔离。主线特别说明 allowAppleEvents 可启动在沙箱外运行的应用，移除代码执行隔离。Windows 的机器级设置和 token / 系统服务例外须独立评估。此处为静态文档与 CLI 核验，没有攻击测试或平台安全认证。根许可证 Apache-2.0。

## 补充建议

固定版本，在临时账户里测试密钥目录读取、项目允许写入、禁止路径、受限域名、解析到内网地址和本地 socket；逐平台保留拒绝证据。尽量不启用弱化选项；变更策略后检查是否需要重建进程，避免以为热更新覆盖了所有 OS 规则。

## 参考资料

- [README.md](https://github.com/anthropics/sandbox-runtime/blob/c66fb77b28fdbea8b9788aca72377238ae67ca20/README.md)。
- [package.json](https://github.com/anthropics/sandbox-runtime/blob/c66fb77b28fdbea8b9788aca72377238ae67ca20/package.json)。
- [src/cli.ts](https://github.com/anthropics/sandbox-runtime/blob/c66fb77b28fdbea8b9788aca72377238ae67ca20/src/cli.ts)。
- [src/sandbox/sandbox-config.ts](https://github.com/anthropics/sandbox-runtime/blob/c66fb77b28fdbea8b9788aca72377238ae67ca20/src/sandbox/sandbox-config.ts)。
- [LICENSE](https://github.com/anthropics/sandbox-runtime/blob/c66fb77b28fdbea8b9788aca72377238ae67ca20/LICENSE)。
- [仓库 API](https://api.github.com/repos/anthropics/sandbox-runtime)、[发行 API](https://api.github.com/repos/anthropics/sandbox-runtime/releases?per_page=3)；动态元数据只代表本轮采样。
- 事实来源为以上固定文件；价值、风险评估和验证建议为本库工程判断，未作为上游实测结果。
