<!-- markdownlint-disable MD013 -->

# It's a Plan

> 更新：2026-10-20（Asia/Shanghai）。分类：办公、商业与行业应用。上游 `croffasia/itsaplan`；快照 `9258bb683516`（main）。本文基于官方榜单、认证 API 与上游文件静态研究；热度、版本时间与跨平台证据见[当日日报](../../daily/2026-10-20/ai-hotspots.md)。

## 定位

自托管项目管理与 issue tracker，包含看板、周期、自定义字段、文档、仪表盘、REST / webhook / MCP。人和 Agent 使用同一套成员、任务与分配机制；不启用 Agent 也能作为任务系统使用。[README.md](https://github.com/croffasia/itsaplan/blob/9258bb683516a56f1aa5ed62d9c3a7929f01e0ed/README.md)

## 用法

本地体验需要 Docker 与 Bun；按上游流程执行 `bun install` 后运行 `bun run setup` 并选择 `Try it`。脚本选择空闲端口、生成 secrets 并启动 Docker 栈，README 示例入口为 localhost:3001。生产部署另读 self-hosting / Railway 文档，不能直接照搬体验环境。[README.md](https://github.com/croffasia/itsaplan/blob/9258bb683516a56f1aa5ed62d9c3a7929f01e0ed/README.md)

内置 Agent 配模型与工具；外部 Agent 通过 `@itsaplan/runner` 在自己的机器接任务。不同 CLI 必须依照 runner 文档接入 MCP 凭据和会话续接，不能只替换可执行文件名。[docs/runner.md](https://github.com/croffasia/itsaplan/blob/9258bb683516a56f1aa5ed62d9c3a7929f01e0ed/docs/runner.md)

## 原理

Bun / Elysia 后端、Next.js 前端、Postgres、对象存储与 Mastra 内部 Agent 组成服务；提及、分配和调度可启动一次 run。外部 runner 拉取队列、调用编码 CLI，将过程与结果流回任务 / 聊天；工具 API 与仓库系统集成把修改映射回项目状态。[README.md](https://github.com/croffasia/itsaplan/blob/9258bb683516a56f1aa5ed62d9c3a7929f01e0ed/README.md)[docs/runner.md](https://github.com/croffasia/itsaplan/blob/9258bb683516a56f1aa5ed62d9c3a7929f01e0ed/docs/runner.md)

## 价值

将“分配给 Agent”纳入团队已有任务记录，使负责人、任务上下文、运行与交付有共同入口；适合评估跨 CLI 工单自动化和自托管协作。任务状态更新不等于代码通过验收，吞吐和人力节省仍需独立量化。

## 风险边界

- 外部 runner 继承本机账户与 CLI 权限。文档当前 Claude 预设使用 `--permission-mode auto`，Codex 用 `sandbox_mode="workspace-write"`，Antigravity 则用 `--dangerously-skip-permissions`；不能声称全部 backend 逐动作人工批准或有同一种沙箱。[docs/runner.md](https://github.com/croffasia/itsaplan/blob/9258bb683516a56f1aa5ed62d9c3a7929f01e0ed/docs/runner.md)
- 遥测默认开启：worker 启动即发送，随后每日快照，失败有重试。包括随机实例 ID、版本、功能开关、区间计数和失败比例等；文档声明不发标题、正文、凭据。设 `TELEMETRY_DISABLED=1` 或 `DO_NOT_TRACK=1` 可关闭。自托管不等于没有出站。[TELEMETRY.md](https://github.com/croffasia/itsaplan/blob/9258bb683516a56f1aa5ed62d9c3a7929f01e0ed/TELEMETRY.md)
- MCP / API key、公开分享链接、webhook、外部集成与模型 provider 有各自权限和数据出口；角色分配不构成外部 CLI 的 OS 隔离。[README.md](https://github.com/croffasia/itsaplan/blob/9258bb683516a56f1aa5ed62d9c3a7929f01e0ed/README.md)[.env.example](https://github.com/croffasia/itsaplan/blob/9258bb683516a56f1aa5ed62d9c3a7929f01e0ed/.env.example)
- 主体 AGPL-3.0，`packages/runner` 例外为 Apache-2.0；商业许可另议。最新 Release 为 `v1.5.0`，但主 README 仍保留首次稳定版前可能 breaking 的提醒，应视为文档状态差异，不能仅凭版本数字推断迁移无风险。[README.md](https://github.com/croffasia/itsaplan/blob/9258bb683516a56f1aa5ed62d9c3a7929f01e0ed/README.md)[LICENSE](https://github.com/croffasia/itsaplan/blob/9258bb683516a56f1aa5ed62d9c3a7929f01e0ed/LICENSE)[packages/runner/LICENSE](https://github.com/croffasia/itsaplan/blob/9258bb683516a56f1aa5ed62d9c3a7929f01e0ed/packages/runner/LICENSE)

## 补充建议

用一次性项目 / 目录测分配、拒绝、取消、断线续接与实际文件改动；对每个 CLI 分别记录启动参数、有效审批模式和允许目录。把数据库 / 对象存储备份、schema 迁移、API key 撤销、遥测开关与 webhook 重放纳入上线验收。本轮只读研究，没有启动栈或 runner。

## 参考资料

- [README.md](https://github.com/croffasia/itsaplan/blob/9258bb683516a56f1aa5ed62d9c3a7929f01e0ed/README.md)
- [LICENSE](https://github.com/croffasia/itsaplan/blob/9258bb683516a56f1aa5ed62d9c3a7929f01e0ed/LICENSE)
- [packages/runner/LICENSE](https://github.com/croffasia/itsaplan/blob/9258bb683516a56f1aa5ed62d9c3a7929f01e0ed/packages/runner/LICENSE)
- [TELEMETRY.md](https://github.com/croffasia/itsaplan/blob/9258bb683516a56f1aa5ed62d9c3a7929f01e0ed/TELEMETRY.md)
- [docs/runner.md](https://github.com/croffasia/itsaplan/blob/9258bb683516a56f1aa5ed62d9c3a7929f01e0ed/docs/runner.md)
- [.env.example](https://github.com/croffasia/itsaplan/blob/9258bb683516a56f1aa5ed62d9c3a7929f01e0ed/.env.example)
- [仓库 API](https://api.github.com/repos/croffasia/itsaplan)
- [v1.5.0 Release](https://github.com/croffasia/itsaplan/releases/tag/v1.5.0)
