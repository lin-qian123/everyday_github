<!-- markdownlint-disable MD013 -->

# HexStrike AI（0x4m4/hexstrike-ai）

> 上游仓库：<https://github.com/0x4m4/hexstrike-ai> · 归类：Agent 框架与技能生态 · 本页基于 2026-10-07 的 GitHub API、README、server / MCP 源码、依赖清单与 LICENSE 静态整理，未安装安全工具、扫描任何目标或执行 payload。

- 抓取快照：12,462 stars、2,539 forks、114 open issues。
- 热度信号：GitHub Python Trending 抓取时约 +59 当日 stars；最后 push 为 2026-08-03，属于旧项目重新上榜。
- 版本与许可：README 自称 `v6.0.0`，但 API 无 Release / tag；MIT；本页固定审计 commit `d689933ff579`。

## 定位

HexStrike AI 是把大量渗透测试、云安全、二进制、取证、OSINT 与浏览器工具包装成 HTTP API 和 MCP 的安全自动化平台。上游宣传 150+ 外部工具、12+ Agent 与自动工具选择；它是高权限 offensive control plane，不是通用安全扫描器或默认安全的 Agent sandbox。

## 用法

只能在自有或书面授权的隔离靶场使用。上游流程是创建 Python 虚拟环境、安装 `requirements.txt`，启动 `hexstrike_server.py`，再让 `hexstrike_mcp.py` 连接本机 8888 端口；大量 nmap、sqlmap、Ghidra、云 CLI 等工具仍需分别安装。正式试验前应先删减到明确 allowlist，并把 server 置于无生产凭据、无公网路由的容器 / VM 中。

## 原理

MCP 端把 Agent tool call 转发到 Flask server；server 为 reconnaissance、Web、密码、云、二进制、CTF、浏览器与 payload 流程构造命令，交给进程管理器执行，再缓存、汇总或可视化结果。源码还暴露通用 command / Python 执行、异步任务与恢复接口；默认末尾以 `0.0.0.0` 监听 8888 端口。

## 价值

在明确授权的实验环境，它能把异构安全工具的参数、长任务、结果和 Agent 调用方式集中起来，适合做 CTF、内部演练和自动化编排原型。README 与代码也提供了一份广泛工具目录，便于研究如何把长耗时安全任务纳入 MCP。

## 风险边界

- 未经授权的扫描、口令攻击、利用、payload、OSINT 或云操作可能违法并造成真实损害；项目能力本身不提供授权，必须以书面 scope、目标 allowlist、时间窗和停止条件约束。
- server 默认绑定 `0.0.0.0`，源码含通用命令 / Python 执行与大量高权限路由；本轮未看到足以把它当多租户安全边界的认证、RBAC 或网络隔离，严禁直接暴露到 LAN / Internet。
- 参数校验、timeout、cache 和错误恢复不是命令 sandbox；字符串拼接、外部 CLI、浏览器与云凭据共同放大命令注入和横向移动风险。
- 150+ 工具必须另行安装，各有版本、许可、数据库、更新源和供应链；README 数量与 Agent 能力主张未逐项运行核验。
- README 自称 v6.0.0，但仓库没有 Release / tag；浮动 `main` 与安装说明不足以形成可复现发行 provenance。
- 自动 exploit / payload 与“zero-day research”命名不代表有效、合规或无副作用；生成结果必须由有资质人员在靶场人工审查。

## 补充建议

先 fork 到私有测试仓库，移除通用 command / Python 与未使用路由，只保留少量只读枚举工具；强制 loopback、反向代理认证、容器非 root、只读文件系统、出站 allowlist、CPU / 内存 / 时间配额和完整审计。用故意无漏洞的 fixture 测误报，用有标注的靶场测召回，并验证越界参数、并发、取消、日志脱敏和紧急停机。

## 参考资料

- [GitHub 仓库](https://github.com/0x4m4/hexstrike-ai)
- [GitHub REST API](https://api.github.com/repos/0x4m4/hexstrike-ai)
- [README 与架构](https://github.com/0x4m4/hexstrike-ai/blob/master/README.md)
- [HTTP server 源码](https://github.com/0x4m4/hexstrike-ai/blob/master/hexstrike_server.py)
- [MCP client 源码](https://github.com/0x4m4/hexstrike-ai/blob/master/hexstrike_mcp.py)
- [Python 依赖与外部工具清单](https://github.com/0x4m4/hexstrike-ai/blob/master/requirements.txt)
- [MIT License](https://github.com/0x4m4/hexstrike-ai/blob/master/LICENSE)
- [上游安装演示](https://www.youtube.com/watch?v=pSoftCagCm8)
