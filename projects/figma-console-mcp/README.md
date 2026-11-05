<!-- markdownlint-disable MD013 -->

# figma-console-mcp（southleft/figma-console-mcp）

- 更新：2026-11-06（Asia/Shanghai）；官方 TypeScript daily +242，为读取快照，不是自然日结算。
- GitHub API：3,136 stars / 286 forks / 9 open issues（含 PR）；仓库 ID `1070285775`。
- 核读基线：`5ef4df3791606b8e1f877557ec0dde4796250b44`；文档与抽样实现核验，不是安装运行、安全或性能认证。

## 定位

Southleft 维护的 Figma MCP 服务，以设计 token、组件、变量和状态为结构化接口，支持读取、写入及设计与代码的一致性检查。它是独立社区项目，不能与 Figma 官方 MCP 的权限和功能混为一谈。当前 manifest 与稳定发行均为 1.46.0。

## 用法

1. 先选连接模式：NPX / 本地 Git 提供完整工具；Cloud Mode 需配对 Desktop Bridge 才能写；Remote SSE 提供只读子集。README 的 130 / 105 工具是当前版本说明，不是跨版本保证。
2. 本地模式需 Node.js 18+、Figma Desktop、MCP 客户端和相应 Figma PAT。参考 README 配置服务，建议把其滚动 `@latest` 示例固定为 `figma-console-mcp@1.46.0`。
3. 服务启动后，在 Figma Desktop 导入 `~/.figma-console-mcp/plugin/manifest.json` 并运行插件；桥接扫描 9223–9232。先在文件副本读取状态，再试单个 frame 写入。
4. 升级时分别核服务器和桥插件版本；Figma 可能缓存插件，是否重导入需看对应 release 的要求。

本轮没有配置 PAT、安装 MCP 或修改 Figma 文件。

## 原理

本地服务通过 stdio 与 Agent 通信，Desktop Bridge 经 WebSocket 在 Figma 插件上下文执行读写；文件、版本等能力也使用 Figma REST API。Cloud Mode 经云端配对与中继提供写操作；代码库提取等部分能力仅本地可用。1.46.0 新增 shader、布局、色彩和文字等能力，不能由工具注册数量直接推断设计质量。

## 价值

对已有设计系统的团队，明确的 token / variant / binding 比截图猜样式更便于审查；可重复的 parity 和 accessibility 检查也有工程价值。确定性检查只覆盖其规则和输入，不保证所有交互、响应式、视觉审美或完整 WCAG 合规。

## 风险边界

- **本地模式仍有网络**：安全文档开头写“零外部调用”，后文却明确列出 `api.figma.com`；应理解为本地传输与避免厂商中继，而非离线。MCP 客户端 / 云模型仍可能外发读取的设计内容。
- **PAT 与插件范围不同**：文档明确 PAT 可访问该账户能访问的文件，无法缩到单一文件；插件写入当前打开文件不代表整个服务只能读一个文件。配置中的 token 应按敏感凭据保护。
- **localhost 不是账户隔离**：WebSocket 默认本地绑定、无独立用户认证；抽样源码有 Origin 白名单，同时接受缺省 / null Origin。可选 HTTP 默认关闭，可配 bearer token。这里只核机制，未复现攻击或验证隔离强度。
- **云模式另核数据流**：安全文档称无遥测 / 设计持久化；这是上游声明，Cloudflare 代理、OAuth 和第三方 AI 客户端仍需分别评估。MIT 许可也不赋予设计素材的再分发权。

## 补充建议

在专用测试账户 / 文件副本验证读取范围、错误文件写入、撤销 PAT、断连恢复、桥插件版本和 token 同步删除。设计验收同时看原生 Figma 对象、生成代码、交互和人工视觉结果；保留规则报告，但不要把评分当完整产品验收。

## 参考资料

- [README.md](https://github.com/southleft/figma-console-mcp/blob/5ef4df3791606b8e1f877557ec0dde4796250b44/README.md)
- [package.json](https://github.com/southleft/figma-console-mcp/blob/5ef4df3791606b8e1f877557ec0dde4796250b44/package.json)
- [docs/security.md](https://github.com/southleft/figma-console-mcp/blob/5ef4df3791606b8e1f877557ec0dde4796250b44/docs/security.md)
- [src/core/websocket-server.ts](https://github.com/southleft/figma-console-mcp/blob/5ef4df3791606b8e1f877557ec0dde4796250b44/src/core/websocket-server.ts)
- [仓库与 API 快照](https://api.github.com/repos/southleft/figma-console-mcp)；[发行列表](https://github.com/southleft/figma-console-mcp/releases)。
- [发行 v1.46.0](https://github.com/southleft/figma-console-mcp/releases/tag/v1.46.0)。
