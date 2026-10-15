<!-- markdownlint-disable MD013 -->

# Beads / bd（gastownhall/beads）中文解读

> 上游仓库：<https://github.com/gastownhall/beads> · 归类：记忆层与个人 AI 基础设施 · 证据快照：2026-10-16（Asia/Shanghai）。API：27,916 stars / 1,890 forks / 1,463 open issues；MIT；稳定 Release `v1.3.1`；tags 首项 `v1.3.2-rc.2`。本页为上游文档与相关源码的静态整理，未安装运行、接入真实数据 / 凭据、复测性能或完成全面安全审计。

## 定位

Beads 是面向 Coding Agent 的依赖图 issue tracker 和持久任务记忆，以 `bd` CLI 和 Dolt 版本化数据库保存任务、依赖、领取、关闭与项目事实。它适合跨 session 恢复长任务状态，把“接下来能做什么”显式表达为图查询。

## 用法

从上游 Release 核验 checksum 后安装，或按文档用 `brew install beads`。先在测试仓库执行 `bd init`；注意默认会修改 / 创建 `AGENTS.md` 并安装宿主集成，试用时可选 `bd init --stealth`。日常从 `bd ready`、`bd show <id>` 到 `bd update <id> --claim`、`bd close <id>`；`bd remember` / `bd prime` 用于保存和注入项目事实。

## 原理

- 以依赖关系计算 ready work，原子 claim 降低多个执行者重复领取的机会；hash ID 减少标识碰撞，不能消除语义冲突。
- main README 当前区分默认 embedded 单 writer 与外部 Dolt server 多 writer；通过 Dolt remote push / pull 同步。
- 分支 / merge / history 保存数据演进；压缩旧任务减少上下文占用，`--json` 给 Agent 稳定结构化入口。
- experimental HTTP backend 允许远端访问，但与本地后端有明确操作差异，需阅读 divergence ledger。

## 价值

- 阻塞、优先级、任务领取和来源历史比散落对话更容易查询，适合需要续跑的工程任务。
- 图结构能把一个任务完成后解锁的后续工作显式列出；项目 memory 可与宿主的个人偏好分开。
- 版本化数据库提供恢复与协作基础，但任务关闭仍需要真实测试和产物证据。

## 风险边界

- 数据和配置中的部分 tracker token 可为明文，Git / Dolt history 也不是加密；不应把秘密或私人用户数据放入 issue / memory。
- SECURITY.md 提醒 Dolt 默认上传 usage metrics；关闭依赖遥测可用 `DOLT_DISABLE_EVENT_FLUSH=1` 或 `dolt config --global --add metrics.disabled true`，实际出站仍需验证。
- 外部 issue / memory 是不可信文本，结构化输出和终端控制符过滤不等于消除给模型的 prompt injection。
- main README、稳定二进制与 SECURITY.md 对 storage / network 的描述存在代际差异；尤其不能沿用“无监听端口”概括当前 experimental HTTP / server 模式。
- 升级可能触发 schema migration；JSONL export 不是数据库真源或完整备份。上游同时警告 issue / PR 评论中的 fix ZIP 恶意附件，GitHub 托管域名不等于受信制品。

## 补充建议

- 固定 `v1.3.1`，先核对该 tag 的帮助与文档，再在可丢弃仓库验证 create → dependency → claim → close → backup / restore。
- 多人升级指定一个迁移者，先导出与备份再迁移 / push，其余 clone 更新并 bootstrap；不直接跳过 schema guard。
- 明确 embedded / server / HTTP 的写者数量、认证和 TLS；用同一组任务验证各模式语义，外部同步与 hooks 单独审阅。

## 参考资料

- 上游仓库：<https://github.com/gastownhall/beads>
- GitHub REST API：<https://api.github.com/repos/gastownhall/beads>
- README / 最新模式说明：<https://github.com/gastownhall/beads/blob/main/README.md>
- 入门文档：<https://github.com/gastownhall/beads/blob/main/docs/getting-started/quickstart.md>
- 安全与依赖隐私：<https://github.com/gastownhall/beads/blob/main/SECURITY.md>
- Dolt 后端说明：<https://github.com/gastownhall/beads/blob/main/docs/architecture/dolt.md>
- HTTP 差异清单：<https://github.com/gastownhall/beads/blob/main/engdocs/design/http-divergence-ledger.md>
- LICENSE：<https://github.com/gastownhall/beads/blob/main/LICENSE>
- Releases：<https://github.com/gastownhall/beads/releases>
