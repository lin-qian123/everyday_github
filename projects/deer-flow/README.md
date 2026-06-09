# bytedance/deer-flow

## 项目简介
[bytedance/deer-flow](https://github.com/bytedance/deer-flow) 是一个面向深度研究（Deep Research）场景的开源项目，核心目标是把“复杂问题研究流程”拆解成可执行的多智能体协作流水线。项目基于 `LangGraph` 构建，用流程图（节点/边）组织研究任务，让 Agent 可以进行检索、规划、执行和结果汇总。

## 为什么今天值得关注
- 在 GitHub Trending（Python）中进入前列，显示 **17,400+ stars**，且出现 **今天 +696 stars** 的增长信号。
- 与“单轮对话式助手”不同，deer-flow 主打“研究流程化”，符合近期 AI Agent 从“聊天”走向“任务编排”的趋势。

## 它怎么用（实操）

### 1. 本地运行 Web UI（推荐）
```bash
# 方式 A：克隆后用 uv 管理依赖
git clone https://github.com/bytedance/deer-flow.git
cd deer-flow
uv sync
cp .env.example .env
# 编辑 .env，填入模型/API 配置
uv run main.py
```

```bash
# 方式 B：无需克隆，直接运行（uvx）
uvx deer-flow@latest
```

### 2. 作为 MCP Server 接入到你的 Agent/IDE
示例（Claude Code）：
```json
{
  "mcpServers": {
    "deer-flow": {
      "command": "uvx",
      "args": ["deer-flow@latest", "--mcp"]
    }
  }
}
```

### 3. Docker 方式
```bash
docker compose up
```

## 核心原理（工作机制）
1. **图式编排（Graph-based Orchestration）**
   使用 LangGraph 把研究流程拆成可复用节点（如检索、阅读、总结、反思），节点之间按状态机路由。
2. **多智能体协作**
   不同 Agent 角色分工处理任务（信息收集、证据整合、结论产出），比单 Agent 更稳定。
3. **MCP 生态接入**
   通过 MCP 暴露工具能力，便于被外部助手调用，形成“研究能力即服务”。
4. **可观测与可扩展**
   项目结构围绕工作流扩展，便于插入新工具（搜索、知识库、执行器）和新节点。

## 适合人群
- 需要做“研究型任务”的开发者（调研报告、竞品分析、技术方案比选）。
- 想把 Agent 从 Demo 走向生产流程的团队。
- 需要 MCP 方式集成研究能力的工程团队。

## 风险与注意点
- 多智能体流程更强，但配置复杂度和调试成本也更高。
- 输出质量高度依赖模型能力和检索数据质量。
- 在企业场景需补齐权限控制、审计和敏感数据治理。

## 参考链接
- GitHub: https://github.com/bytedance/deer-flow
- 官方文档: https://deerflow.tech/
- Hugging Face 演示空间: https://huggingface.co/spaces/akira108/deer-flow
