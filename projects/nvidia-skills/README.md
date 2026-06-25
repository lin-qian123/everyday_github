# nvidia-skills（NVIDIA/skills）

- GitHub: https://github.com/NVIDIA/skills
- 文档: https://docs.nvidia.com/skills
- 记录日期: 2026-06-25 (Asia/Shanghai)

## 定位

`NVIDIA/skills` 是 NVIDIA 官方维护的 agent skill 目录仓库，面向 CUDA-X、AI Blueprints 和相关平台工具，为 AI agent 提供经过 NVIDIA 验证的技能包入口。它的关键意义不在“技能数量”，而在“厂商正式把技能目录当作能力治理接口”。

## 用法

### 1) 通过 `skills` CLI 安装

官方 README 给出的默认方式是：

```bash
npx skills add nvidia/skills
```

### 2) 指定单个 skill 安装

如果已经知道 skill 名称，可以直接跳过交互：

```bash
npx skills add nvidia/skills --skill cuopt-numerical-optimization-api-python --yes
```

### 3) 指定目标 agent

README 明确给出了对 Claude Code、Codex、Cursor、Kiro 等目标 agent 的安装方式：

```bash
npx skills add nvidia/skills --skill cuopt-numerical-optimization-api-python --agent codex
```

## 原理

1. 该仓库本身更像 catalog，而不是所有 skill 的唯一开发仓库；README 明确写到技能维护在各自产品仓库，再通过自动同步流水线镜像到这里。
2. 它遵循 agent skills 规范和 `skills` CLI 安装路径，因此能被已有的 skills 分发生态直接消费。
3. “NVIDIA-verified” 的标签说明它要解决的不只是安装问题，还包括来源可信度与能力治理问题。

## 价值

- 对使用 NVIDIA 软硬件栈的团队来说，它降低了让 agent 正确使用 CUDA-X、蓝图和平台工具的门槛。
- 它把技能仓库从“社区经验包”推进到“厂商认证目录”，对企业采用会更有说服力。
- 这类仓库也在给整个 agent 生态示范一种模式：厂商可以把最佳实践和接入规范沉淀成可安装能力，而不是只给 PDF 文档。

## 风险边界

- 它明显偏向 NVIDIA 生态，对多厂商混合环境来说并不天然中立。
- 技能“已验证”不代表在你的权限模型、驱动版本或部署环境里一定能直接工作，仍需做本地验证。
- 当技能目录来自多个上游产品仓库时，版本同步、弃用策略和兼容说明会变得重要。

## 补充建议

1. 把它优先当成“NVIDIA 栈最佳实践入口”，而不是通用 agent 技能市场。
2. 试用时先选一个边界清晰的技能，例如某个 Python API 或优化器，而不是一次装很多技能。
3. 如果团队已经用 `vercel-labs/skills` 或自建技能仓库，重点关注它在来源可信度、文档质量和厂商背书上的差异。

## 参考资料

- https://github.com/NVIDIA/skills
- https://docs.nvidia.com/skills
- https://developer.nvidia.com/blog/nvidia-verified-agent-skills-provide-capability-governance-for-ai-agents/
- https://github.com/trending/python
