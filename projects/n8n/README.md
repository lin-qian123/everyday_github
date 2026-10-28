<!-- markdownlint-disable MD013 -->

# n8n

## 定位

n8n 是将可视化节点、自定义代码、外部服务与 AI Agent 组合成工作流的平台，可自托管或使用云服务。它适合把检索、模型调用、人工审核和业务系统连接起来；上游自称 fair-code / source available，许可范围需独立检查。

2026-10-29 快照：TypeScript daily +147 stars；API 208,909 stars / 61,287 forks / 1,193 open issues（含 PR）。核读主线 `0b04add5b381`；发行 API 首项是可移动标签 stable，2026-10-28 UTC 发布，说明正文对应 2.45.5。这里区分主线与发行，未启动服务或创建真实工作流。

## 用法

1. 从上游部署文档选择云端或 Docker；本地试用只绑定回环地址，保留数据卷并先完成账户初始化。
2. 用合成数据创建“手动触发 → 数据变换 → 结果检查”工作流，再加入一个受限的模型或只读服务凭据。
3. 将写入、发送、删除等节点放在人工确认之后，检查失败重试是否会重复外部动作。

下面依据 README 的容器方式收窄监听，并固定到本轮 stable 正文版本，供审阅后试用：

```bash
docker volume create n8n_data
docker run -it --rm --name n8n \
  -p 127.0.0.1:5678:5678 \
  -v n8n_data:/home/node/.n8n \
  -e N8N_DIAGNOSTICS_ENABLED=false \
  -e N8N_VERSION_NOTIFICATIONS_ENABLED=false \
  docker.n8n.io/n8nio/n8n:2.45.5
```

这不是生产部署配置，也不是断网配置。本轮未拉取该镜像或运行命令；正式使用还要按制品 digest、代理 / TLS、备份和访问权限验收。

## 原理

触发节点提供输入，后续节点在图上执行转换、条件分支、API 调用与工具动作，AI 节点可接不同模型。可视化编辑降低了连接服务的门槛，实际工作仍由节点代码、凭据、网络和运行环境执行。自托管决定服务运行位置，数据是否外发取决于具体节点、provider 与平台配置。

## 价值

- 把分散 API、表单、文档与 AI 步骤组织成可审阅流程。
- 支持在低代码界面中保留代码扩展与人工审核节点。
- 能用小规模合成任务验证流程，再逐步评估可靠性和运维成本。

## 风险边界

- 根 LICENSE 对主要适用部分使用 Sustainable Use License；含 `.ee.` / `.ee` 的部分受 Enterprise 条款约束，第三方组件保留各自许可。不能将源码公开理解为无条件商业托管 / 转售授权。
- 官方文档说明自托管默认收集遥测。`N8N_DIAGNOSTICS_ENABLED=false` 关闭诊断事件，版本通知另有开关；二者不约束工作流主动连接的外部服务。
- 持久化目录涉及数据库和凭据加密密钥，备份需同时考虑恢复可用性与秘密保护；加密凭据不代表执行记录、输出和日志都没有敏感数据。
- 社区节点、代码节点及导入模板属于要审阅的执行内容。公开 webhook、过宽 OAuth scope、AI 工具调用和重试都会扩大外部动作范围。
- 企业级能力的产品介绍不能证明当前部署已具备对应授权、访问控制或审计配置。

## 补充建议

以一次可撤销的内部任务验收：固定镜像、导出工作流，记录输入输出、重试次数、模型费用、凭据 scope 与回滚方式。上线前测试超时、重复回调、撤销凭据和数据恢复，并按实际业务模式核许可。若必须限制平台出口，继续阅读官方 isolate 指南并做网络验证。

## 参考资料

- [上游仓库](https://github.com/n8n-io/n8n)、[GitHub API](https://api.github.com/repos/n8n-io/n8n)。
- [固定 README：平台与容器入口](https://github.com/n8n-io/n8n/blob/0b04add5b381f59a013d7a27c5680a7f7c8966be/README.md)。
- [Sustainable Use 与适用范围](https://github.com/n8n-io/n8n/blob/0b04add5b381f59a013d7a27c5680a7f7c8966be/LICENSE.md)、[Enterprise 条款](https://github.com/n8n-io/n8n/blob/0b04add5b381f59a013d7a27c5680a7f7c8966be/LICENSE_EE.md)。
- [stable 发行快照入口](https://github.com/n8n-io/n8n/releases/tag/stable)（标签可移动）、[官方遥测控制](https://docs.n8n.io/deploy/host-n8n/configure-n8n/security/control-telemetry.md)、[部署环境变量](https://docs.n8n.io/deploy/host-n8n/configure-n8n/basic-configuration/use-environment-variables/deployment.md)。
