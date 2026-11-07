<!-- markdownlint-disable MD013 -->

# AutoRAG Agent：原位检索与整理个人文件的 Librarian 引擎

- 上游：[Marker-Inc-Korea/AutoRAG](https://github.com/Marker-Inc-Korea/AutoRAG)；仓库 ID：`741450201`。
- 快照：2026-11-08（Asia/Shanghai）；stars / forks / open issues（含 PR）：5,402 / 486 / 68；官方 daily 榜 TypeScript +40，不是自然日结算。
- 分类：RAG、检索与知识处理；最新发行：[v2.13.6](https://github.com/Marker-Inc-Korea/AutoRAG/releases/tag/v2.13.6)（UTC 2026-11-05 17:40:51，非预发行标记）。
- 核读基线：`main@8e777148835909de116410fa712ea3d4a2322b0e`。以下为文档与抽样源码核读，作者声明与本轮运行验证分开。

## 定位

当前 AutoRAG 2.x 是基于 Pi 的个人知识 / 文件 Agent，可联合检索本地文档、邮件、聊天和笔记，回到原始来源读证据并生成引用，也能整理文件。原 Python RAG AutoML / pipeline 优化器迁到 `legacy/`，仍维护；`pip install AutoRAG` 安装的是旧工具，不是当前 Agent。

## 用法

当前 npm 引擎名为 `@autorag/librarian`，要求 Node.js 24+，也提供 Bun 路径。先在仅含复制件的小目录中评估：

```bash
npm install -g @autorag/librarian@2.13.6
autorag init
autorag status --json
autorag tui --permission-mode ask
```

在 TUI 中用 `/login`、`/model` 选择 provider 和模型，配置检索根目录后按文档准备索引。setup / 首次使用可能安装 MinSync、filee-cli、解析 / 转换引擎和模型；不是一个无需联网依赖的单包。CLI `search` 与消息桥接默认权限不同，勿直接复用 TUI 的默认假设。本轮未执行安装、登录或索引。

## 原理

Pi 承载模型会话、工具、凭据和会话持久化；AutoRAG 组织原位数据源、MinSync 稀疏 / 向量 / 混合检索、Jikji 文件发现、来源直读与回答复核。检索记忆保存被模型判断支持回答的证据，作为后续参考，不能取代当前原始来源。文件镜像、索引与历史对话仍是需要治理的派生副本。

## 价值

对跨文件、聊天和邮件的问答可保留来源身份，减少手工搬运到单一知识库。可从 TUI、CLI、TypeScript API 或 Lite MCP 接入。但“已索引”“搜得到”“引用支持结论”和“修改正确”须分别核验；不能仅因输出带引用就认为事实可靠。

## 风险边界

- 权限文档写 TUI 默认 `auto`，而 `autorag search` 及 Telegram / Discord / WhatsApp TUI 默认 `full`。auto 可由 Jev 静默批准认为已获授权的修改；`ask` 也不是 OS sandbox，外部 MCP 工具不在该 gate 内。
- 本地 embedding 不等于全流程离线：回答模型、decision model、可选远端 embedding / rerank 和各数据连接器各有出口。Jev 判断会使用用户对话、工具调用与路径存在信息；脱敏是上游设计声明，未抓包验证。
- 主线在会话首问探测 decision model，并可回退到配置的小模型；两者都不可用则停止。不要把 README 较早的“无 Jev 后端照常审批”描述扩大为所有当前搜索可用性。
- 文件整理拥有 bash / write / edit；先用副本、明确权限模式、限制工作目录，并审查自动化和远端消息入口。
- 本仓库引擎与 legacy 均 Apache-2.0；Dazzi 桌面应用另仓使用 FSL-1.1-MIT，外部工具也保留各自许可，不能把整套产品统一写成 Apache。
- 未运行 retrieval、权限绕过、云连接、文件变更或隐私验证，未独立复现作者质量 / 性能结论。

## 补充建议

用有金标的问题集检查命中、引用和“没有证据”响应，再测改名、复制、撤销及重索引。记录每个数据源、provider、自动下载和后台进程；共享设备需审查索引、记忆、会话和云占位文件下载范围。需要纯检索时先评估 Lite MCP 的工具面，仍须限制其 refresh 和数据读取范围。

## 参考资料

- [README.md](https://github.com/Marker-Inc-Korea/AutoRAG/blob/8e777148835909de116410fa712ea3d4a2322b0e/README.md)
- [package.json](https://github.com/Marker-Inc-Korea/AutoRAG/blob/8e777148835909de116410fa712ea3d4a2322b0e/package.json)
- [docs/permissions.md](https://github.com/Marker-Inc-Korea/AutoRAG/blob/8e777148835909de116410fa712ea3d4a2322b0e/docs/permissions.md)
- [src/agent/permission-gate.ts](https://github.com/Marker-Inc-Korea/AutoRAG/blob/8e777148835909de116410fa712ea3d4a2322b0e/src/agent/permission-gate.ts)
- [src/agent/decision-model-check.ts](https://github.com/Marker-Inc-Korea/AutoRAG/blob/8e777148835909de116410fa712ea3d4a2322b0e/src/agent/decision-model-check.ts)
- [LICENSE](https://github.com/Marker-Inc-Korea/AutoRAG/blob/8e777148835909de116410fa712ea3d4a2322b0e/LICENSE)
- [GitHub API 快照](https://api.github.com/repos/Marker-Inc-Korea/AutoRAG)；[发行列表](https://github.com/Marker-Inc-Korea/AutoRAG/releases)。
