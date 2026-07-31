# architect-agent

## 定位

`architect-agent` 是 Commonwealth Bank of Australia 发布的研究型工作流：把 BPMN 流程图转换为可执行的 agent 工具、API 包装、CLI 与单元测试。仓库关联 ICML 2026 SCALE workshop 论文；截至 2026-08-01 的 GitHub API 快照，项目创建于 2026-07-31，约 5 stars、0 forks、MIT。

## 用法

使用 `uv sync` 安装依赖，配置 `OPENAI_API_KEY`、`AGENT_LLM` 与 `EVAL_LLM`；先在独立终端启动仓库的 mock API，再在 `architect_agent/` 运行 `uv run main.py -d <输出目录>`。生成后应先运行 `pytest test_tools.py`，再以受控样例启动生成的 CLI agent。

## 原理

工作流将 BPMN 中的确定性步骤映射为工具与接口契约，分阶段生成实现和测试，并配有 tool-use、单测与运行评测。论文比较的是特定 BPMN 转代码任务上的专用流程与通用 coding agent，不是对所有 agent 任务的普适排序。

## 价值

- 将业务流程、生成代码与测试产物放在同一可审阅链路中。
- 为“专用 agent 是否优于通用 agent”提供可复现的任务设定与评测入口。

## 风险边界

- 官方明确仅供研究、教育与社区用途，不应部署到安全或生产环境。
- 不要将不可信 BPMN、模型输出或生成工具直接接到有权限的内部 API。
- mock 服务默认监听 `0.0.0.0:8080`；本机开发也应限制网络暴露并使用非 root 账号。

## 补充建议

先选无敏感数据的确定性流程做 shadow run，检查状态分支、异常路径、幂等性和人工批准点。上线判断应另做威胁建模、权限最小化、端到端测试与独立评审。

## 参考资料

- GitHub：<https://github.com/Commonwealth-Bank-of-Australia/architect-agent>
- 论文：<https://arxiv.org/abs/2607.14456>
- GitHub API 快照：<https://api.github.com/repos/Commonwealth-Bank-of-Australia/architect-agent>
