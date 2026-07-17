# waku-agent

## 定位

`waku-agent` 是一个个人本地 AI agent 教学/实用项目，强调用可阅读的 Python 代码展示 Harness、Loop、Memory、Eval / LLM-Ops，而不是把关键逻辑藏在大型框架后面。

截至 2026-07-18 抓取时，仓库约 `269` stars、`71` forks，主要语言为 Python，许可证为 `MIT`。

## 用法

README 给出的快速启动：

```bash
git clone https://github.com/ShenSeanChen/waku-agent
cd waku-agent
uv venv
uv pip install -e .
uv run waku
uv run waku dashboard
```

`uv run waku dashboard` 会启动本地浏览器 cockpit，默认地址为 `localhost:7777`。项目还支持 Telegram bot token，把本地 agent 接到聊天入口。

## 原理

项目围绕本地 agent loop 展开：用户输入进入 harness，agent 通过记忆层、工具、评估/观测逻辑和模型调用完成一轮任务。它强调“在自己机器上运行”，并用 dashboard 帮助用户理解每一轮 agent 执行。

## 价值

- 适合作为学习本地 agent 架构的代码读本。
- 把 memory、eval 和 dashboard 放在一个轻量项目里，便于快速实验。
- 对想从“调用 LLM API”迈向“可运行个人 agent”的开发者有实践价值。

## 风险边界

- 教学和个人实验属性强，不能默认具备生产级权限治理、安全沙箱和长期稳定 API。
- 接入 Telegram 或外部模型时，仍需自行处理 token、隐私和日志。
- README 提到视频 walkthrough，长期可用性依赖外部平台。

## 补充建议

- 可与 `learn-agent`、`hello-agents`、`agent-runtime` 对照：前者偏教学，后者偏 runtime 抽象。
- 后续关注是否补充更系统的测试、离线 mock、权限策略和 MCP 示例。

## 参考资料

- GitHub: <https://github.com/ShenSeanChen/waku-agent>
- YouTube walkthrough: <https://www.youtube.com/watch?v=rvRyBhILrls>
