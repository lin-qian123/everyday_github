<!-- markdownlint-disable MD013 -->

# infinity

## 定位

Infinity 是 Rust Agent runtime 与工具协议体系，面向大量并发、等待外部工具和 serverless 运行。仓库同时包含 Infinity Runtime、Reactive Agent Protocol（RAP）和 Infinity Code；三者版本与用途需分别看。

2026-10-30 快照：Rust daily +162 stars；API 累计 373 stars / 35 forks / 54 open issues（含 PR）。核读 main `1abc6fcff1f1`；发行 API 首项 [sandbox-remote-v0.2.0](https://github.com/hydro-project/infinity/releases/tag/sandbox-remote-v0.2.0)，2026-10-22 UTC。以下为文档与有限源码核读，未安装运行。

## 用法

官方 quickstart 用 Amazon Bedrock，先创建普通 Rust 二进制项目：

```bash
cargo new my-agent
cd my-agent
```

按固定 quickstart 添加 infinity-agent-core = "0.2"、infinity-provider-bedrock = "0.2" 与 Tokio，配置自己的 Bedrock 身份和模型权限后复制完整示例。示例使用 InMemoryConversationStore / InMemoryStateStore；重启恢复需要另接持久化存储。本文不把简短示例写成可直接生产部署的服务，也未调用模型。

## 原理

输入、工具返回、子任务报告和定时唤醒统一为消息。一次 slice 加载状态、去重、调用模型、持久化 turn，然后分派工具并让出执行；RAP 通过回调送回结果。同步工具可在 slice 内完成并继续模型循环。同一会话按 FIFO 串行，不同会话并发；AWS 路径使用 SQS FIFO 的 group_id。

## 价值

适合慢工具、多并发会话和弹性队列：等待期间不必持续占用执行进程。对已有 MCP 的兼容层可以降低工具迁移成本，但需验证传输、鉴权和调用语义。

## 风险边界

- 根 Apache-2.0。发行首项 sandbox-remote-v0.2.0 是组件标签，不代表整个 runtime 的统一稳定版本。
- README 的 Raspberry Pi 75k agents 属作者容量表述；休眠会话数量不等于同时推理吞吐、可用内存零开销或模型费用为零。
- 持久化历史与 processed-ID 去重处理重复投递，不能单凭设计说明保证发邮件 / 扣费等外部动作 exactly-once；仍需工具幂等键、事务出箱或可恢复的动作状态。
- 同会话 FIFO 是正确性前提，替换队列或存储时不能只测吞吐。内存 store 与持久 store 的故障语义不同。
- RAP 的 callback_url、远端工具、云队列、存储和模型都需要独立身份与最小权限；并发框架不自动形成 OS 隔离。
- 长工具等待可让进程释放，但推理、冷启动、状态装载、队列和回调仍有时延 / 成本。

## 补充建议

用 mock 模型和带幂等键的假工具做重复消息、乱序、超时、dispatch 后崩溃、回调重放和取消测试，再接真实持久 store。分别测休眠会话占用、活跃推理并发、端到端 P99 与每任务成本。

## 参考资料

- [上游仓库](https://github.com/hydro-project/infinity)、[仓库 API](https://api.github.com/repos/hydro-project/infinity)。
- [README.md](https://github.com/hydro-project/infinity/blob/1abc6fcff1f186124f924b56aa92c3a3684c90c5/README.md)。
- [docs/docs/infinity-runtime/architecture.md](https://github.com/hydro-project/infinity/blob/1abc6fcff1f186124f924b56aa92c3a3684c90c5/docs/docs/infinity-runtime/architecture.md)。
- [docs/docs/infinity-runtime/quickstart/launching-your-first-agent.md](https://github.com/hydro-project/infinity/blob/1abc6fcff1f186124f924b56aa92c3a3684c90c5/docs/docs/infinity-runtime/quickstart/launching-your-first-agent.md)。
- [LICENSE.txt](https://github.com/hydro-project/infinity/blob/1abc6fcff1f186124f924b56aa92c3a3684c90c5/LICENSE.txt)。
