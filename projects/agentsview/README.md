# agentsview（kenn-io/agentsview）

- GitHub: https://github.com/kenn-io/agentsview
- 官网: https://agentsview.io
- 记录日期: 2026-06-16 (Asia/Shanghai)

## 定位

`agentsview` 是面向 AI coding agent 的本地优先可观测层，用来统一查看会话、搜索历史、统计 token 使用量和估算成本。它更像“agent 时代的本地 usage / observability 控制台”，而不是单一模型聊天工具。

## 热度信号

1. GitHub 仓库页在 2026-06-16 抓取时约有 `2,674 stars`、`237 forks`。
2. GitHub Trending Go 页面当天出现该项目，说明“agent 使用分析”已经从个人脚本走向产品化工具。
3. GitHub API 显示仓库在 `2026-06-16` 仍有推送更新，项目活跃度较高。

## 用法

### 1) 本机安装

```bash
curl -fsSL https://agentsview.io/install.sh | bash
```

或直接使用桌面版 / Docker。

### 2) 启动本地 Web UI

```bash
agentsview serve
```

默认会在 `http://127.0.0.1:8080` 打开界面，并从本机已支持的 agent 会话目录自动建索引。

### 3) 查每日成本

```bash
agentsview usage daily
agentsview usage daily --breakdown
agentsview usage daily --agent claude --since 2026-04-01
```

## 原理

1. 首次运行时扫描多种 agent 的本地会话目录，并统一写入本地 SQLite。
2. `usage` 子命令直接对已索引数据库做查询，因此比每次重扫原始 JSON 日志更快。
3. UI 层把会话搜索、usage 统计、模型维度拆分和成本估算放到同一个本地面板里。
4. 官方还提供 DuckDB、PostgreSQL 和 Quack 等模式，方便多机聚合或远程查看。

## 价值

- 对同时使用 Claude Code、Codex、OpenCode、Forge 等多工具的人很实用。
- 能把“这个月到底烧了多少钱、哪个模型最贵、哪个 agent 最常用”变成可直接查询的事实。
- 本地优先路线对隐私敏感用户更友好，也更适合个人工作站。

## 风险边界

- 它依赖读取本地 agent 会话目录，因此访问权限和数据保留策略要事先想清楚。
- 成本估算依赖模型价格表与日志完整性，适合做运维判断，不适合当财务结算依据。
- 若通过反向代理或公网暴露 UI，必须额外处理 Host 校验、认证和访问控制。

## 补充建议

1. 用它做团队共享面板时，优先走只读镜像或数据库复制，而不是直接共享原始会话目录。
2. 给高成本模型单独建告警或日报，避免“感觉没用多少”但实际超支。
3. 把 usage 报表和项目产出一起看，别把 token 节省误当作唯一目标。

## 参考资料

- https://github.com/kenn-io/agentsview
- https://agentsview.io
- https://github.com/trending/go
