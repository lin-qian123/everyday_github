<!-- markdownlint-disable MD013 -->

# claude-mem

## 定位

Claude-mem 从 Agent 生命周期事件中捕获操作观察，以模型压缩、数据库与分层检索在后续会话补回上下文。当前除 Claude Code 插件外还有多 harness 适配、My Work 和可选托管功能；这些路径不共享完全相同的捕获、登录和数据出口。本轮在原有页面更新，没有新建同项目副本。

2026-10-31 采样：综合 / TypeScript daily +1,145 stars；API 累计 106,149 stars / 9,348 forks / 139 open issues（含 PR）。核读 main `70aa40042cfb`；发行 API 首项 [v15.7.0](https://github.com/thedotmack/claude-mem/releases/tag/v15.7.0)，2026-10-30 UTC。以下区分作者文档与有限源码核读，未做上游运行验收。

## 用法

按上游选择 `npx claude-mem install`，或在 Claude Code 内安装 marketplace / plugin 后重启：

```text
/plugin marketplace add thedotmack/claude-mem
/plugin install claude-mem
```

`npm install -g claude-mem` 仅装 SDK / library，不能代替 hooks / worker 安装。npx 安装器默认可引导账号登录和托管 observer 试用；显式 `--provider` 或 `CLAUDE_MEM_ONLINE_OPTIN=false` 可跳过账号交互，模型与 provider 仍要另行配置。当前 package engines 比 README 的“Node 20+”更严格：`^20.19.0 || >=22.12.0`，Bun `>=1.1.31`。本轮未安装或改动本机插件。

## 原理

hooks / 平台适配采集事件，本地 worker 管理 SQLite 观察与摘要，并可结合 Chroma 做检索。典型工作流为先 `search` 取紧凑索引，再 `timeline` 看上下文，最后 `get_observations` 取完整条目。压缩与召回有模型 / 检索误差，原始证据、时间和项目身份仍需保留。

## 价值

适合跨天维护代码和资料时减少重复背景说明，可按 observation ID 回到历史记录。token 节约和完成质量需在同任务、同模型、同记忆量下量化；README 的节省倍数不是本轮测试结果。

## 风险边界

- 当前根 LICENSE 与许可说明为 Apache-2.0，托管 cloud、团队 / 企业能力有独立商业边界，不能由根许可推导全部服务免费或实现都在仓库。
- telemetry 文档与 `consent.ts` 一致：匿名产品 analytics 默认开启；`DO_NOT_TRACK` 优先，再看 `CLAUDE_MEM_TELEMETRY`、telemetry.json，最后为 on。可用 `npx claude-mem telemetry disable`，但环境变量显式 on 可覆盖本地配置。
- 关闭产品统计不关闭本地日志、observer 模型请求或 Cloud Sync。文档明确本地日志保留完整细节，不走 telemetry scrubber；另有独立错误统计开关，但总 consent 关时也不发错误统计。本轮未抓包。
- 默认 worker host 为 `127.0.0.1`；远程访问、Origin / token 设置与不同只读 / 写入路由要按当前配置检查，不直接暴露数据库与 worker。
- `<private>` 标签是产品隐私控制的一环，不是对所有采集器、宿主日志或外部模型的全局保证。截图持久化、云同步和图片推理有各自 opt-in，不能混为一个开关。
- 长期记忆会过期、误归因或收进不可信指令；跨来源注入和团队共享要保留范围、删除 / 恢复能力与独立事实复核。

## 补充建议

在一次性测试会话埋入可追踪的普通 / 私密标记，分别检查捕获、压缩、召回、日志、云同步与删除后的残留。记录每个 harness 的实际 hooks / watcher、provider 和 consent 来源；同时测试旧结论被纠正后的召回，不只看“记得住”。

## 参考资料

- [上游仓库](https://github.com/thedotmack/claude-mem)、[仓库 API](https://api.github.com/repos/thedotmack/claude-mem)。
- [README.md](https://github.com/thedotmack/claude-mem/blob/70aa40042cfb8157a0d84954b9c0d2b30b50af80/README.md)。
- [LICENSE](https://github.com/thedotmack/claude-mem/blob/70aa40042cfb8157a0d84954b9c0d2b30b50af80/LICENSE)。
- [package.json](https://github.com/thedotmack/claude-mem/blob/70aa40042cfb8157a0d84954b9c0d2b30b50af80/package.json)。
- [docs/public/telemetry.mdx](https://github.com/thedotmack/claude-mem/blob/70aa40042cfb8157a0d84954b9c0d2b30b50af80/docs/public/telemetry.mdx)。
- [src/services/telemetry/consent.ts](https://github.com/thedotmack/claude-mem/blob/70aa40042cfb8157a0d84954b9c0d2b30b50af80/src/services/telemetry/consent.ts)。
- [docs/public/configuration.mdx](https://github.com/thedotmack/claude-mem/blob/70aa40042cfb8157a0d84954b9c0d2b30b50af80/docs/public/configuration.mdx)。
- [docs/license.md](https://github.com/thedotmack/claude-mem/blob/70aa40042cfb8157a0d84954b9c0d2b30b50af80/docs/license.md)。
- [docs/ip-boundary.md](https://github.com/thedotmack/claude-mem/blob/70aa40042cfb8157a0d84954b9c0d2b30b50af80/docs/ip-boundary.md)。
