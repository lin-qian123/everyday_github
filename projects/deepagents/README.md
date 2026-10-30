<!-- markdownlint-disable MD013 -->

# deepagents

## 定位

Deep Agents 是 LangChain 的 Python Agent harness，把规划、文件工具、子任务、上下文压缩和技能装配在 LangGraph / LangChain 之上。适合需要多步骤执行、恢复和观测的开发者；它是可嵌入的库，终端产品 Deep Agents Code 和 JavaScript 实现各有独立入口。

2026-10-31 采样：Python daily +60 stars；API 累计 30,796 stars / 4,329 forks / 210 open issues（含 PR）。核读 main `287fab316960`；发行 API 首项 [langchain-quickjs==0.3.11](https://github.com/langchain-ai/deepagents/releases/tag/langchain-quickjs%3D%3D0.3.11)，2026-10-27 UTC。以下区分作者文档与有限源码核读，未做上游运行验收。

## 用法

固定 SDK 版本，在隔离的 Python 环境安装；主线 manifest 为 `0.7.32`，要求 Python `>=3.11,<4.0`。先配置支持 tool calling 的模型与对应 provider 依赖，再以 `create_deep_agent(model=...)` 创建代理；模型凭证、账单和网络出口由实际 provider 决定。

```bash
uv add deepagents==0.7.32
```

先测试只读工具，再按需增加文件写入、shell、MCP、跨会话 store 与 checkpointer；高影响工具显式配置 `interrupt_on`，恢复调用使用相应线程标识。本轮未安装 SDK 或调用模型。

## 原理

`create_deep_agent` 装配文件系统、子代理、skills、memory、上下文管理等 middleware。源码在未指定 backend 时使用 `StateBackend()`，文件属于代理状态；落盘、长期 store、sandbox 是独立配置，不由“有文件工具”自动获得。LangGraph 的 checkpoint 为恢复提供基础，但外部 API 动作仍需幂等设计。

## 价值

提供可替换的长任务基础层，减少自行拼接上下文裁剪、委派和文件工具的工作。适合在固定任务集上比较不同模型、后端与恢复策略；README 的 production-ready 是作者定位，本轮没有生产可用性验收。

## 风险边界

- MIT；模型、MCP、远程执行与可选观测服务分别核条款和数据出口。
- `FilesystemBackend` 的虚拟路径约束不提供进程隔离；`LocalShellBackend` 明示在宿主执行，shell 可访问文件工具虚拟根之外的路径。不要把 `root_dir` 当成 OS sandbox。
- SDK 默认 backend 与终端产品的默认权限不是同一配置；人工中断需要调用端持久化并实现审批 / 恢复交互。
- 子代理上下文分离不等于用户、文件和凭证隔离；工具允许什么，代理就可能做什么。
- 发行 API 首项是 `langchain-quickjs==0.3.11` 组件，不是 SDK `0.7.32` 的统一发行。固定 commit、安装包和后端后再比较。

## 补充建议

用十个有明确产物的任务检查恢复、拒绝工具、上下文压缩丢失、重复外部调用和跨线程污染。记录模型 / token / 耗时 / 重试次数及人工接管；先用状态后端或真实隔离环境，最后再评估宿主 shell。

## 参考资料

- [上游仓库](https://github.com/langchain-ai/deepagents)、[仓库 API](https://api.github.com/repos/langchain-ai/deepagents)。
- [README.md](https://github.com/langchain-ai/deepagents/blob/287fab3169602d326674a1c4892810efef183710/README.md)。
- [LICENSE](https://github.com/langchain-ai/deepagents/blob/287fab3169602d326674a1c4892810efef183710/LICENSE)。
- [libs/deepagents/pyproject.toml](https://github.com/langchain-ai/deepagents/blob/287fab3169602d326674a1c4892810efef183710/libs/deepagents/pyproject.toml)。
- [libs/deepagents/deepagents/graph.py](https://github.com/langchain-ai/deepagents/blob/287fab3169602d326674a1c4892810efef183710/libs/deepagents/deepagents/graph.py)。
- [libs/deepagents/deepagents/backends/filesystem.py](https://github.com/langchain-ai/deepagents/blob/287fab3169602d326674a1c4892810efef183710/libs/deepagents/deepagents/backends/filesystem.py)。
- [libs/deepagents/deepagents/backends/local_shell.py](https://github.com/langchain-ai/deepagents/blob/287fab3169602d326674a1c4892810efef183710/libs/deepagents/deepagents/backends/local_shell.py)。
