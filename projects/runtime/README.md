<!-- markdownlint-disable MD013 MD034 -->

# E2B Runtime：Agent Cloud 背后的 Firecracker 沙箱控制面

> 上游仓库：https://github.com/e2b-dev/runtime · 归类：Agent 框架与技能生态 · 本页基于 2026-09-18 的 README、architecture、Embed 文档、release、LICENSE 与 REST API 静态整理；未部署 KVM / Firecracker 集群，也未做逃逸测试。

## 定位

E2B Runtime 是 E2B Cloud、企业部署和单机 Embed 共用的开源后端：API 负责 sandbox lifecycle 与 placement，node orchestrator 驱动 Firecracker microVM，`envd` 在 VM 内暴露进程、PTY、文件和端口接口，template / snapshot 支撑快速创建、暂停、恢复和 fork。

2026-09-18 的 GitHub 官方 Go Trending 抓取显示约 `+125 stars today`；REST API 快照为 `1,565 stars / 431 forks / 204 open issues`，Apache-2.0，最新 release 为 `2026.30`（9 月 10 日）。

## 用法

最快路径是使用 E2B Cloud SDK；自托管评估可在支持 KVM 的 Linux 主机上启动 Embed：

```sh
mkdir e2b && cd e2b
curl -fsSL --remote-name-all \
  "https://raw.githubusercontent.com/e2b-dev/runtime/main/embed/compose/{compose.yaml,.env}"
docker compose up -d --wait
```

上游明确称 Embed 是 evaluation package，不是生产部署模式。源码开发还需要 PostgreSQL、Redis、ClickHouse、KVM、网络和对象存储等基础设施。

## 原理

- template 预启动 VM 并保存内存、磁盘和机器状态；创建 sandbox 实际是恢复 snapshot。
- `userfaultfd` 按页懒加载内存，root filesystem 使用只读镜像上的 copy-on-write overlay。
- API 只决定放置和状态；每节点 orchestrator 管理 Firecracker、network namespace、block device、cgroup 与 nftables egress。
- pause 保存相对 template 的内存 / 磁盘 diff，resume 优先使用节点缓存；live fork 从同一 checkpoint 派生多个 sandbox。
- client proxy 将 `<port>-<sandbox>.<domain>` 路由到节点；`envd` 提供 SDK 实际调用的执行 API。

## 价值

- 比进程或容器级隔离提供更清楚的 microVM 边界，适合运行 Agent 生成的不可信代码。
- snapshot、lazy restore 和 fork 让短生命周期、并行试验和可恢复任务更高效。
- 同一代码覆盖 cloud、dedicated 和单机 evaluation，便于从黑盒 SaaS 迁到自有基础设施。
- architecture、network、identity、secret 与 observability 组件公开，平台团队可审计实际控制面。

## 风险边界

- Firecracker microVM 降低但不消除 guest escape、kernel、KVM、host、orchestrator 和供应链风险；“hardware-isolated”需要持续补丁和对抗验证。
- sandbox URL、端口代理、持久 volume、snapshot、template 与 object storage 都可能泄露跨任务数据；fork 还会复制 checkpoint 中的 secret 或状态。
- egress firewall 与域名 allow / deny 依赖 DNS、SNI / Host、代理和应用协议；不能假设默认阻止所有 exfiltration。
- README 的 metadata-only secret 与 workload identity 设计仍需核验日志、trace、crash dump、guest memory 和 token 撤销路径。
- 单机 Embed 不是生产 HA / hardening 模式，直接照抄 compose 到公网会暴露控制面和节点能力。
- 本页未运行 `2026.30`，未测启动延迟、pause/resume 数据一致性、跨租户隔离、网络旁路或灾难恢复。

## 补充建议

1. 在专用 KVM host 上从无 secret 的合成 workload 开始，对 VM、network、volume、snapshot 与 template 做租户交叉测试。
2. 默认拒绝 egress，仅对白名单域名、方法和端口开放；用 DNS rebinding、redirect、raw IP、tunnel 与长连接测试绕过。
3. 为 template / snapshot / volume / object storage 设置加密、租户 key、TTL、删除证明和备份恢复演练。
4. 固定 host kernel、Firecracker、runtime release 与镜像 digest，独立运行逃逸、资源耗尽、noisy neighbor 和 token 撤销评测。

## 参考资料

- 上游 README：https://github.com/e2b-dev/runtime
- 架构文档：https://github.com/e2b-dev/runtime/blob/main/docs/ARCHITECTURE.md
- 单机 Embed：https://github.com/e2b-dev/runtime/blob/main/embed/README.md
- `2026.30` release：https://github.com/e2b-dev/runtime/releases/tag/2026.30
- GitHub REST API：https://api.github.com/repos/e2b-dev/runtime
- LICENSE：https://github.com/e2b-dev/runtime/blob/main/LICENSE
