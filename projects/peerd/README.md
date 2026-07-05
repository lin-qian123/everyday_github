# peerd

## 1. 定位

`peerd` 是一个浏览器原生 AI agent harness，以 Chrome/Firefox 扩展形式运行完整
agent loop。它的目标是让 agent 在用户已有浏览器环境中读取和操作页面，同时使用
浏览器安全模型隔离 API key、页面内容、WebAssembly VM、JS notebook 和客户端应用。

它适合归入 `前端、UI 与 Agent 交互层`：重点不是模型本身，而是把浏览器变成 agent
运行时、权限边界和交互界面。

## 2. 基本用法

当前主要安装方式是开发者预览：

```bash
git clone https://github.com/NotASithLord/peerd.git
cd peerd
```

然后在 Chrome 中打开 `chrome://extensions`，启用 Developer mode，选择仓库中的
`extension/` 目录作为 unpacked extension。首次运行时需要创建本地 vault，并配置
Anthropic、OpenRouter 或本地 Ollama 等模型入口。

README 明确标注项目仍是 `0.x experimental beta`，存储格式和接口可能变化。

## 3. 核心原理

peerd 把浏览器本身作为 runtime 和 security model：

- API key 存在本地 vault 中，由 service worker 持有和把关。
- 每个 tab、VM、notebook、app 由独立 actor agent 驱动。
- 主 agent 更像 orchestrator，只接收被标记为 untrusted 的摘要。
- 页面动作会回报真实 navigation 或 mutation summary，用观察到的效果判断成功。
- 预览通道还探索 WebRTC peer-to-peer agent 通信和 dweb 应用共享。

这种设计试图降低 prompt injection 从页面内容直接触达密钥和高权限工具的风险。

## 4. 工程价值

浏览器是用户真实工作的主入口，也是 web agent 最难处理的执行环境。peerd 的价值在于
把 browser-use 类能力、客户端 sandbox 和 BYOK 模型调用放到同一个扩展里，避免所有
页面内容都先上传到第三方后端。

它也给 agent 安全设计提供了一个可观察样本：主 agent、actor agent、vault、service
worker 和页面 actor 之间的边界比普通“浏览器自动化 + LLM”更清晰。

## 5. 风险边界

peerd 需要宽泛浏览器权限，并会驱动真实页面。即便项目强调无后端、无 telemetry，
用户仍需理解扩展权限、模型 provider 数据流和本地 vault 的恢复机制。

项目仍处于 0.x beta，不能直接用于高价值账号、生产后台或敏感网页。对企业环境来说，
还需要审查扩展签名、更新渠道、权限策略和日志留存。

## 6. 补充建议

- 先用独立浏览器 profile 和测试账号试用。
- 打开动作确认，避免 agent 自动操作真实账户。
- 对网页 prompt injection、表单提交和文件下载场景做专门测试。
- 与 `browser-use`、`cua`、`Agent-S`、`chrome-devtools-mcp` 对比，观察浏览器原生
  harness 是否能成为 GUI agent 的长期形态。

## 7. 参考资料

- GitHub 仓库：<https://github.com/NotASithLord/peerd>
- 官网：<https://peerd.ai>
- 许可证：Apache-2.0
