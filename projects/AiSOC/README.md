<!-- markdownlint-disable MD013 -->

# AiSOC

## 定位

AiSOC 是自托管的安全运营辅助平台：把安全遥测归一化，执行规则检测与事件关联，再由 Agent 调查、写入 Investigation Ledger 并提出响应。定位是分析员 copilot，实际覆盖取决于接入的数据源与规则字段。

2026-10-30 快照：Python daily +318 stars；API 累计 5,133 stars / 540 forks / 11 open issues（含 PR）。核读 main `8ebedd2fcf3f`；发行 API 首项 [v20.2.1](https://github.com/beenuar/AiSOC/releases/tag/v20.2.1)，2026-10-28 UTC。以下为文档与有限源码核读，未安装运行。

## 用法

在独立测试环境审阅固定版本的 Makefile / Compose 后，按上游入口启动：

```bash
git clone https://github.com/beenuar/AiSOC
cd AiSOC
make doctor
make up
make smoke
```

主线文档要求 Docker Compose v2、Docker VM 至少 8 GB 内存 / 20 GB 空闲磁盘，以及 Python 3.9+ 和 bash；首次下载约 2 GB 模型。make up 生成部署密钥与管理员凭据。先走标记为 sample / synthetic 的内置样本，再使用有授权的只读日志源。以上命令未在本轮运行。

## 原理

文档描述的主路径是 ingest → Kafka → fusion / correlation → Postgres alert → 本地模型 triage → 证据账本；full profile 再增加事件湖与图等组件。Agent 使用 typed tools，调查输出保留提示、工具调用、引用与 token 成本。响应 playbook 默认 preview，部署、租户和 playbook 三层开关共同控制启用，审批可持久暂停。

## 价值

把告警依据、调查过程和动作建议连到可追查记录，适合研究告警分流、分析员复核和响应治理。规则可达性、模型输出格式可靠性、检测准确率和实际处置效果是四种不同验收。

## 风险边界

- 根许可 MIT。README 当前列 7,015 条规则、2,530 条可执行规则；均为上游计数，本轮没有重数或回放。可执行只说明特定事件能触发，不能推导真实攻击召回率。
- README 自述本地模型路径已有测量、托管 provider 未实测；50 条告警的格式可用性不是独立准确率评测。
- Reality 文档仍保留 2026-09-23 / v8.1.0 审计头和“live-agent 路径未核”的旧段落，且夹有后续修复记录。不能将该页当作 v20.2.1 的统一验收清单；与当前 README 的差异需按版本追证。
- 部署和合成演示不构成生产可靠性证据；日志保留、迁移、跨租户隔离、真实 vendor 连接和重启恢复须独立验证。
- 默认本地推理不代表所有组件离线：模型下载、CISA KEV、vendor connector 或另选云模型均可能联网。
- 响应工具可能隔离终端或改变账号状态；审批与 capability contract 的文档声明尚未经本轮负面测试。

## 补充建议

用脱敏历史事件做按时间隔离的回放，记录规则覆盖、误报、漏报、引用准确率和人工复核耗时。再用 stub vendor 检查审批人职责分离、越权拒绝、重启恢复和审计导出；将上游自测与自己的验收结果分栏。

## 参考资料

- [上游仓库](https://github.com/beenuar/AiSOC)、[仓库 API](https://api.github.com/repos/beenuar/AiSOC)。
- [README.md](https://github.com/beenuar/AiSOC/blob/8ebedd2fcf3fa9a6af1761a5c1000a644b1548b8/README.md)。
- [docs/audit/REPOSITORY_REALITY.md](https://github.com/beenuar/AiSOC/blob/8ebedd2fcf3fa9a6af1761a5c1000a644b1548b8/docs/audit/REPOSITORY_REALITY.md)。
- [LICENSE](https://github.com/beenuar/AiSOC/blob/8ebedd2fcf3fa9a6af1761a5c1000a644b1548b8/LICENSE)。
