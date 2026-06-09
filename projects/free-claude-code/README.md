# Free Claude Code（Alishahryar1/free-claude-code）

- GitHub: https://github.com/Alishahryar1/free-claude-code
- 记录日期: 2026-04-29 (Asia/Shanghai)

## 这是什么

`free-claude-code` 是一个 Anthropic Messages API 兼容代理层，让 Claude Code 客户端可以路由到多个后端（NVIDIA NIM、OpenRouter、DeepSeek、LM Studio、llama.cpp、Ollama）。核心价值是“保留 Claude Code 使用体验 + 切换底层模型与成本结构”。

## 热度信号

1. GitHub 仓库约 `17.3k stars`（2026-04-29 抓取）。
2. GitTrend（2026-04-25 数据）显示其为当日高增项目之一。

## 怎么用（最短路径）

```bash
# 1) 准备 Python 与 uv
# 2) 启动代理服务
uv run uvicorn server:app --host 0.0.0.0 --port 8082
```

最小配置思路：
1. 复制 `.env.example` 为 `.env`。
2. 选择一个 provider 并填入 key。
3. 设置 `ANTHROPIC_AUTH_TOKEN` 作为本地代理鉴权。
4. 让 Claude Code 指向该代理地址。

## 核心原理

1. 协议兼容：对外保持 Anthropic 接口语义，降低客户端改造成本。
2. 路由分发：按模型名/策略把请求转发到不同推理后端。
3. 中间层增强：在代理层处理流式输出、工具调用、失败回退与日志。

## 适用场景

1. 需要在本地模型与云模型间灵活切换的开发者。
2. 希望控制 token 成本和延迟的团队。
3. 想统一多供应商模型接入的实验环境。

## 价值与风险

价值：
- 降低单一模型/单一供应商锁定。
- 让成本、隐私、性能之间更易做权衡。

风险：
- 代理层本身是新的可用性与安全边界。
- 多后端行为不一致会引入调试复杂度。

## 我认为有价值的补充材料

1. 给每个 provider 维护独立基准任务（代码生成、修复、长上下文）。
2. 代理层默认开启请求审计与敏感字段脱敏。
3. 为“高风险命令”增加人工确认闸门。

## 参考来源

- https://github.com/Alishahryar1/free-claude-code
- https://gittrend.io/
