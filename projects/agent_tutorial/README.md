<!-- markdownlint-disable MD013 -->

# agent_tutorial

> 上游仓库：[gitzyong812/agent_tutorial](https://github.com/gitzyong812/agent_tutorial) · 归类：AI 学习与教育资源 · 本页基于 2026-08-24 的上游 README、仓库目录与 GitHub API 快照整理。

## 定位

`agent_tutorial` 是一套中文开源智能体教程，以“AI 数字员工到一人公司”为叙事线，按模型调用、ChatBot、RAG、工具与记忆、harness、多智能体、应用和进阶八章组织文字与配套代码。它定位为学习资料与练习起点，而不是生产级 agent 平台或商业方案保证。

API 快照：3 stars、0 forks、0 个开放 issue；创建于 2026-08-23；Apache-2.0。该数字只是很早期的公开关注信号，并不代表课程质量、代码安全、教学有效性或 GitHub Trending 排名。

## 用法

建议顺序阅读每章正文与该章 `code/README.md`，只在本地 `.env` 或系统环境变量配置模型服务，不提交密钥、数据库或运行日志。上游给出的典型启动形式是：

```sh
git clone https://github.com/gitzyong812/agent_tutorial.git
cd agent_tutorial/chapterN_xxx/code
cp .env.example .env
python -m pip install -r requirements.txt
python -m uvicorn app.main:app --reload
```

第 1 章是脚本型练习，后续章节的依赖、服务端口与数据要求并不完全相同；应以对应章节的说明为准，并从不含真实业务数据的最小样例开始。

## 原理

- 课程按“模型调用 → 多轮上下文 → 外部知识 → 工具行动 → 可控可靠的 harness → 多角色协作 → 应用”的依赖链递进，避免把 agent 理解为一次提示词调用。
- RAG 章节将外部资料接入回答；工具与记忆章节把 ReAct 循环、工具调用和状态保存放入同一个数字员工示例；harness 章节强调可控、可靠与可追踪的工程封装。
- 多智能体章节用角色分工与任务依赖拆解协作，但这种架构是教学模型，不自动解决任务分解、成本、冲突、权限或结果验收问题。

## 价值

- 中文材料把概念、实践步骤、图片和代码放在同一章节中，适合从单模型调用逐步建立 agent 系统的完整心智模型。
- 章节产物明确，便于教师或自学者为每一阶段补充单元测试、评测集和运行日志，而不是只展示最终 UI。
- Apache-2.0 使文字、原创图与配套代码在许可证范围内更便于复用；仓库同时提示第三方组件仍保留各自许可证。

## 风险边界

- 教程示例可能依赖外部模型服务、数据库或 Web 服务；费用、日志、网络出口、提示词与上传资料的数据流必须单独确认。
- RAG、工具调用和记忆会放大错误检索、幻觉、提示注入和越权影响；演示成功不等于具备生产安全、评测或合规能力。
- `uvicorn --reload` 仅适合本地开发，不能直接作为公网部署方式；认证、密钥轮换、限流、审计、隔离与备份需要自行补齐。
- 课程目录的 README 对不同章节的实际依赖和测试覆盖并无统一保证，使用前应逐章锁定版本并运行测试或最小回归。

## 补充建议

1. 每章建立自己的 lockfile、`.env.example` 与可删除的测试数据，记录模型、温度、检索语料和工具版本，避免课堂结果不可复现。
2. 在进入工具调用与多 agent 前，先为“允许的动作、最大成本、超时、失败回退和人工确认”写出可执行策略与测试。
3. 用带正确答案和对抗输入的固定小评测集验证 RAG 引用、工具参数与记忆污染；不要只以演示对话判断效果。
4. 将一人公司案例视为产品原型练习，对支付、个人信息、外发营销与自动执行保持人工审批和法律/平台规则审查。

## 参考资料

- [上游 README / 课程目录与启动说明](https://github.com/gitzyong812/agent_tutorial)
- [GitHub API 元数据](https://api.github.com/repos/gitzyong812/agent_tutorial)
- [上游许可证](https://github.com/gitzyong812/agent_tutorial/blob/main/LICENSE)
- [FastAPI 文档](https://fastapi.tiangolo.com/)
- [Uvicorn 文档](https://www.uvicorn.org/)
