# security-audit-skill

## 1. 项目定位

`security-audit-skill` 是 Cloudflare 开源的 coding-agent 安全审计 skill，用于把支持工具调用和并行子代理的 coding agent 组织成多阶段漏洞审计流程。它强调可利用漏洞、对抗性验证、结构化输出和独立复核，而不是让模型一次性给出泛泛安全建议。

它适合需要用 Claude Code、Codex 等 agent 辅助做代码安全审计的工程团队，也适合作为 agent 安全工作流设计样本。

## 2. 基本用法

官方 README 推荐通过 Skills CLI 安装：

```bash
npx skills add https://github.com/cloudflare/security-audit-skill \
  --skill security-audit
```

安装后，在目标代码库中向 coding agent 提出安全审计请求，例如：

```text
security audit this codebase
find security vulnerabilities in ./src
do a security review, output to ~/audits/my-project
```

skill 会根据触发词启动审计流程，并默认把输出写到独立审计目录。

## 3. 核心原理

项目把安全审计拆成六个阶段：

- Recon：并行研究 agent 梳理架构、信任边界和输入面。
- Hunt：多个 agent 从注入、访问控制、业务逻辑、密码学、链式攻击等角度寻找漏洞。
- Validate：独立 agent 尝试推翻每个发现，降低误报。
- Report：输出人类可读报告和中高危发现的详细追踪。
- Structured output：生成符合 schema 的 `findings.json`，并用 Node.js 校验器检查。
- Independent verification：新的 agent 对结构化结论逐条复核源码依据。

这种设计把“发现”和“验证”拆开，避免同一个 agent 同时当攻击者和裁判。

## 4. 工程价值

`security-audit-skill` 的价值在于把 agent 安全审计从 prompt 模板推进到可执行流程。它要求每个漏洞有可利用场景、影响判断和事实依据，并把被否决的发现也结构化记录下来，这对减少 AI 安全报告中的泛化噪声很重要。

它和 `SkillSpector`、`strix`、`VulnClaw` 形成互补：`SkillSpector` 偏 skill 供应链审计，`strix` / `VulnClaw` 偏授权攻击验证，而 Cloudflare 这个项目偏单仓库代码审计流程。

## 5. 风险边界

- 它不能替代专业安全团队，尤其不能替代威胁建模、动态测试和生产环境权限审计。
- 多 agent 并行会消耗较多 token 和时间，且结果质量依赖模型能力。
- agent 可能读取敏感代码、配置和测试数据，输出目录也可能包含内部漏洞细节。
- “只报告可利用漏洞”的原则能减少噪声，但也可能漏掉架构级硬化建议。

## 6. 补充建议

- 在隔离环境中运行，输出目录不要自动同步到公开仓库。
- 把 `findings.json` 纳入安全团队的复核流程，而不是直接转成 issue。
- 对高危结论要求人工复现或至少用独立工具交叉验证。
- 后续重点观察 Cloudflare 的 vulnerability harness 经验是否会继续回流到这个公开 skill。

## 7. 参考资料

- GitHub 仓库：https://github.com/cloudflare/security-audit-skill
- Cloudflare 博客：https://blog.cloudflare.com/build-your-own-vulnerability-harness
- Skills CLI：https://skills.sh
- GitHub API 元数据：仓库创建于 `2026-06-18`，抓取时约 `2.1k stars / 151 forks`
