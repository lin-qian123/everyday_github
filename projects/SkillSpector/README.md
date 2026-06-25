# SkillSpector（NVIDIA/SkillSpector）

- GitHub: https://github.com/NVIDIA/SkillSpector
- 记录日期: 2026-06-26 (Asia/Shanghai)

## 定位

`SkillSpector` 是一个面向 AI agent skills 的安全扫描器，重点不是做通用 SAST，而是专门检查 Claude Code、Codex CLI、Gemini CLI 等生态里技能包的恶意行为、危险模式和权限风险。

## 热度信号

1. GitHub API 在 2026-06-26 抓取时显示约 `10,667 stars`、`856 forks`，仓库在 `2026-06-25T00:23:50Z` 仍有推送。
2. GitHub Trending Python 日榜在 2026-06-26 抓取时显示其当日新增约 `410 stars today`。
3. 官方 README 直接写到 `26.1% of skills contain vulnerabilities`、`5.2% show likely malicious intent`，很明确地把 skill 安全当成独立问题域。

## 用法

### 1) 直接用 `uv` 安装

README 推荐的无克隆安装方式是：

```bash
uv tool install git+https://github.com/NVIDIA/skillspector.git
```

### 2) 扫描本地技能目录或单个文件

```bash
skillspector scan ./my-skill/
skillspector scan ./SKILL.md
```

### 3) 扫描远程仓库并输出结构化报告

```bash
skillspector scan https://github.com/user/my-skill
skillspector scan ./my-skill/ --format sarif --output report.sarif
```

如果只想跑静态分析，可以加 `--no-llm`。

## 原理

1. 它围绕 agent skill 这个特定对象做扫描，而不是只按普通代码文件处理。
2. 核心检测分成两层：快速静态分析，以及可选的 LLM 语义分析。
3. README 列出的风险面覆盖 prompt injection、数据外传、权限升级、memory poisoning、tool misuse、MCP least privilege、MCP tool poisoning 等多种 agent 特有问题。
4. 输出支持终端、JSON、Markdown、SARIF，说明它既能给人工审查，也能接进 CI / 安全平台。

## 价值

- 这是今天非常值得关注的信号：agent 生态已经开始从“装更多 skill”转向“先验证 skill 安不安全”。
- 相比一般安全工具，`SkillSpector` 更贴近当前真实风险，因为 skill、plugin、MCP server 天生就带着高权限与隐式信任。
- 如果厂商和社区后续都开始把 skill 审计前置，这类项目可能会成为 agent 供应链的基础设施层。

## 风险边界

- 扫描结果只能提高发现概率，不等于完全证明某个 skill 安全。
- README 自带的风险统计结论来自项目研究上下文，落地时仍应关注误报、漏报和规则漂移。
- 若团队把它接入 CI，还需要自己决定“多高风险分数才阻塞安装或合并”，工具不会自动替代安全治理。

## 补充建议

1. 先用 `--no-llm` 跑一遍基线扫描，再决定是否引入联网语义分析，避免把审计流程本身做得过重。
2. 若仓库里已经在用 `agents`、`nvidia-skills`、`agent-toolkit-for-aws` 这类插件 / skill 目录项目，可以把 `SkillSpector` 视为它们的配套治理层。
3. 更适合把它放在“安装前检查”和“定期重扫”两个环节，而不是只在出现事故后补救。

## 参考资料

- https://github.com/NVIDIA/SkillSpector
- https://github.com/trending/python
- https://osv.dev
