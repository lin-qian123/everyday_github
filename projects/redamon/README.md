<!-- markdownlint-disable MD013 -->

# RedAmon（samugit83/redamon）

> 上游仓库：<https://github.com/samugit83/redamon> · 归类：Agent 框架与技能生态 · 本页基于 2026-09-29 的 GitHub API、README、Disclaimer、Security Posture / threat model、Release、第三方许可证清单与 LICENSE 静态整理；未安装或运行任何扫描、利用、凭据测试、横向移动或修复 Agent。

- 抓取快照：2,747 stars、567 forks、16 open issues。
- 热度信号：GitHub Python Trending 抓取时约 +97 当日 stars。
- 版本与许可：根代码 MIT；latest GitHub Release 为 `v6.14.1`，根 `VERSION` 已为 `6.20.0`，存在发布面漂移；集成工具另含 GPL / AGPL / WPScan Public Source License 等条款。

## 定位

RedAmon 是高风险的 agentic red-team 平台，把 reconnaissance、漏洞验证、exploitation、post-exploitation、AI triage、代码修复与 GitHub PR 串成一条自动化链。它只适用于自有系统或有明确书面授权的安全测试、教学靶场与研究，不能因为代码开源就扩大攻击授权。

## 用法

上游以 Docker Compose 启动 webapp、Postgres、Neo4j、agent、Kali sandbox、recon orchestrator 与 Docker broker；可选 OpenVAS / GVM 和本地知识库会显著增加镜像、磁盘与启动时间。配置 LLM provider、OSINT / threat-intel keys 和目标后，用户从 Web UI 创建 project 并启动扫描。默认 raw stack 仅适合可信本地网络；对外服务必须使用上游 hardened single-host deploy，并仍需组织自己的访问、审计与测试授权。

## 原理

六阶段 recon pipeline 把多种安全工具输出汇总、去重并写入 Neo4j attack graph；LangGraph / ReAct Agent 再查询图谱、选择工具、验证路径。CypherFix 对发现做关联与排序，CodeFix Agent 可 clone 代码、实施补丁并创建 PR。Docker-socket proxy 只允许编排已知 tool images，但容器、模型与网络仍组成高权限攻击执行面。

## 价值

对合法红队，RedAmon 的价值在于把工具调用、attack graph、raw session、walkthrough 与修复提案放进同一可追溯流程，便于复盘遗漏和人工验证。上游公开 XBOW 解题记录与 coverage audit，可作为复现实验入口；它们仍是作者生成 / 自评材料，不能直接写成独立安全效果证明。

## 风险边界

- 自主扫描、exploit、凭据策略测试、横向移动和 secret hunting 都可能造成真实入侵、数据泄露、服务中断或违法；目标 scope 必须来自书面授权并技术强制。
- 上游明确指出 raw stack 若直接暴露公网会暴露未认证内部服务；即使使用 hardened deploy，也不能替代 tenant、MFA、网络分段和 incident response。
- 平台集中 LLM、Shodan、Censys、Vulners、GitHub 等高价值 keys，并保留 scan artifact、图数据库与日志；prompt injection、恶意目标响应与模型误判会沿工具链传播。
- Docker / Kali / OpenVAS / WPScan 等供应链与容器权限需要独立审计；WPScan Public Source License 还限制部分商业产品 / SaaS 使用。
- 自动创建的修复 PR 可能改变安全语义或引入回归；“找到 exploit”与“安全修复完成”必须由不同人员和测试链确认。

## 补充建议

只在隔离靶场或明确列出的 CIDR / domain / account scope 运行，并在网络层 allowlist 目标与 egress；使用无生产 secret 的专用主机、provider 账号和 GitHub 测试组织。禁用默认不需要的 exploit / credential / post-exploitation 能力，为每阶段设置人工闸门、速率与停止条件。保存不可篡改审计记录但为敏感 artifact 设置最短 retention；补丁必须经独立 review、回归与部署审批。

## 参考资料

- [GitHub 仓库](https://github.com/samugit83/redamon)
- [GitHub REST API](https://api.github.com/repos/samugit83/redamon)
- [v6.14.1 Release](https://github.com/samugit83/redamon/releases/tag/v6.14.1)
- [Legal Disclaimer](https://github.com/samugit83/redamon/blob/master/DISCLAIMER.md)
- [Security Posture](https://github.com/samugit83/redamon/blob/master/docs/readmes/README.SECURITY_POSTURE.md)
- [Threat Model](https://github.com/samugit83/redamon/blob/master/docs/readmes/README.TM.SYSTEM_OVERVIEW.md)
- [Third-party licenses](https://github.com/samugit83/redamon/blob/master/THIRD-PARTY-LICENSES.md)
- [Security Policy](https://github.com/samugit83/redamon/blob/master/SECURITY.md)
- [LICENSE](https://github.com/samugit83/redamon/blob/master/LICENSE)
