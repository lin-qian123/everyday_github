# VulnClaw（Unclecheng-li/VulnClaw）

> GitHub: https://github.com/Unclecheng-li/VulnClaw  
> PyPI: https://pypi.org/project/vulnclaw/  
> 定位：基于 LLM Agent、MCP 工具链和渗透测试 skill 的安全测试 CLI / Web UI。

## 项目定位

`VulnClaw` 是一个 AI 驱动的渗透测试 agent。它把自然语言输入、LLM tool calling、MCP 工具链、漏洞检测插件、渗透测试 skill 和报告生成串成一条工作流，目标是在已授权场景下自动完成信息收集、漏洞发现、漏洞利用验证和报告生成。

它的热点意义在于：agent 技术正在从“写代码/写文档”扩展到高风险的安全操作领域。这类项目能展示 agent + MCP + skills 的能力上限，也必须同时讨论授权、隔离和误用风险。

## 用法

官方 README 给出的安装方式包括 PyPI 和源码安装：

```bash
pip install vulnclaw
```

或：

```bash
git clone https://github.com/Unclecheng-li/VulnClaw.git
cd VulnClaw
pip install -e .
```

Docker / Web UI 模式可通过 `docker compose up --build` 启动，默认 Web UI 地址为：

```text
http://127.0.0.1:7788
```

使用前需要配置兼容 OpenAI 协议的模型 API key。项目 README 明确强调适用于已授权渗透测试、CTF、安全教学、红队演练等场景。

## 核心原理

- **目标驱动求解引擎**：不再只跑固定轮数，而是以目标达成、探索前沿耗尽或安全预算触顶作为终止条件。
- **黑板图状态空间搜索**：把渗透过程建模为 Fact（已确认事实）和 Intent（探索方向），减少重复请求与空转。
- **证据级反幻觉闸门**：结论必须能在真实工具输出中找到证据，降低 LLM 编造 flag 或漏洞结论的风险。
- **MCP 工具链**：通过 fetch、memory、chrome-devtools、burp 等 MCP 服务连接外部工具。
- **skill 与插件体系**：内置 Web、CTF、OSINT、安全知识等 skill，并把检测结果汇入报告链路。
- **多模型兼容**：支持 OpenAI 兼容协议以及多家中文模型服务商，便于在不同预算和能力下测试。

## 价值

`VulnClaw` 代表“agent 安全自动化”的一个方向：不是简单问模型“哪里有漏洞”，而是让模型在工具输出、状态图和证据约束下逐步探索。对安全团队和 agent 工程团队，它的观察价值包括：

- 高风险工具调用如何设计安全预算和终止条件；
- LLM 幻觉如何通过真实工具输出做硬约束；
- MCP 在浏览器、抓包、记忆和执行工具间如何串联；
- 安全报告能否从探索过程自然生成，而不是事后手写；
- agent skill 是否能把渗透测试经验变成可复用流程。

## 风险边界

- 只能用于合法授权目标、CTF 或教学环境；未授权扫描和利用存在明确法律与伦理风险。
- `python_execute`、浏览器自动化、Burp 对接等能力属于高风险工具，应在隔离环境运行。
- 自动漏洞利用可能误伤目标系统，尤其是生产站点、第三方服务和共享环境。
- 模型仍可能误判、漏报或生成不可执行 PoC；报告必须由安全人员复核。
- 多模型 API key、目标信息和扫描结果都可能包含敏感数据，应做好本地存储和日志清理。

## 补充建议

- 首次测试应使用本地靶场、CTF 或明确授权的演练环境。
- 为 agent 设置网络出口、目标域名、命令执行和时间预算白名单。
- 把生成报告中的每条漏洞结论映射到工具输出、请求响应和复现步骤。
- 与 `strix`、`SkillSpector`、`nvidia-skills` 一起观察 agent 安全赛道：应用漏洞验证、skill 供应链审计和官方能力目录会逐渐分化。

## 参考资料

- GitHub 仓库：https://github.com/Unclecheng-li/VulnClaw
- PyPI 项目页：https://pypi.org/project/vulnclaw/
- MCP 官方站点：https://modelcontextprotocol.io/
- GitHub API 元数据：https://api.github.com/repos/Unclecheng-li/VulnClaw
