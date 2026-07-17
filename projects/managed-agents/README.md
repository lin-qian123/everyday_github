# managed-agents

## 定位

`managed-agents` 是 SandBase 推出的本地优先、自托管 agent runtime/control plane。它不主打“写一个 agent loop”，而是补齐生产 agent 需要的 session、工具治理、审批、沙箱执行、记忆、凭据 vault、审计、事件回放和可观测控制台。

截至 2026-07-18 抓取时，仓库约 `172` stars、`7` forks，主要语言为 TypeScript。GitHub API 未识别出标准 SPDX 许可证，需要后续复核仓库许可证文件。

## 用法

快速启动：

```bash
npx managed-agents init
npx managed-agents start
```

或全局安装：

```bash
npm install -g managed-agents
managed-agents init
managed-agents start
```

默认 Dashboard 地址：

```text
http://127.0.0.1:3000/dashboard
```

要求 Node.js 22+、npm 10+，并配置模型 provider key 或本地 OpenAI-compatible endpoint。Docker 仅在需要 Docker-backed sandbox 时使用。

## 原理

项目提供 Claude Managed Agents 风格的 Console 和 `/v1` resource API，用 SQLite 存储 agents、skills、sessions、environments、credential vaults、memory stores、API keys 和 file metadata。它支持 resumable SSE session timelines、MCP toolsets、permission policies、skill packages，以及 OpenAI-compatible、Ollama-compatible、Anthropic 等模型 adapter。

## 价值

- 把 agent 运行治理从“脚本级”提升到 runtime/control plane。
- 适合企业 PoC、自托管内部 agent、客服/事件响应/研究/数据分析/软件工程 agent 的运行层实验。
- 强调 runtime state 默认放在源码仓库外，降低把密钥和会话状态误提交的风险。

## 风险边界

- 项目很新，stars 和生态验证还有限。
- 许可证状态需要人工复核，商用前不能只看 GitHub API 的 `NOASSERTION`。
- 运行时治理不等于模型输出可靠，仍需要任务级验收、权限最小化和日志脱敏。

## 补充建议

- 与 `agent-runtime`、`tupper`、`clawk`、`background-agents` 横向比较 runtime、sandbox 和团队工作流边界。
- 后续关注是否实现稳定 API、迁移工具、审计导出和多用户权限。

## 参考资料

- GitHub: <https://github.com/sandbaseai/managed-agents>
