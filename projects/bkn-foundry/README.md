<!-- markdownlint-disable MD013 -->

# bkn-foundry（openbkn-ai/bkn-foundry）

- GitHub：<https://github.com/openbkn-ai/bkn-foundry>
- 抓取快照：2026-09-23，537 stars、51 forks、199 open issues
- 热度信号：GitHub Go Trending 抓取时约 +22 当日 stars
- 版本与许可：API 为 `NOASSERTION`；latest GitHub Release `v0.1.4`，tag 有 `v0.1.5`，仓库 `VERSION` 为 `0.2.0`；按文件在 Apache-2.0 与 OpenBKN License 间多许可

## 定位

BKN Foundry 是 OpenBKN 的后端基础设施，用 ontology-driven business knowledge network 把企业数据、规则、动作和风险组织成 Agent 可检索、可执行、可追踪的对象。它包含数据虚拟化、Context Loader、execution factory、权限 / policy、安全审计和 trace；Web Studio 与 SDK 在独立仓库，不属于本仓库交付。

## 用法

完整安装面向 Linux / Kubernetes，先用 `preflight.sh` 检查主机，再由 `deploy.sh` 安装服务；`onboard.sh` 可注册 LLM / embedding、创建用户并写入 CLI token。客户端另装 `bkn-sdk` / `openbkn` CLI，登录实例后管理 knowledge network、context、model、agent、admin 与 trace。默认示例密码、自签名 `-k` 和全角色测试用户只适合隔离环境。

## 原理

BKN Lang 用 Markdown 表达 Object、Relationship、Risk、Action；VEGA 统一底层多源数据，Context Loader 做 recall、coarse rank、fine rank，Exec Factory 编排 tools / MCP / skills，BKN Safe 在对象 / 动作层执行身份与 policy，BKN Trace 记录从意图、知识节点、数据源到最终调用的证据链。

## 价值

它试图把企业 Agent 的“取什么上下文、为何选择工具、谁有权执行、执行后如何追溯”放入统一语义层。对于规则多、系统多、审计要求高的场景，这比把长文和所有工具直接塞进 prompt 更便于治理，也提供了完整的部署、API 和样例入口。

## 风险边界

- README 的 93%+、99%+ accuracy、15%+ improvement、30%+ token reduction 和 300% build efficiency 都是作者在特定 HR / BIRD 派生样本上的报告，本轮未独立复现。
- ontology / policy 写错会把业务错误固化为“可解释”路径；有 trace 不等于来源正确、规则完备或动作安全。
- 安装脚本涉及 `sudo`、Kubernetes、默认测试用户、模型 key 和持久 token；必须先审阅脚本、替换默认凭据并限制集群 / 网络范围。
- 版本存在 `v0.1.4` latest Release、`v0.1.5` tag 与仓库 `0.2.0` 三重漂移，部署时须锁定具体 commit 与组件矩阵。
- 多许可证按文件头适用；OpenBKN License 对商业 entitlement、共享 / 多租户 hosted service、logo 和 license check 有额外限制，不能整体称 Apache-2.0。

## 补充建议

先用一个低敏感、规则可穷举的小业务域建立 golden ontology、action allowlist 和错误注入集，分别测 retrieval、policy、trace 与真实后端副作用。对 benchmark 固定样本、模型、embedding、并发、cost 口径和失败样本；上线前审计每个文件 / 组件的许可证以及 SDK / Studio 的独立条款。

## 参考资料

- [GitHub 仓库](https://github.com/openbkn-ai/bkn-foundry)
- [GitHub REST API](https://api.github.com/repos/openbkn-ai/bkn-foundry)
- [README 架构章节](https://github.com/openbkn-ai/bkn-foundry#core-architecture)
- [部署说明](https://github.com/openbkn-ai/bkn-foundry/tree/main/deploy)
- [v0.1.4 Release](https://github.com/openbkn-ai/bkn-foundry/releases/tag/v0.1.4)
- [许可证总览](https://github.com/openbkn-ai/bkn-foundry/blob/main/LICENSE)
- [OpenBKN License](https://github.com/openbkn-ai/bkn-foundry/blob/main/LICENSE-OPENBKN.txt)
