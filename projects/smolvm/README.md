<!-- markdownlint-disable MD013 MD034 -->

# smolvm：面向 Agent 与不可信任务的可分支轻量 microVM

> 上游仓库：https://github.com/smol-machines/smolvm · 归类：Agent 框架与技能生态 · 本页基于 2026-09-21 的 README、security model、examples、release 与许可证静态整理；未安装 VMM、启动 VM、复现分支性能或执行逃逸测试。

## 定位

`smol-machines/smolvm` 是 Rust 编写的跨平台 microVM CLI / SDK，把 OCI image 作为独立 Linux VM 启动，并可把运行中机器 checkpoint、branch、打包为 `.smolmachine`。对 Agent 场景，它提供比共享宿主内核容器更清晰的 guest / host 边界，也支持从同一已预热状态派生并行 worker。

2026-09-21 的 GitHub 官方 Rust Trending 抓取显示约 `+40 stars today`；REST API 快照为 `6,184 stars / 297 forks / 79 open issues`，Apache-2.0，最新 release 为 `v1.16.2`（9 月 18 日）。

## 用法

上游提供安装脚本与 GitHub Release；高信任环境应先检查脚本和 release evidence，再安装：

```sh
smolvm machine run --image alpine -- sh -c 'uname -a'
smolvm machine create --name source --image python:3.12-alpine --net
smolvm machine start --name source --branchable
smolvm machine branch --from source --count 8 --name-prefix worker --parallel 8
```

`Smolfile` 可声明 image、CPU、内存、网络、端口、mount、init、workdir、user、GPU 与 egress allowlist；未知字段会失败而不是静默忽略。

## 原理

- macOS 使用 Hypervisor.framework，Linux 使用 KVM，Windows 使用 Windows Hypervisor Platform；`libkrun` 提供 VMM，guest 拥有独立 kernel。
- OCI image 转为 VM root filesystem；每个 workload 由单独 VMM 进程运行，无需常驻 Docker daemon。
- branch 对运行态的 memory 与 disk 做 checkpoint，并以 copy-on-write 派生 child；worker 可用 ready protocol 标记预热完成。
- `.smolmachine` 将停止的状态打包为可移植 artifact；同架构主机可从 registry pull 后恢复。
- 网络默认关闭；启用后可配 host allowlist、端口映射。显式 mount、SSH agent、Docker socket、GPU 与 host service 都会扩大 guest authority。

## 价值

- 适合 Agent 生成代码、并行评测、浏览器任务和可恢复开发环境等短生命周期 workload。
- live branch 可复用模型 / 依赖预热状态，减少多个 worker 重复初始化；实际节省需按 workload 测量。
- Smolfile 和打包 artifact 有利于复现环境并减少“本机已经配好”的隐性状态。
- Kubernetes RuntimeClass、headless browser、local LLM 与 Docker-in-VM 示例便于接入现有平台。

## 风险边界

- microVM 不是完整的恶意多租户控制面；host user、OS、hypervisor backend、libkrun、VMM 和 smolvm 都属于 trusted computing base。
- `--volume`、`--ssh-agent`、`--net`、port、Docker socket 和 host service 是显式能力穿透，可能让不可信 guest 读写宿主或请求签名。
- release checksum 缺失时 installer 仍允许安装，且当前 release 未签名、无 provenance attestation；不能把 checksum 叙述升级成完整供应链保证。
- GPU 访问由 host process / shared GPU 调解，不是 hardened multi-tenant GPU isolation；Windows 尚不支持 branch / checkpoint 与 GPU。
- 上游 `<200ms` cold start 与比较表是项目自报数据，本页未在固定硬件、镜像和缓存条件下复现。

## 补充建议

1. 固定 `v1.16.2`、libkrun、guest image digest 和 host kernel，先跑无 secret、无 mount、无网络的合成任务。
2. 建立能力矩阵：network、volume、SSH agent、GPU、Docker socket 每次只开放一项，并记录 guest 实际可达面。
3. 用恶意文件、资源耗尽、fork storm、DNS / redirect 与 snapshot secret persistence 做对抗测试。
4. 不直接 pipe 远程安装脚本到 shell；下载、审阅、校验 release，并保留内部镜像和回滚版本。

## 参考资料

- 上游 README：https://github.com/smol-machines/smolvm
- Examples：https://github.com/smol-machines/smolvm/tree/main/examples
- 安全策略：https://github.com/smol-machines/smolvm/blob/main/SECURITY.md
- `v1.16.2` release：https://github.com/smol-machines/smolvm/releases/tag/v1.16.2
- GitHub REST API：https://api.github.com/repos/smol-machines/smolvm
- LICENSE：https://github.com/smol-machines/smolvm/blob/main/LICENSE
