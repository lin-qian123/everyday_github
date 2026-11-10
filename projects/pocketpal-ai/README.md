<!-- markdownlint-disable MD013 -->

# PocketPal AI

> 更新：2026-11-11（Asia/Shanghai）。分类：前端、UI 与 Agent 交互层。上游 `a-ghorbani/pocketpal-ai`，仓库 ID `847231566`；源码 `b0f3c83082eeb4b372372f4168ffdeca515b649c`。静态核读，未安装手机应用、下载模型、采音或测试推理 / 网络。

## 定位

PocketPal 是 iOS / Android 端本地模型客户端，整合 GGUF 聊天、语音输入 / 输出、角色 Pals、模型下载与工具调用。离线推理是核心用途，也有用户可选的网页搜索、远端服务器、社区和排行榜功能。[README](https://github.com/a-ghorbani/pocketpal-ai/blob/b0f3c83082eeb4b372372f4168ffdeca515b649c/README.md)

TypeScript daily 为 +50 stars；API 为 9,183 stars / 1,066 forks / 126 open issues（含 PR）。[v1.23.0](https://github.com/a-ghorbani/pocketpal-ai/releases/tag/v1.23.0) 于 UTC 11-10 发布，新增本地 OpenAI-compatible API POC，并修复导入聊天、路径校验和部分 Adreno GPU 问题；清单也是 1.23.0。[API](https://api.github.com/repos/a-ghorbani/pocketpal-ai)

## 用法

从上游链接的应用商店安装，在 Models 下载适合设备内存的 GGUF 或导入本地文件，加载后聊天；语音模型按需另下。先用小模型核输出与内存，之后再启用联网工具或远端模型。源码开发使用 Node ≥22.21.0、Yarn Classic 1.22.22，并按平台准备 Xcode / CocoaPods 或 Android 环境。[构建说明](https://github.com/a-ghorbani/pocketpal-ai/blob/b0f3c83082eeb4b372372f4168ffdeca515b649c/README.md) / [清单](https://github.com/a-ghorbani/pocketpal-ai/blob/b0f3c83082eeb4b372372f4168ffdeca515b649c/package.json)

新增本地 API 初始关闭、端口 8080、LAN 初始关闭；只服务当前本地模型，可选 API key。设置页和 store 都检查 Plus 解锁，README 另称源码构建包含全部 Plus 功能；因此商店版中不应仅凭“免费聊天”推断 API 功能可用。[API store](https://github.com/a-ghorbani/pocketpal-ai/blob/b0f3c83082eeb4b372372f4168ffdeca515b649c/src/store/LocalApiServerStore.ts) / [设置入口](https://github.com/a-ghorbani/pocketpal-ai/blob/b0f3c83082eeb4b372372f4168ffdeca515b649c/src/screens/SettingsScreen/LocalApiServerCard.tsx)

## 原理

React Native UI 通过原生桥接调用 llama.cpp / llama.rn；语音输入用 whisper.cpp，输出按引擎使用 ONNX 或原生运行时。AgentRunner 检出模型工具调用后执行 Talents，再把结果回传。CPU、Metal、OpenCL、Hexagon 等后端有设备与模型条件，不能从一个后端可用推断全部功能受同一加速。[技术栈](https://github.com/a-ghorbani/pocketpal-ai/blob/b0f3c83082eeb4b372372f4168ffdeca515b649c/README.md)

本地 API 是 TCP HTTP listener，提供 `GET /v1/models` 和 `POST /v1/chat/completions`，有连接 / 请求数限制。存在 key 时验证 Bearer；无 key 时拒绝带 Origin 的请求，但原生客户端不必带 Origin。API 兼容范围限于实际实现，不能当成完整云服务替代。[连接实现](https://github.com/a-ghorbani/pocketpal-ai/blob/b0f3c83082eeb4b372372f4168ffdeca515b649c/src/services/localApiServer/connection.ts)

## 价值

适合离线聊天、轻量语音交互及比较同一模型在不同手机上的资源使用。模型、量化、上下文和工具配置可控，便于做可复现实验；本地 API 还能探索手机作为推理端的流程，但目前 POC 身份和系统前后台行为都应纳入验证。

## 风险边界

- **聊天离线与应用零联网不同**：模型 / 音色下载、PalsHub、购买、启动时 CDN 兼容性规则、主动反馈和 opt-in 排行榜仍有网络；网页工具、远端模型或在线系统音色可让内容离机。README 对隐私的声明尚未经本轮抓包验证。[隐私范围](https://github.com/a-ghorbani/pocketpal-ai/blob/b0f3c83082eeb4b372372f4168ffdeca515b649c/README.md)
- **LAN 与认证独立**：LAN 开启时绑定 `0.0.0.0`，代码未强制要求先设置 key；默认 URL 为 HTTP。无 key 的 Origin 拒绝机制不能鉴别任意本地或局域网原生客户端。先配置 key 并核网络范围，再开放 LAN。[监听状态](https://github.com/a-ghorbani/pocketpal-ai/blob/b0f3c83082eeb4b372372f4168ffdeca515b649c/src/store/LocalApiServerStore.ts) / [鉴权](https://github.com/a-ghorbani/pocketpal-ai/blob/b0f3c83082eeb4b372372f4168ffdeca515b649c/src/services/localApiServer/connection.ts)
- **版本修复不等于验收完成**：发行记录包含导入路径校验和 GPU 崩溃修复，本轮未复现旧问题或验证补丁。导入的模型、Pals、聊天和工具返回均需审查来源。[发行记录](https://github.com/a-ghorbani/pocketpal-ai/releases/tag/v1.23.0)
- **资源和质量依赖具体配置**：模型大小、量化、上下文、温度、散热和后台限制影响速度与稳定性。tokens/s、离线可运行与任务正确率分别评估；代码 MIT 不覆盖模型、音色或社区内容的许可。[代码许可](https://github.com/a-ghorbani/pocketpal-ai/blob/b0f3c83082eeb4b372372f4168ffdeca515b649c/LICENSE)

## 补充建议

保留手机型号 / 系统、模型 SHA、量化、上下文、后端和温度；分别测首 token 延迟、持续速度、峰值内存、耗电与正确率。下载完成后在断网状态核本地聊天 / 语音，再逐项开启联网功能。API 单独测试关闭、后台切换、无模型、错误 key、并发和 LAN 范围；不要把聊天成功视为 API 或隐私验收。

## 参考资料

1. [固定 SHA 项目与隐私说明](https://github.com/a-ghorbani/pocketpal-ai/blob/b0f3c83082eeb4b372372f4168ffdeca515b649c/README.md)
2. [本地 API 状态与配置](https://github.com/a-ghorbani/pocketpal-ai/blob/b0f3c83082eeb4b372372f4168ffdeca515b649c/src/store/LocalApiServerStore.ts)
3. [HTTP 路由与鉴权](https://github.com/a-ghorbani/pocketpal-ai/blob/b0f3c83082eeb4b372372f4168ffdeca515b649c/src/services/localApiServer/connection.ts)
4. [v1.23.0](https://github.com/a-ghorbani/pocketpal-ai/releases/tag/v1.23.0) / [TypeScript Trending](https://github.com/trending/typescript?since=daily)
