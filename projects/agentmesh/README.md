<!-- markdownlint-disable MD013 -->

# Agent Mesh（google/agentmesh）中文解读

> 上游仓库：<https://github.com/google/agentmesh> · 归类：Agent 框架与技能生态 · 本页基于 2026-10-15 的 README、安全架构、隐私文档、SDK / 部署入口、Release、许可证与 GitHub REST API 静态整理；未加入公共 testnet、部署控制面或验证跨云策略与密码学实现。

## 定位

Agent Mesh 是跨笔记本、容器、集群、云和移动设备连接 AI Agent / tool / model 的私有网络。每个 Agent 旁运行 node，发布或发现 MCP、A2A、inference、egress 服务；control plane 负责身份、策略和短时凭据，router 负责发现与 NAT relay，调用尽量点对点传输。

## 用法

快速体验会下载 `agentmesh-node` 并加入上游共享 testnet，再在本机 `127.0.0.1:8080` 暴露 MCP / OpenAI-compatible 入口。严肃评估应部署自己的 `agentmesh-one` 或分离 control-plane / router，接入 OIDC / workload identity，先只发布无副作用工具，再为明确 subject、service、tool、method、path 与 TTL 编写最小 policy。

## 原理

- 节点以 OIDC、Kubernetes SA、GCE / Cloud Run、SPIFFE JWT 等证明身份，control plane 签发与节点 key 绑定的短时 Biscuit credential。
- 父 Agent 可追加只能收窄权限的 task authorization block，服务端在每跳重新验证。
- node 间通过加密、相互认证的 libp2p stream 通信；router 只转发 NAT 后的密文。
- egress node 可把 task identity 换成云端 token 或代持静态 API key，并生成可按 principal / task 关联的审计记录。

## 价值

- 将“谁在调用、哪次任务、可用哪些服务 / 工具”从 IP 与长期 key 中分离，适合多 Agent 委派和跨环境调用。
- 默认不暴露服务、按 service name 授权、下游凭据不交给 Agent，可降低 ambient credentials 的 blast radius。
- 安全文档主动列出未解决边界与不同云 IAM 的残余权限，比只宣传 zero-trust 更利于工程审计。

## 风险边界

- 上游明确说明它不提供 OS、文件系统、容器或网络 namespace sandbox；被允许的 Agent 仍可能在本机读写任意宿主可访问资源。
- API-key provider 无法在上游按任务缩权；mesh 只能限制 service / method / path，最终权限上限仍由静态 key 决定。
- Google Cloud 的请求 body、opaque TCP 等场景存在策略看不到的语义；加密与 policy 通过也不证明工具调用意图安全。
- 项目 pre-1.0，sandbox blueprint 与 mobile app 仍为 preview；共享 testnet 无 uptime 承诺。`v0.1.0-rc.10` 名称仍是 RC，即使 GitHub API 的 prerelease 字段为 false。

## 补充建议

- 在自建 mesh 中用 mock MCP 和假 secret 做 allow / deny / delegation / expiry / revocation / router compromise 测试，不把公共 testnet 接真实数据。
- 将 Agent Mesh 与 gVisor / Kata / Landlock、Kubernetes NetworkPolicy、provider-side IAM 和人工写操作审批组合，而不是替代它们。
- 保存 policy revision、task chain、双端 audit 与 cloud audit，做跨租户、body-level bypass 和断网 / 重放故障注入。

## 参考资料

- GitHub 仓库：<https://github.com/google/agentmesh>
- GitHub REST API：<https://api.github.com/repos/google/agentmesh>
- `v0.1.0-rc.10` Release：<https://github.com/google/agentmesh/releases/tag/v0.1.0-rc.10>
- 项目文档：<https://google.github.io/agentmesh/docs/>
- Security architecture：<https://github.com/google/agentmesh/blob/main/site/content/docs/contributing/security-architecture.md>
- Privacy：<https://github.com/google/agentmesh/blob/main/site/content/docs/privacy.md>
- LICENSE：<https://github.com/google/agentmesh/blob/main/LICENSE>
