<!-- markdownlint-disable MD013 -->

# OpenSandbox：统一 Agent 沙箱 API，区分运行时与发行验证

- 上游：[`opensandbox-group/OpenSandbox`](https://github.com/opensandbox-group/OpenSandbox)；仓库 ID：`1118085970`。
- 核读：2026-11-12（Asia/Shanghai）；主线固定于 [`f72baeae3a7f`](https://github.com/opensandbox-group/OpenSandbox/tree/f72baeae3a7feb11a49cc42f48dba3e93a94600d)。
- 热度快照：17,201 stars / 1,630 forks / 210 open issues（含 PR）；来自 [GitHub API](https://api.github.com/repos/opensandbox-group/OpenSandbox)，不代表采用量或质量。

## 定位

在自有基础设施中运行 Agent 代码、命令、文件操作、浏览器和桌面环境的开源平台，以生命周期 / 执行 API 连接 Docker、Kubernetes 和 Fast Sandbox，提供多语言 SDK、CLI、MCP。

原页 2026-03-05 跟踪 `alibaba/OpenSandbox`；该 API 当前返回迁移目标 `/repositories/1118085970`，与新组织仓库 ID 一致，故在原目录刷新，不另建项目。当前 README 标明为 AAIF 项目，代码 Apache-2.0。今天官方 Python daily +88；榜单语言分组并不等同 API 当前主语言（Go）。

## 用法

先按**已发布版本**选 server / SDK / 镜像组合。[PyPI `opensandbox-server`](https://pypi.org/pypi/opensandbox-server/json) 当前为 1.2.0；稳定平台发行 `release-1.2.0` 于 UTC 10-27 发布。最新 `release-1.2.1-rc.2`（UTC 11-11）是候选版，发行说明明确只发布镜像，SDK/CLI 包留待 1.2.1 稳定发布；不要直接把主线新能力套给 1.2.0 安装。

本地需 Docker 和 Python >=3.10。上游工作流先生成 Docker TOML，再启动 server、用 SDK 创建实例，执行命令 / 文件操作，最后在 `finally` 销毁实例；当前文档清理方法为 `destroy()`，不沿用旧页过时示例。CLI `osb` 与 MCP 分别安装，都是有实际创建和执行权限的入口。

主线示例 TOML 监听 `127.0.0.1:8080`，API key 留空注释。空 key 会无认证，需 TTY 确认，非交互需 `OPENSANDBOX_INSECURE_SERVER=YES` 显式承认；实际接入应设置 key。生成配置后核对版本、监听、沙箱端口发布地址和 egress，不要以控制面 loopback 推断所有入口仅本机可达。

## 原理

生命周期层创建、查询、暂停 / 恢复、销毁沙箱，执行层提供 commands / files 等接口；具体隔离强度取决于容器 / 微虚机、挂载、权限和宿主。Fast Sandbox 的预热容量与快照恢复降低创建等待，不能等同冷启动或任意负载性能。

网络分 ingress 和逐沙箱 egress。Credential Vault 由 egress sidecar 保管真实凭据，工作负载使用假值或空值；对获准 HTTPS 请求进行绑定匹配和认证头注入。主线要求 `dns+nft`、网络策略和 Credential Proxy，建议 `defaultAction=deny`；不是启用 SDK 就自动具备的保护。

## 价值

把 Agent 执行环境和应用逻辑解耦，适合每任务独立空间、受控代码执行、浏览器任务和评测训练。统一 API 便于替换后端，但各后端的版本、能力、恢复和网络策略仍须逐项验证。

作者 10-08 双节点 ACK warm 测量中，初始串行 create 100/100 成功、p50 64 ms；并发 20 则为 51/100 成功。时延只统计成功样本，且预热、缓存、客户端和存储条件已说明；不可把“64 ms”外推为生产吞吐、冷启动或全负载 SLA。

## 风险边界

- **发行签名有明确缺口**：SECURITY 有概括性签名说明，但更具体的当前 release-verification 文档指出 umbrella / package workflow 缺 Cosign / provenance 步骤，并跟踪 issue #2463。digest 对应只证明内容身份，不能代替构建者来源证明。
- `release-1.2.1-rc.1` 的 API `prerelease=false`，但名称和说明明确仍是 RC；不能仅按布尔标志认定稳定。rc.2 的资源超配、修复和功能属于候选版，不是本轮部署验收。
- 控制面 key、工作负载身份、execd、公开沙箱端口、ingress 和 egress 是不同边界；单一 server key 不自动建立业务多租户授权。
- Vault 仍需审 request scheme / host / port / method / path、代理 CA、宿主及 sidecar 权限；保密凭据不等于请求行为获授权。动态 exchange 主线文档和发行说明对 SDK 覆盖存在粒度差异，接入前逐语言核版本。
- 容器共享内核、宿主 bind、镜像、恢复制品和集群权限均影响隔离。网络控制必须在所选后端实际验，不能只看 API 接受策略或健康检查成功。

## 补充建议

固定 server、SDK、组件镜像 digest、配置和部署后端，先验证禁止访问、端口曝光、超时销毁、失败恢复和凭据不落盘，再测 warm / cold、成功率和尾延迟。若组织要求签名来源，当前缺失应作为未满足条件保留，或使用经独立核验的构建流程。

本轮为迁移身份、文件、发行与性能文档静态核读；未安装 server、拉镜像、启动沙箱、注入凭据、跑 ACK / KVM、验签或执行隔离测试。

## 参考资料

- [README 与统一入口](https://github.com/opensandbox-group/OpenSandbox/blob/f72baeae3a7feb11a49cc42f48dba3e93a94600d/README.md)。
- [主线 server 配置与认证](https://github.com/opensandbox-group/OpenSandbox/blob/f72baeae3a7feb11a49cc42f48dba3e93a94600d/docs/getting-started/configuration.md)。
- [Docker 示例 TOML](https://github.com/opensandbox-group/OpenSandbox/blob/f72baeae3a7feb11a49cc42f48dba3e93a94600d/server/opensandbox_server/examples/example.config.toml)。
- [当前发行验证缺口](https://github.com/opensandbox-group/OpenSandbox/blob/f72baeae3a7feb11a49cc42f48dba3e93a94600d/docs/community/release-verification.md)。
- [Vault 前提和匹配规则](https://github.com/opensandbox-group/OpenSandbox/blob/f72baeae3a7feb11a49cc42f48dba3e93a94600d/docs/guides/credential-vault.md)。
- [性能环境、成功率和样本定义](https://github.com/opensandbox-group/OpenSandbox/blob/f72baeae3a7feb11a49cc42f48dba3e93a94600d/docs/architecture/fast-sandbox/performance.md)。
- [安全报告与支持范围](https://github.com/opensandbox-group/OpenSandbox/blob/f72baeae3a7feb11a49cc42f48dba3e93a94600d/SECURITY.md)。
