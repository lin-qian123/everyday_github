<!-- markdownlint-disable MD013 -->

# Kortix CompanyOS

## 定位

CompanyOS 是 Kortix 面向团队的云端 agent 运行与协作平台，将代理、技能、连接器和规则纳入工作区仓库，用事件、计划任务和会话推动工作。它有托管云与自托管路线；“公司操作系统”是产品组织方式，结果仍需业务验收。

- 上游：[kortix-ai/CompanyOS](https://github.com/kortix-ai/CompanyOS)，仓库 ID `868173144`；现有项目映射未发现同一上游。
- 2026-11-10：20,604 stars / 3,468 forks / 62 open issues（含 PR）；TypeScript daily +27。
- 稳定发行 [v0.15.2](https://github.com/kortix-ai/CompanyOS/releases/tag/v0.15.2)，UTC 11-09；默认分支 `dev` 的 VERSION 已为 0.15.3。本页按 `7cce1ec4dc28f21fa2f302950a203f3ac869c625` 静态核读。

## 用法

1. 托管路线在官网建工作区并配 agent、模型和连接器；CLI 以 `kortix init` 生成 `kortix.yaml` 等文件，再用 `kortix ship` 部署。后者涉及远端资源与费用，先审配置和目标 host。
2. README 自托管入口为 `kortix self-host start`，随后 `kortix hosts use selfhost`；它会拉 Docker Hub 镜像，sandbox 默认走 Platinum，模型 key 和 GitHub 后续配置。自托管不等于离线。
3. 从单个测试任务开始，分别配置 agent 权限、connector Allow / Ask / Block、secret audience 与传递方式，核 session、artifact、变更和审计记录。
4. 计划任务 / 长期 outcome 先定义完成条件、预算与停止机制，再验证独立 verifier 的判据。

本轮未执行安装脚本、登录、部署、连接第三方账号或运行 agent。

## 原理

文档将计算与状态分离：每个 session 有单独云计算机，空闲后休眠；仓库、Drive、`/workspace` 与 session record 保存不同状态。My Kortix 路由到专用 agent，事件和 workflow 驱动多会话协作，上下文耗尽后检索原始记录。

连接器凭据保留服务端，由代理调用时应用规则；普通 secret 则可作为真实环境变量进入 sandbox，或通过 egress-enforced 以占位值出站替换。两类机制不能概括成“全部凭据永不进入机器”。

## 价值

- 组合团队协作、事件触发、持久状态和结果审查，适合评估持续业务流程。
- 仓库化配置有利于版本管理、迁移与审查；云会话减少任务随本地休眠中断。
- “数千 agent”“3,000+ apps”与案例是上游宣传范围，本轮未核规模压测、连接器逐项质量或独立客户效果。

## 风险边界

- **人工批准存在例外**：README 广义称变更由人审查，但同 SHA Guide 明确警告 `worker` 持有全部 Kortix 权限，可合并自己的 change request，目前靠 standing instructions 要求仅在用户请求时合并。要强制每次人审，需移除 merge 权限。
- **秘密与共享**：Guide 的 secret audience 默认为工作区所有人；环境变量方式让会话代码得到真实值。egress-enforced 是另一条路径，需按目标地址、实际请求和日志验证。
- **持续成本**：触发、模型回退、休眠 / 唤醒、连接器与持久存储分别消耗资源；计算机休眠不代表全部账单停止。
- **根许可**：LICENSE 是 Elastic License 2.0，限制把实质功能作为第三方托管 / 管理服务提供、绕过许可功能和移除许可声明，不能写成无条件 MIT / Apache 开源。
- **白标另签**：默认免费白标须签以 Platinum 为独家计算提供方的协议，含范围扩展、终止和通知变更条款；“free”不能推导无供应商约束。
- sandbox、SOC 2 和隔离均是上游陈述，本轮未审认证报告或实测跨会话、网络、凭据与租户边界。

## 补充建议

先导出有效权限表：谁能读仓库、用 secret、调用 connector、审批和 merge。用公开资料小任务核暂停 / 恢复、事件去重、预算、回滚和 verifier 独立性；自托管 / 白标应分别对照控制面、计算提供方、模型出口与许可范围。

## 参考资料

- [固定 SHA README：架构与入口](https://github.com/kortix-ai/CompanyOS/blob/7cce1ec4dc28f21fa2f302950a203f3ac869c625/README.md)
- [Guide：worker 例外、秘密与连接器](https://github.com/kortix-ai/CompanyOS/blob/7cce1ec4dc28f21fa2f302950a203f3ac869c625/apps/web/content/docs/guide.mdx)
- [根许可证](https://github.com/kortix-ai/CompanyOS/blob/7cce1ec4dc28f21fa2f302950a203f3ac869c625/LICENSE)
- [白标协议](https://github.com/kortix-ai/CompanyOS/blob/7cce1ec4dc28f21fa2f302950a203f3ac869c625/WHITE-LABEL-LICENSE.md)
- [主线 VERSION](https://github.com/kortix-ai/CompanyOS/blob/7cce1ec4dc28f21fa2f302950a203f3ac869c625/VERSION)、[官网指南](https://kortix.com/docs/guide)
