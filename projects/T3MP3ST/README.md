# T3MP3ST

## 1. 定位

`T3MP3ST` 是一个面向授权安全测试的多代理红队平台，目标是把
Claude Code、Codex、Hermes 或本地模型接入 recon、exploit、报告生成等
安全测试链路。它的核心卖点不是“又一个漏洞扫描器”，而是把现有 coding
agent 作为推理中枢，再在外侧补上工具、范围控制、benchmark 和 War Room
界面。

仓库在 2026-07-02 创建后迅速获得高星标，README 明确标注 AGPL-3.0、
`npm run verify-claims` 可复算声明，以及“authorized use only”。这类项目
适合放在 AI 安全 agent 与 agent harness 交叉位置观察。

## 2. 基本用法

项目当前主入口是 Node/TypeScript 工作流：

```bash
npm install
npm run server
```

启动后可打开本地 War Room，并在设置中连接本机已有的 agent 或配置
OpenRouter、Anthropic、OpenAI、xAI、Ollama、LM Studio、vLLM 等后端。README
也提供本地模型路径，用 `TEMPEST_LOCAL_BASE_URL` 和 `TEMPEST_LOCAL_MODEL`
把工具链接到 OpenAI-compatible server。

另一个关键命令是：

```bash
npm run verify-claims
```

它用于复算 README 中的 benchmark 声明，是判断该仓库是否认真处理安全项目
可信度的一个重要入口。

## 3. 核心原理

T3MP3ST 把任务拆成安全测试 kill chain：目标范围、侦察、利用、结果复核和
报告。仓库强调 recon engine、Arsenal、MCP server、HTTP API、scope
containment 和 coordinated-disclosure pipeline 等模块，并把部分能力标成
stable、experimental 或 roadmap。

它的技术路线可以理解为三层：

- agent 层：复用用户已经登录或部署的 coding agent / LLM。
- 工具层：把 nmap、DNS、HTTP fingerprint、PoC 验证、MCP 工具等纳入统一
  arsenal。
- 证据层：通过 benchmark JSON、`verify-claims` 和状态表区分可复算结果、
  实验能力和路线图。

## 4. 工程价值

对安全团队来说，它代表了“agentic security harness”的新形态：安全能力不
只靠单次 LLM 分析，而是把工具调用、范围约束、复算 benchmark 和人类审批
组合成可审计流程。

对普通工程团队来说，更值得借鉴的是它的状态披露方式。README 对已验证能力、
实验模块和路线图区分得较清楚，这比只宣传“AI 黑客 agent”更有工程参考价值。

## 5. 风险边界

这是高风险安全工具，必须只用于自己拥有或明确授权的目标。即便 README 已经
写明授权使用边界，使用者仍需自行保证测试范围、日志留存、披露流程和法律合规。

另外，仓库声称的 benchmark 需要持续复核。安全评测容易受到样本泄漏、prompt
设置、工具环境和目标范围影响，不能把单仓库结果直接等同于真实生产渗透能力。

## 6. 补充建议

- 优先从本地靶场、CTF 或自有应用开始，不要直接接入公网真实目标。
- 每次任务前固定 scope，保留命令日志和 agent 输出，避免无法复盘。
- 关注 `verify-claims` 是否持续通过，以及 benchmark 数据是否有第三方复测。
- 与 `strix`、`VulnClaw`、`SkillSpector` 做横向比较：T3MP3ST 更偏 offensive
  meta-harness，SkillSpector 更偏 skill 供应链审计。

## 7. 参考资料

- GitHub 仓库：<https://github.com/elder-plinius/T3MP3ST>
- GitHub Topics：`agents`、`ai`、`multi-agent`、`offensive-security`、`redteam`
- 许可证：AGPL-3.0
