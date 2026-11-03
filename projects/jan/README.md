<!-- markdownlint-disable MD013 -->

# Jan：本地模型桌面工作台与可选云模型 / Agent 能力

- 上游：[janhq/jan](https://github.com/janhq/jan)；分类：模型、训练与推理基础设施。
- 更新：2026-11-04（Asia/Shanghai）；固定 main SHA：`c1a64a78515e1726999fa10e3c43de7a5a2ba3d0`。
- 热度：Rust daily +70；API 45,397 stars / 3,141 forks / 572 open issues（含 PR）。最新 v0.8.8，UTC 2026-10-28。
- 根 LICENSE 声明 Apache-2.0 并请求适当署名；API 为 NOASSERTION，不能据此判定没有许可证。
- 证据范围：榜单、API、发行与固定文档 / 源码；未安装、下载权重、启动 API、执行工具或测试漏洞修复。

## 定位

用 Tauri 桌面界面组织本地 LLM、对话与助手，提供 OpenAI 兼容 API 和 MCP / Agent 能力，也支持连接多家云模型服务。README 的离线定位适用于选择本地模型的路径，不能覆盖下载、远程 provider、工具联网和可选统计的全部行为。

## 用法

从上游 Releases 选择与系统、架构和加速后端相符的版本，记录安装包版本与校验值；不要把 latest 下载地址当作固定版本。先下载合适模型，在关闭云 provider、联网工具和可选统计的条件下验证本地聊天。

需要给其他应用使用时，在 Settings → Local API Server 启动服务。文档默认 `127.0.0.1:1337`、`/v1`；配置自己的 API key 和目标模型后再接客户端。非本机监听必须设置 key，Trusted Hosts 和服务端工具执行开关分别配置。

从源码开发另需 Node >=20、Yarn >=4.5.3、Make 与 Rust；`make dev` 会安装依赖并构建 / 启动，不是纯只读检查。模型、GPU 和系统支持应以选定发行包实际结果为准。

## 原理

- 桌面前端通过 Tauri 调用本地组件，llama.cpp 等运行路径负责权重加载、推理与硬件加速。
- 远程 provider 是另一条数据路径，本地 API 可为兼容客户端代理请求；MCP 为模型提供工具访问。
- v0.8.8 发行说明加入浏览器 Origin / Trusted Hosts 检查、链接外部打开、文件路径边界及所有 API 端点的服务端工具 opt-in。
- 桌面产品分析、Agent OTLP 与 MCP routing callback 是不同机制；routing 文档说明发行版未注册该 callback。

## 价值

适合把本地模型和兼容 API 作为日常试验入口，同时保留云模型选择。工程价值在于统一模型、会话和客户端接入；本机性能、模型质量与工具任务成功率仍取决于硬件、权重和配置。

## 风险边界

- 首次安装、引擎 / 模型下载、更新、远程模型及 Web / MCP 工具可能联网；“本地”不自动证明整个工作流断网。
- 默认本机监听可不设 key；扩大监听范围需 key。Trusted Hosts 的网页来源检查不是脚本客户端认证，非浏览器请求的处理应与 API key 分开理解。
- 聊天工具与 Local API 的服务端工具开关不同；v0.8.7 说明支持时聊天 Shell 默认开启，v0.8.8 说明 API 工具保持 opt-in，不能把两者混为一个开关。
- 桌面产品分析状态初值 false，界面有明确同意 / 拒绝；Agent OTLP 默认关闭，但文档另列匿名更新检查。此处为静态配置与文档证据，未做全链路抓包。
- v0.8.8 是作者建议更新的安全发行；本页记录其修复声明，没有复现旧漏洞或验证所有保护。主线文档、发行二进制、模型与第三方组件许可分别核对。

## 补充建议

1. 固定发行包、引擎、模型哈希、后端和上下文，用自己的任务记录内存、延迟、质量与断网行为。
2. 先保持 loopback、设置 key、关闭不需要的工具；逐项开启云服务或 MCP 并记录数据流。
3. 升级后检查 Trusted Hosts、API 工具开关、聊天 Shell、统计选择与历史数据；不要以旧设置推断新行为。

## 参考资料

- [README](https://github.com/janhq/jan/blob/c1a64a78515e1726999fa10e3c43de7a5a2ba3d0/README.md)、[LICENSE](https://github.com/janhq/jan/blob/c1a64a78515e1726999fa10e3c43de7a5a2ba3d0/LICENSE)、[API](https://api.github.com/repos/janhq/jan)。
- [本地 API 文档](https://github.com/janhq/jan/blob/c1a64a78515e1726999fa10e3c43de7a5a2ba3d0/docs/src/pages/docs/desktop/api-server.mdx)、[服务端配置](https://github.com/janhq/jan/blob/c1a64a78515e1726999fa10e3c43de7a5a2ba3d0/src-tauri/src/core/server/commands.rs)。
- [桌面分析状态](https://github.com/janhq/jan/blob/c1a64a78515e1726999fa10e3c43de7a5a2ba3d0/web-app/src/hooks/useAnalytic.ts)、[同意界面](https://github.com/janhq/jan/blob/c1a64a78515e1726999fa10e3c43de7a5a2ba3d0/web-app/src/containers/analytics/AnalyticConsent.tsx)。
- [Agent OTLP](https://github.com/janhq/jan/blob/c1a64a78515e1726999fa10e3c43de7a5a2ba3d0/docs/src/pages/docs/agent/telemetry.mdx)、[MCP routing callback](https://github.com/janhq/jan/blob/c1a64a78515e1726999fa10e3c43de7a5a2ba3d0/docs/src/pages/docs/desktop/mcp-routing-telemetry.mdx)。
- [v0.8.8](https://github.com/janhq/jan/releases/tag/v0.8.8)、[v0.8.7 工具开关](https://github.com/janhq/jan/releases/tag/v0.8.7)。
