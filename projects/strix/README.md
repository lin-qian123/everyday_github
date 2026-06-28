# strix（usestrix/strix）

- GitHub: https://github.com/usestrix/strix
- 记录日期: 2026-06-29 (Asia/Shanghai)

## 定位

`strix` 是一个面向应用安全测试的开源 AI hacker agent 项目。它试图把侦察、动态运行、漏洞验证、PoC 生成与 CI/CD 阻断串成自动化流程，让安全测试从“静态规则扫描”推进到“agent 模拟攻击者验证漏洞”。

## 热度信号

1. GitHub API 在 2026-06-29 抓取时显示约 `26,681 stars`、`2,983 forks`。
2. GitHub Python 日榜在 2026-06-29 抓取时出现该项目。
3. 官方 README 明确写到它是 `Open-source AI hackers to find and fix your app’s vulnerabilities`，并强调可与 GitHub Actions / CI/CD 集成。

## 用法

### 1) 安装或进入托管入口

官方 README 同时提供文档站点、Web 应用和 PyPI 包入口：

```bash
pip install strix-agent
```

实际接入前应先阅读官方文档，确认目标应用、运行权限、网络访问范围和测试授权边界。

### 2) 用于开发流程

典型使用方式不是替代传统 SAST，而是在 PR、预发布环境或授权测试环境中，让 agent 动态运行目标、尝试复现漏洞，并输出可验证证据。

### 3) 接入 CI/CD

README 重点宣传了 GitHub Actions / CI/CD 场景：在 pull request 阶段自动扫描并阻止明显不安全的代码进入主干。

## 原理

1. 它把安全测试拆成多 agent 协作：侦察、攻击面枚举、payload 尝试、漏洞确认和修复建议。
2. 它强调动态验证与 PoC，而不是只返回“疑似风险”。
3. 从趋势上看，它代表的是“agent 进入安全验证链路”，与 `SkillSpector` 的 agent skill 供应链安全形成互补：一个看应用漏洞，一个看 agent 生态自身风险。

## 价值

- 对开发团队，价值在于把安全反馈提前到 PR 和 CI，而不是等上线后再做集中渗透测试。
- 对安全团队，agent 可以承担一部分重复侦察和初步验证工作，把人工精力留给复杂漏洞链分析。
- 对 AI 工具生态，这是“coding agent 写代码”之后的自然延伸：同一条流水线还需要“security agent 验证代码”。

## 风险边界

- 只能在授权目标和可控环境中运行，不能把它当成无边界扫描器使用。
- 动态攻击测试可能触发限流、脏数据、告警或服务不稳定，需要先准备测试环境。
- AI 生成的漏洞报告可能存在误报、遗漏和夸大影响，需要安全人员复核。

## 补充建议

1. 先在内部演示应用或 staging 环境中验证输出质量，再接入真实生产流程。
2. 与传统 SAST、依赖漏洞扫描、secret scanning 并行使用，不要只依赖 agent。
3. 若引入 CI 阻断，建议先用非阻断模式积累误报样本，再逐步提升门禁强度。

## 参考资料

- https://github.com/usestrix/strix
- https://docs.strix.ai
- https://github.com/trending/python
