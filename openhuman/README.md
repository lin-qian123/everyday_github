# openhuman

## 项目定位

- GitHub：<https://github.com/tinyhumansai/openhuman>
- 定位：本地优先（local-first）的个人 AI 助手平台，强调“长期记忆 + 工具集成 + 桌面体验”。
- 当前信号（2026-05-16 抓取）：约 8.9k stars，近期进入 GitHub Trending AI 讨论区。

## 用法

1. 官网下载桌面安装包：<https://tinyhumans.ai/openhuman>
2. 或终端安装（macOS/Linux）：

```bash
curl -fsSL https://raw.githubusercontent.com/tinyhumansai/openhuman/main/scripts/install.sh | bash
```

3. Windows（PowerShell）：

```powershell
irm https://raw.githubusercontent.com/tinyhumansai/openhuman/main/scripts/install.ps1 | iex
```

## 原理

- **UI-first 交互层**：以桌面界面作为主入口，降低纯终端门槛。
- **记忆树（memory tree）**：将用户上下文和外部连接数据持续组织，支撑跨会话任务连续性。
- **集成层**：声明支持 Gmail、Notion、GitHub、Slack 等工具连接，形成 agent 工具调用面。

## 价值

- 适合希望把“个人工作上下文”持续沉淀到本地环境的用户。
- 对比一次性聊天型助手，更强调长期任务链与跨日协作。

## 风险边界

- 项目仍是早期 Beta，接口和行为可能频繁变化。
- 大量第三方连接会引入权限管理复杂度，需要最小权限原则。
- “全能助手”叙事容易高估实际稳定性，需通过真实工作流验证。

## 补充建议

- 优先用低风险场景试运行（文档整理、日报、代码检索）。
- 建立集成白名单，逐步放开高敏感权限。
- 将关键自动化输出保留可审计日志，避免隐式错误扩散。

## 参考资料

- GitHub 仓库：<https://github.com/tinyhumansai/openhuman>
- 文档：<https://tinyhumans.gitbook.io>
- 官网：<https://tinyhumans.ai/openhuman>
