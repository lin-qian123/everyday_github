<!-- markdownlint-disable MD013 -->

# open-kritt

## 定位

`open-kritt` 是 Kritt-ai 开源的 agentic security scanner，用多个 AI agents 编排代码漏洞发现、验证和 PoC 构建。它面向授权安全研究和 bug bounty 场景，和 `strix`、`VulnClaw`、`SkillSpector` 同属 AI 安全工具链热点。

## 今日信号

- GitHub：<https://github.com/Kritt-ai/open-kritt>
- 官网：<https://kritt.ai/>
- 创建时间：2026-07-20。
- 抓取时约 36 stars、11 forks。
- 语言 / 许可证：JavaScript，AGPL-3.0。
- Topics：`agent`、`ai`、`bug-bounty`、`security-research`。

## 用法

项目通过 Docker Compose 启动本地 stack，仓库内 CLI `./kritt setup` 负责配置模型访问和运行环境，`./kritt start` 后打开本地 Web UI。它支持用户自带 Codex 登录或连接 OpenAI、Anthropic、OpenRouter 等模型入口，也可选配 GitHub token 扫描私有仓库。

## 原理

open-kritt 将安全扫描拆成 workflow steps 和 tool-enabled agents。agents 在 disposable job containers 内运行，拥有目标仓库的可写副本、网络和编译/测试工具，围绕真实漏洞查找、验证和 PoC 生成协作。项目同时提供 threat model 文档，强调容器运行边界。

## 价值

- 把 AI 安全从“静态提示生成报告”推进到可运行工具链、验证步骤和 PoC 证据。
- 对授权 bug bounty、内部安全审计和 CI 安全门禁都有参考价值。
- AGPL 开源使团队可以审查 workflow 和威胁模型，而不是依赖黑盒 SaaS。

## 风险边界

- Tool-enabled agents 在容器内可联网、可安装工具、可执行代码，README 明确建议使用专用 Docker host 或 VM。
- 默认本地端口绑定到 `127.0.0.1`，但后端不包含应用认证，不应暴露到不可信网络。
- 漏洞发现工具具备双重用途，只适合授权范围内使用；自动化 PoC 也可能触发目标系统副作用。

## 补充建议

- 后续跟踪其 threat model、workflow 可配置性、误报率和真实 bug bounty 复现证据。
- 可与 `strix` 做横向比较：二者都关注漏洞验证，但 open-kritt 更强调开源本地 stack 和研究者 workflow。
- 团队试用前应先用 deliberately vulnerable repo 或内部靶场验证隔离与日志。

## 参考资料

- GitHub 仓库：<https://github.com/Kritt-ai/open-kritt>
- 官网：<https://kritt.ai/>
- README：<https://github.com/Kritt-ai/open-kritt#readme>
- Threat model：<https://github.com/Kritt-ai/open-kritt/blob/main/docs/threat-model.md>
