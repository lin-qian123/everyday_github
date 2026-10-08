<!-- markdownlint-disable MD013 -->

# Codex Security（openai/codex-security）

> 上游仓库：<https://github.com/openai/codex-security> · 归类：Coding Agents 与终端助手 · 本页基于 2026-10-09 的 GitHub API、README、CLI / SDK、GitHub Action、findings service 与安全文档静态整理，未向真实仓库发起扫描、提交修复或上传 finding。

- 抓取快照：11,034 stars、856 forks、250 open issues。
- 热度信号：GitHub TypeScript Trending 抓取时约 +25 当日 stars；最后 push 为 2026-10-08。
- 版本与许可：最新 Release / tag `npm-v0.2.0`，Apache-2.0；本页固定审计 commit `e4f2f3daf644`。

## 定位

Codex Security 是 OpenAI 的代码安全 CLI 与 TypeScript SDK，用 Agent 执行漏洞发现、候选验证、补丁生成、修复核验、威胁模型和 `SECURITY.md` 草案，并可导入 GitHub code-scanning alert、导出 SARIF / JSON / CSV。它是分析与审阅工具，不是对仓库安全性的认证。

## 用法

Node.js 22.13+ / 24 / 26 与 Python 3.10+ 环境可用 `npx @openai/codex-security scan ...` 扫描目录、指定路径或 Git diff；先以小型测试仓库、标准 access program、只读凭据和明确 cost limit 运行。CI 应固定 Action 完整 commit，`persist-credentials: false`，报告先作为 artifact 审阅；启用 patch、Linear 发布或自定义 findings service 前另设人工批准。

## 原理

CLI 把扫描拆成 discovery、validation、severity、patch 与 verification 等阶段；deep 模式可并行 worker / subagent，并把 recipe、manifest、finding 与 threat model 持久化。findings service 以 SQLite 和 embeddings 存储完整 finding、候选重复项与人工确认分组；GitHub Action 和容器封装同一核心流程，多 provider 支持会改变模型、凭据和数据边界。

## 价值

它把“找到可疑点—验证—给出修复—复查”从单轮提示提升为有 artifact、scope、成本限制和导出格式的工作流。对已有 AppSec 团队，SARIF、历史 scan、owner suggestion 与 diff scope 可降低分诊和回归成本，也更容易把模型意见与人工处置分开。

## 风险边界

- finding、patch 与 severity 仍是模型驱动结果，可能漏报、误报、错误利用路径或破坏业务语义；必须由代码所有者和安全人员复核。
- deep scan 会读取更多源码并产生模型 / provider 费用；OpenAI、Bedrock、OpenRouter、Fireworks 等 provider 的数据位置、保留与凭据边界不同。
- preview findings service 的 API 没有内建认证；只能绑定 loopback 或置于认证 TLS proxy 后，否则完整 finding JSON 可被读写。
- 导入 finding 会把完整 JSON 发给配置的 embeddings endpoint；其中可能包含代码片段、路径、secret 线索和未披露漏洞。
- patch / policy 草案、Linear 发布和 GitHub Action 均可能产生外部副作用；“验证通过”只覆盖工具执行的检查，不等于完整业务回归。
- Daybreak / Trusted Access 控制的是能力访问，不构成对具体目标的授权；扫描第三方代码仍需所有权、合同与披露流程。

## 补充建议

先用含已知漏洞和无漏洞对照的 fixture 记录 precision、recall、重复 finding、成本与耗时；真实仓库从 `--diff`、只读 CI 和短期 key 开始。完整 scan artifact 设为敏感数据，findings service 不出 loopback，补丁必须经原测试、静态分析、人工 review 与部署回滚演练后再合并。

## 参考资料

- [GitHub 仓库](https://github.com/openai/codex-security)
- [GitHub REST API](https://api.github.com/repos/openai/codex-security)
- [README](https://github.com/openai/codex-security/blob/main/README.md)
- [项目配置](https://github.com/openai/codex-security/blob/main/docs/project-configuration.md)
- [Findings service](https://github.com/openai/codex-security/blob/main/sdk/typescript/docs/findings-service.md)
- [GitHub Action](https://github.com/openai/codex-security/blob/main/github-action/README.md)
- [安全策略](https://github.com/openai/codex-security/blob/main/SECURITY.md)
- [npm-v0.2.0 Release](https://github.com/openai/codex-security/releases/tag/npm-v0.2.0)
