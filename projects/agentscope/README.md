<!-- markdownlint-disable MD013 -->

# agentscope

## 定位

AgentScope 是阿里通义实验室团队维护的 Python Agent 框架。2.0 把 ReAct、模型、工具、权限、上下文、事件和 workspace 等构件组合成 SDK，并提供应用服务、Web UI、team、RAG 与调度入口。本文记录 Python 仓库，与已有 [AgentScope Java](../agentscope-java/README.md) 分开。

- 上游：[agentscope-ai/agentscope](https://github.com/agentscope-ai/agentscope)，仓库 ID `742244656`；旧 owner `modelscope` 也参与本地去重。
- 2026-11-22（Asia/Shanghai）07 时段：官方 Python daily **+64**；API stars / forks / open issues（含 PR）为 **36,438 / 3,899 / 843**。[API](https://api.github.com/repos/agentscope-ai/agentscope)
- 最新核到非预发行版 [v2.0.12](https://github.com/agentscope-ai/agentscope/releases/tag/v2.0.12)，UTC 2026-11-16；本页主干快照固定 `ba9e9d04eb3788b3dc8d8148d27c0948a3b7f43e`。当前 `latest` 权限文档重定向到 `2.0.13dev`，不能当作稳定版已实现的逐项保证。
- 分类：`Agent 框架与技能生态`。本轮仅资料与少量源码核读，未安装、授权、连接模型 / MCP / 数据库或启动服务。

## 用法

要求 Python 3.11+。在独立环境中可先选择已发布版本，以下未执行：

```bash
python -m pip install 'agentscope==2.0.12'
python -m pip show agentscope
```

随后按对应版本构造 `Agent(name, system_prompt, model, toolkit=...)` 并用 `launch_console(agent)` 接入终端。固定主干 README 示例使用 `DashScopeChatModel`、从 `DASHSCOPE_API_KEY` 读取凭据，并主动注册 Bash / 读写工具；这会调用模型服务并允许工具访问，不能当作无副作用示例。初试可先不注册文件和 shell 工具，再逐项加入。[固定快速开始](https://github.com/agentscope-ai/agentscope/blob/ba9e9d04eb3788b3dc8d8148d27c0948a3b7f43e/README.md)、[Agent 构造入口](https://github.com/agentscope-ai/agentscope/blob/ba9e9d04eb3788b3dc8d8148d27c0948a3b7f43e/src/agentscope/agent/_agent.py)

服务与 Web UI 是另一层部署：README 分别从 `examples/agent_service` 运行后端、从 `examples/web_ui` 安装前端依赖并启动。正式使用应先读版本对应的服务配置、存储和认证，再决定接入 channel、调度或共享资源。按需安装 extras；`[full]` 会加入模型、sandbox、存储、RAG 等多类依赖，不是最小安装。[包元数据与 extras](https://github.com/agentscope-ai/agentscope/blob/ba9e9d04eb3788b3dc8d8148d27c0948a3b7f43e/pyproject.toml)

## 原理

Agent 在推理与工具调用循环中，通过事件输出 reasoning、工具和多模态内容；Toolkit 注册 Python 工具、MCP 和 skills，middleware 插入模型调用、权限、上下文压缩等阶段。模型、工具与 workspace 分层，使同一应用可替换 provider 和执行后端；接口统一不表示后端行为相同。

权限引擎对每次调用返回 ALLOW / DENY / ASK。固定 `PermissionContext` 默认 DEFAULT；该模式先处理 deny / ask，再判断该次调用是否只读和工具自身检查，最后按 allow 或 ASK 决定，不能概括成“每次都询问”。BYPASS 则放宽若干检查与回退，仍保留显式规则等约束，不能把它理解为安全的无人值守默认。[默认 context](https://github.com/agentscope-ai/agentscope/blob/ba9e9d04eb3788b3dc8d8148d27c0948a3b7f43e/src/agentscope/permission/_context.py)、[权限实现](https://github.com/agentscope-ai/agentscope/blob/ba9e9d04eb3788b3dc8d8148d27c0948a3b7f43e/src/agentscope/permission/_engine.py)

## 价值

- 对需要追踪工具调用、中断与状态的应用，提供比一段裸模型循环更明确的构件和扩展点。
- SDK 和应用服务分层，适合先验证单 Agent，再引入 team、RAG 和多会话功能。
- 权限、执行位置和模型路由可以分别实验；上游的 production-ready 描述属于项目定位，本轮没有生产可用性、租户隔离或成功率验收。

## 风险边界

- **本地目录不是 sandbox。** `LocalWorkspace` 构造本机 `LocalBackend`，把 Bash / PowerShell 的 cwd 设到 workdir，并组织 skills / MCP / 会话文件。目录布局本身不限制宿主权限；Docker、Bubblewrap、Apple Container 或云后端还要各自核挂载、环境、网络和凭据。[本机 workspace 实现](https://github.com/agentscope-ai/agentscope/blob/ba9e9d04eb3788b3dc8d8148d27c0948a3b7f43e/src/agentscope/workspace/_local_workspace.py)
- **权限模式有不同语义。** DEFAULT 会自动放行被判定只读的调用；BYPASS 跳过部分 safety ASK。自定义工具的检查质量、shell 解析和规则范围需要真实拒绝测试。不能只从模式名称推断全局只读或系统隔离。
- **预算是每次 reply 的 token 控制。** 抽读 `ReplyBudgetControlMiddleware`：累计加权 usage 到阈值后，在下一次推理前加入收尾提示，并禁用普通工具或只保留结构化输出工具；仍会走模型调用。据此不能认定它提供服务商费用硬上限、单次调用不会超额或团队总预算硬限制。[预算实现](https://github.com/agentscope-ai/agentscope/blob/ba9e9d04eb3788b3dc8d8148d27c0948a3b7f43e/src/agentscope/middleware/_budget.py)
- **发行版仍有边界修复。** v2.0.12 包含移除 server-path skill 导入端点、复合 Bash 子命令权限处理、Bubblewrap probe、调度与 RAG 删除失败处理等变更。这是上游修复记录，不证明所有路径已经安全，也不应直接套用开发版文档。[发行说明](https://github.com/agentscope-ai/agentscope/releases/tag/v2.0.12)
- **数据与外部动作。** 模型、embedding、语音、长期记忆和 channel 各有数据出口；skills / MCP 与调度可带来真实执行。服务多租户、知识库 scope、持久化、备份恢复和删除行为要另做测试，不能从 SDK 示例推出。
- **许可与版本。** 根代码 Apache-2.0，模型服务、记忆后端和第三方 skills 分别适用其条款。固定主干、稳定 release 与在线 latest 文档应分别记录。[LICENSE](https://github.com/agentscope-ai/agentscope/blob/ba9e9d04eb3788b3dc8d8148d27c0948a3b7f43e/LICENSE)

## 补充建议

先用脱敏输入验证无外部工具的单 Agent，再增加一项可判定输出的只读工具。测试拒绝写入、复合 shell 命令、模型失败、预算越限和中断接续，保存事件与费用；需要执行代码时再选择并验收执行后端。多会话服务应额外测试跨用户访问与删除失败恢复。本轮未运行这些实验。

## 参考资料

- [固定 README](https://github.com/agentscope-ai/agentscope/blob/ba9e9d04eb3788b3dc8d8148d27c0948a3b7f43e/README.md)、[包元数据](https://github.com/agentscope-ai/agentscope/blob/ba9e9d04eb3788b3dc8d8148d27c0948a3b7f43e/pyproject.toml)、[Agent 入口](https://github.com/agentscope-ai/agentscope/blob/ba9e9d04eb3788b3dc8d8148d27c0948a3b7f43e/src/agentscope/agent/_agent.py)。
- [权限引擎](https://github.com/agentscope-ai/agentscope/blob/ba9e9d04eb3788b3dc8d8148d27c0948a3b7f43e/src/agentscope/permission/_engine.py)、[LocalWorkspace](https://github.com/agentscope-ai/agentscope/blob/ba9e9d04eb3788b3dc8d8148d27c0948a3b7f43e/src/agentscope/workspace/_local_workspace.py)、[reply 预算](https://github.com/agentscope-ai/agentscope/blob/ba9e9d04eb3788b3dc8d8148d27c0948a3b7f43e/src/agentscope/middleware/_budget.py)、[v2.0.12](https://github.com/agentscope-ai/agentscope/releases/tag/v2.0.12)。
- [在线权限文档](https://docs.agentscope.io/latest/en/building-blocks/permission-system/overview)：本轮转 `2.0.13dev`，仅作文档导航和版本漂移证据。README 所链论文未阅读全文，不用历史论文替代当前实现验证。
