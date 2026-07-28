# frieren-dast-ai

## 定位

`frieren-dast-ai` 是 KnowBe4 InfoSec 团队维护的动态应用安全测试工具：它将 HTTPS MITM 代理、被动规则扫描、主动队列、多 agent 漏洞检查与实时 Web 仪表板组合在一起。

截至 2026-07-29，GitHub API 显示其创建于 2026-07-28，约 18 stars，采用 Apache-2.0；星标仍很早期，不能据此判断扫描准确率或企业可用性。

## 用法

只在明确书面授权且隔离的目标上使用。项目的快速开始会安装依赖、配置 AWS SSO、启动本机代理与 dashboard；浏览器随后被显式配置到 `127.0.0.1:8080`，并安装测试 CA 证书。

```bash
make setup
make sso-configure
make sso
make proxy
```

执行前须限定 scope、使用测试账户并记录授权。MITM CA、代理流量、AWS 凭据和扫描结果都不应进入共享仓库或非受控日志。

## 原理

代理截获 HTTP/HTTPS 请求与响应后，先用 YAML 规则做零额外请求的被动检查；在范围内的端点再进入队列，由协调器安排 XSS、SQLi、SSRF、认证、LLM prompt injection 等专门 agent，并由 LLM validator 与仪表板回传发现。它还提供浏览、爬取、参数挖掘与 GraphQL 辅助入口。

## 价值

- 将被动发现与可暂停的主动扫描接在同一可见工作台，便于安全工程师复核证据。
- LLM 端点、业务逻辑与传统 Web 面可在同一授权测试流程中编排。

## 风险边界

- 主动攻击面探测可能触发破坏性请求、误报、告警或合规问题；必须遵守授权、范围和变更窗口。
- HTTPS 解密会接触 cookie、令牌和业务数据，CA 私钥与会话存储需要严格隔离和清理。
- 多 agent 与 LLM validator 不能证明漏洞真实存在；任何发现都必须由人工复现、分级与修复验证。

## 补充建议

先在靶场或 staging 仅启用被动规则，再逐项放开主动插件；为每种 payload 建立速率、超时、停止条件和审计日志，并由独立人员复核高危结论。

## 参考资料

- GitHub：<https://github.com/knowbe4/frieren-dast-ai>
- GitHub API 快照：<https://api.github.com/repos/knowbe4/frieren-dast-ai>
