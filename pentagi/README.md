# PentAGI（vxcontrol/pentagi）项目速览与上手指南

- GitHub: https://github.com/vxcontrol/pentagi
- 更新日期: 2026-04-01（Asia/Shanghai）

## 1. 为什么今天值得跟踪

`PentAGI` 是近期 GitHub 日榜里讨论度很高的 AI 安全工具：把“任务规划 + 工具调用 + 结果沉淀”做成可持续运行的渗透测试 Agent 系统。

- 热度信号（2026-04-01 抓取）:
  - GitHub 仓库页：`14k stars`、`1.7k forks`
  - GitHub Trending 镜像（zdoc）：`1,309 stars today`

## 2. 项目在做什么（核心定位）

官方定位是 `Fully autonomous AI Agents system capable of performing complex penetration testing tasks`。

它不是单个“AI 扫描脚本”，而是一个完整的自托管 Agent 系统，核心包括：

1. 自动化渗透流程
- Agent 自动分解任务、调用工具、推进攻击链与验证过程。

2. 专业工具集成
- 内置 20+ 安全工具（README 提到 nmap、metasploit、sqlmap 等），用于侦察、枚举、利用、验证。

3. 记忆与知识图谱
- 支持长期记忆沉淀；可选 Graphiti + Neo4j 追踪语义关联，减少重复探索。

4. 可观测与 API 化
- 提供 Web UI、REST、GraphQL、Grafana/Prometheus 观测能力，适合团队化与流水线集成。

## 3. 怎么用（快速上手）

## 3.1 环境要求（官方 Quick Start）

- Docker / Docker Compose（也支持 Podman 配置）
- 最低 `2 vCPU`
- 最低 `4GB RAM`
- 约 `20GB` 可用磁盘

## 3.2 最小部署

```bash
mkdir pentagi && cd pentagi
curl -o .env https://raw.githubusercontent.com/vxcontrol/pentagi/master/.env.example
curl -O https://raw.githubusercontent.com/vxcontrol/pentagi/master/docker-compose.yml
docker compose up -d
```

默认访问：`https://localhost:8443`（README 给出默认账户 `admin@pentagi.com / admin`，建议首次登录后立刻修改）。

## 3.3 API 调用方式

- GraphQL 入口：`/api/v1/graphql`
- REST 入口：`/api/v1/flows`
- 认证方式：`Authorization: Bearer <API_TOKEN>`

示例（GraphQL）：

```bash
curl -X POST https://your-pentagi-instance:8443/api/v1/graphql \
  -H "Authorization: Bearer YOUR_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"query": "{ flows { id title status } }"}'
```

## 4. 原理是什么（工程视角）

1. Agent 编排层
- 系统将“渗透测试”拆成可机读的多步骤流程：目标理解 -> 侦察 -> 利用尝试 -> 证据收集 -> 报告产出。

2. 工具执行层
- 通过容器隔离执行命令与第三方工具，避免把 Agent 直接暴露在宿主系统。

3. 记忆/知识层
- 把历史命令输出、发现路径、有效 payload 存档（PostgreSQL + 可选图谱），让后续任务复用历史上下文。

4. 观测与评估层
- 借助日志与指标（Langfuse/Grafana 等可选栈）追踪 Agent 决策链，便于回放与调优。

## 5. 适用场景

- 红队/攻防演练中的自动化侦察与重复性验证。
- 安全研究中对“LLM Agent + 工具链”协作能力做实验。
- 内网安全平台原型：需要 API 化接入 CI/CD 或工单系统。

## 6. 风险与边界

1. 合法合规前置
- 仅应在获得授权的目标上使用；未经授权测试可能违法。

2. 幻觉与误判不可忽略
- Agent 仍可能给出错误推理或危险动作，必须设置人工审查与执行边界。

3. 默认口令与暴露面
- 演示配置默认账户仅适合本地测试；生产环境必须更换口令、最小暴露端口并强化审计。

## 7. 信息来源

- 项目仓库（README / Quick Start / API / 架构）: https://github.com/vxcontrol/pentagi
- GitHub Trending 镜像（today stars）: https://www.zdoc.app/en/trending
