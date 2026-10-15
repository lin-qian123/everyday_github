<!-- markdownlint-disable MD013 -->

# LiveKit Server（livekit/livekit）中文解读

> 上游仓库：<https://github.com/livekit/livekit> · 归类：语音、视频与多模态 · 证据快照：2026-10-16（Asia/Shanghai）。API：21,468 stars / 2,457 forks / 192 open issues；Apache-2.0；Release `v1.13.10`，默认分支 `master`。本页为上游文档与相关源码的静态整理，未安装运行、接入真实数据 / 凭据、复测性能或完成全面安全审计。

## 定位

本页跟踪 `livekit/livekit` 的 Go WebRTC SFU server：在用户、设备和 AI Agent 之间转发实时音视频与数据。STT、LLM、TTS、turn detection 和业务 tools 主要由另一个 LiveKit Agents SDK 组织，server 仓库负责底层连接与房间基础设施。

## 用法

按官方 Release 或 macOS 的 `brew install livekit` 安装 server，开发环境运行 `livekit-server --dev`，再用 `lk` CLI 生成测试房间 token、发布 demo 媒体。开发 key / secret 是公开的 `devkey` / `secret`，只用于本地测试。要接语音 Agent，再按 Agents quickstart 部署独立进程；自托管 server 时可选 model plugins，不能把 Cloud Inference 默认示例视为离线服务。

## 原理

- SFU 按订阅关系选择并转发 track，以 simulcast、带宽适配和 speaker / subscription 等机制控制实时传输。
- 房间内 participant 使用 JWT 表达身份与 join / publish / subscribe 等权限，server SDK 与 webhook 组织控制面。
- UDP、TCP、TURN 等解决不同网络的连接问题；多节点 / 多区域、录制 / 转流、SIP 和 Agents 属于额外部署与服务组合。

## 价值

- 为语音 Agent 提供真实双向媒体通道，便于将传输延迟与模型延迟分开观察。
- 多类 SDK 与 self-host / Cloud 路径可覆盖浏览器、手机、设备和 Agent 的共同房间模型。
- 适合做打断、弱网、重连和人机接管等真实交互测试，而不只测试离线音频。

## 风险边界

- 不得把 `--dev`、公开默认 key / secret 或 sample config 中的示例 key 用于公网；token 应由可信后端按房间与最小能力签发。
- WebRTC 传输加密、应用端 E2EE、服务端录制以及模型参与者能读取的内容属于不同边界；STT / LLM / TTS provider 和 cloud observability 也可能接收音频 / 文本。
- server 许可不自动覆盖模型、电话线路、云托管和录音权利；费用、同意与保留策略要按实际产品配置。
- `v1.13.10` server 与各 SDK / Agents / Egress 版本分开发布；文档的规模和 uptime 数字来自上游声明，本页未做独立容量或 SLA 验证。

## 补充建议

- 用合成音频和测试账号先测 2 人 + 1 Agent 房间的 p95 延迟、barge-in、丢包、断线重连和权限撤销。
- 以最短可用 token TTL、TLS、受限 TURN 与独立 signing backend 配置自托管环境，再做水平扩展。
- 将音频、transcript、recording、provider 日志逐层标注去向和保留，固定 server / SDK / Agent 版本组合。

## 参考资料

- 上游仓库：<https://github.com/livekit/livekit>
- GitHub REST API：<https://api.github.com/repos/livekit/livekit>
- README / Server 与 Agents 分工：<https://github.com/livekit/livekit/blob/master/README.md>
- 配置样例：<https://github.com/livekit/livekit/blob/master/config-sample.yaml>
- LICENSE：<https://github.com/livekit/livekit/blob/master/LICENSE>
- Releases：<https://github.com/livekit/livekit/releases>
- 自托管部署：<https://docs.livekit.io/transport/self-hosting/deployment/>
- 语音 Agent quickstart：<https://docs.livekit.io/agents/start/voice-ai/>
