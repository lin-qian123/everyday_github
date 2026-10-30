<!-- markdownlint-disable MD013 -->

# mesh-llm

## 定位

Mesh LLM 将多台机器的 GPU / 内存组织为推理网络，对外提供 OpenAI 兼容接口；单机 Skippy runtime 与 Mesh host 位于同一 Cargo 工作区。它覆盖本机模型、分片、多节点路由和实验性 Mixture-of-Agents，不是“联网后任意闲置 GPU 都能无代价合并”。

2026-10-31 采样：Rust daily +37 stars；API 累计 3,681 stars / 478 forks / 195 open issues（含 PR）。核读 main `5e2fdddf6a6e`；发行 API 首项 [v0.78.0-preview.40959817943.1](https://github.com/Mesh-LLM/mesh-llm/releases/tag/v0.78.0-preview.40959817943.1)，2026-10-30 UTC，预发行。以下区分作者文档与有限源码核读，未做上游运行验收。

## 用法

先按发行平台 / backend 下载并核签名或校验值，再运行 `mesh-llm setup`。首次评估可以使用已有本地 GGUF 的单机路径：

```bash
mesh-llm serve --local-model-only --gguf /models/model.gguf
```

README 说明该路径默认 API 在 `127.0.0.1:9337`，绕过 Mesh 网络发现；它不代表所有产品 analytics 自动关闭。`serve --auto` 则会发现公共 mesh，可能下载模型，并启动 API / console；不要把两者当作等价入门命令。本轮未安装、下载模型或加入任何 mesh。

## 原理

节点依据模型、容量和拓扑路由请求，必要时分配模型 stage 与片段；Skippy 提供本地执行，QUIC / Iroh 提供节点间传输与中继。多节点计算需要交换数据，收益取决于网络延迟、带宽、分片与批量；Mixture-of-Agents 的聚合推理属于另一种实验路径。

## 价值

适合研究异构机器上模型装载、节点路由和分布式服务，也能以兼容接口接现有应用。容量扩展、吞吐扩展、首 token 延迟和每 token 成本应分别报告，不能由“总显存更大”推出交互更快。

## 风险边界

- Apache-2.0；模型权重、runtime bundle、插件和分发平台分别核兼容性 / 条款。发行首项是 preview，本页源码快照不是该包运行验收。
- 工作流文档明确：默认 join token 编码节点身份和连接地址，并非访问授权凭证；unpublished / 状态值 private 仅说明未公开发现，不能证明启用了准入。owner allowlist / trust policy 需另外验证。
- QUIC 保护在途数据，中继无法读密文的设计不意味着参与计算的端点可信；二进制发行签名也不是远程运行时证明。
- analytics crate 披露 opt-out 产品统计：编译或运行时存在 PostHog key 才可发送，缺 key 的源码构建不发送；`MESH_LLM_ANALYTICS`、`DO_NOT_TRACK`、配置及 CI 有特定优先级。另一个 telemetry 配置用于运维指标，不能用同名概括数据流。
- Windows README 仍记录特定稳定包校验 / CUDA bundle 安装问题；版本、驱动、内核 flavor 和模型格式要一起固定，不照搬其他平台的安装结果。

## 补充建议

从单机正确性基线到两台受控主机，逐步核拒绝未知 owner、断网 / 失联节点、重复请求与模型一致性。记录 p50 / p95 首 token、decode 速率、网络流量、失败率及功耗；单独检验 analytics 关闭、运维 exporter 和控制接口监听范围。

## 参考资料

- [上游仓库](https://github.com/Mesh-LLM/mesh-llm)、[仓库 API](https://api.github.com/repos/Mesh-LLM/mesh-llm)。
- [README.md](https://github.com/Mesh-LLM/mesh-llm/blob/5e2fdddf6a6ea10d16e3689741483574f1274103/README.md)。
- [LICENSE](https://github.com/Mesh-LLM/mesh-llm/blob/5e2fdddf6a6ea10d16e3689741483574f1274103/LICENSE)。
- [mesh/docs/MESHES.md](https://github.com/Mesh-LLM/mesh-llm/blob/5e2fdddf6a6ea10d16e3689741483574f1274103/mesh/docs/MESHES.md)。
- [mesh/crates/mesh-llm-analytics/README.md](https://github.com/Mesh-LLM/mesh-llm/blob/5e2fdddf6a6ea10d16e3689741483574f1274103/mesh/crates/mesh-llm-analytics/README.md)。
- [mesh/crates/mesh-llm-analytics/src/consent.rs](https://github.com/Mesh-LLM/mesh-llm/blob/5e2fdddf6a6ea10d16e3689741483574f1274103/mesh/crates/mesh-llm-analytics/src/consent.rs)。
