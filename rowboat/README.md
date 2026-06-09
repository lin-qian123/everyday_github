# Rowboat（RowboatX）

Rowboat 是 Rowboat Labs 开源的本地优先（local-first）AI coworker/Agent OS。它提供一个“可在本机后台长期运行”的智能体环境，支持定时任务、MCP 工具接入、文件/命令行协作与多模型配置，适合做持续性的研究、数据收集、写作与运维自动化。

## 核心能力
- **后台长期运行**：智能体可以在后台持续工作，支持定时与触发式任务。
- **MCP 工具生态**：可接入 MCP server，让智能体调用文件、浏览器、数据库等工具。
- **本地优先**：数据与状态尽量保留在本地，强调可控性与可审计。
- **多模型配置**：支持配置多模型与路由策略，按任务选择模型。
- **任务与日志管理**：提供任务执行与日志追踪，便于回溯与复盘。

## 原理概述（非实现细节）
1. **Agent 运行时**：提供一个长期运行的 Agent 运行时，负责调度、任务队列与状态持久化。
2. **工具层（MCP）**：通过 MCP 协议把外部能力变成可调用工具（如文件操作、浏览器自动化）。
3. **模型层**：用配置文件管理模型（API Key、provider、默认模型），任务按配置路由。
4. **任务编排**：支持定时任务与手动触发，适合周期性工作流。

## 快速开始

### 1) 运行 RowboatX CLI
```bash
npx @rowboatlabs/rowboatx@latest
```

### 2) 配置模型
RowboatX 通过本地配置文件管理模型信息（如 OpenAI、Anthropic 等），按需填写 API Key 与默认模型。

### 3) 添加 MCP 工具（可选）
可以在 RowboatX 内添加 MCP server，让智能体具备更多外部能力。

## 可视化界面（Rowboat Studio）
官方提供基于 Docker 的 Rowboat Studio，用于查看与管理任务/智能体：
```bash
./start.sh
```
然后访问：
```
http://localhost:3000
```

## 典型使用场景
- 资讯/情报收集与日报生成
- 代码与文档的持续维护
- 运行长周期的数据清洗/抽取
- 智能体驱动的运营、监控与自动化

## 资源链接
- GitHub: https://github.com/rowboatlabs/rowboat
- README: https://github.com/rowboatlabs/rowboat/blob/main/README.md
- RowboatX CLI: https://github.com/rowboatlabs/rowboat#rowboatx
- Rowboat Studio: https://github.com/rowboatlabs/rowboat#rowboat-studio
