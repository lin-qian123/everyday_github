<!-- markdownlint-disable MD013 -->

# Reversa（sandeco/reversa）中文解读

> 上游仓库：<https://github.com/sandeco/reversa> · 归类：Coding Agents 与终端助手 · 本页基于 2026-10-15 的 README、配置文档、Agent skills、论文入口、manifest、tag、许可证与 GitHub REST API 静态整理；未把私有遗留代码交给模型、执行 autonomous / forward 流程或验证生成规格的行为等价性。

## 定位

Reversa 是面向遗留系统的“反向规格工程”框架：它把 Scout、Archaeologist、Detective、Architect、Writer、Reviewer 等 Agent 组织成流水线，从现有源码提取业务规则、模块契约、架构与技术债，再生成可被 Coding Agent 继续消费的可追溯规格。它不是传统反编译器，而是安装到项目中的 skills / orchestrator 集合。

## 用法

在已提交、可恢复的仓库副本中运行 `npx reversa install`，选择宿主和 Agent；安装器会创建 `.agents/skills/`、宿主入口文件、`.reversa/` 状态和默认 `_reversa_sdd/` 输出目录。首次建议只跑受监督的 `/reversa` Discovery，并在每个 `CONTINUAR` 门前人工核对；`reversa-autonomous`、`reversa-forward` 与迁移 / coding 路径应留到规格质量和写入边界验证后。

## 原理

- Discovery 依次做表面侦察、模块挖掘、隐含规则解释、规格生成与复核，进度写入 `.reversa/state.json`。
- 生成结果保留源码定位、模块关系、ADR / ERD / C4 等结构，使后续需求和代码变更能回溯到遗留实现。
- 安装器用 SHA-256 manifest 管理自身写入；团队配置与个人 `config.user.toml` 分离。
- forward / migrate / debugger 等后续 Agent 读取已提取规格，形成 requirements、roadmap、actions、实现与同步记录。

## 价值

- 把“读懂老系统”拆成角色、检查点和持久产物，比一次性让模型概括整个仓库更容易审阅和续跑。
- 将业务规则、架构、数据和界面证据分层，有利于在重构前暴露知识空洞与相互矛盾的实现。
- 规格作为中间层，可供不同宿主复用，而不是把理解绑定在一次对话里。

## 风险边界

- README 的“legacy 不可变”是工作流约束，不是 OS sandbox；上游也明确 autonomous Agent 可能犯错，而 forward coding 路径会按配置写项目代码并运行 build / test / install。
- 框架本身不收集 LLM key，不等于源码不外发：真正读取仓库的是当前 Claude / Codex / Cursor 等宿主，其 provider、MCP、日志和数据保留政策仍然生效。
- 生成规格可能把历史 bug、死代码和过期规则误当成契约；“可追溯”只证明来源位置，不证明业务意图或行为正确。
- GitHub 无正式 Release；API 返回的最新 tag 为 `v1.2.57`，而 `package.json` 已是 `1.3.4`，安装必须固定 npm / commit 并记录实际 payload。

## 补充建议

- 先在去密、只读副本跑 Scout + Writer 的最小路径，抽样把规格逐条回指源码、测试和真实业务负责人。
- 用 Git diff、文件系统监控和宿主 tool allowlist 验证宣称的写入目录；禁用 push、发布、删除和生产凭据。
- 把“已观察行为”“推断规则”“业务确认”“待验证”分栏，迁移前补 golden test 与真实数据回放，不以规格篇幅当覆盖率。

## 参考资料

- GitHub 仓库：<https://github.com/sandeco/reversa>
- GitHub REST API：<https://api.github.com/repos/sandeco/reversa>
- 使用与安全说明：<https://github.com/sandeco/reversa/blob/main/README.md>
- 配置文档：<https://github.com/sandeco/reversa/blob/main/docs/configuracao.md>
- npm manifest：<https://github.com/sandeco/reversa/blob/main/package.json>
- 上游论文入口：<https://arxiv.org/abs/2605.18684>
- LICENSE：<https://github.com/sandeco/reversa/blob/main/LICENSE>
