<!-- markdownlint-disable MD013 -->

# Biscotti

> 更新：2026-10-22（Asia/Shanghai）。分类：办公、商业与行业应用。主上游 `scosman/Biscotti`；默认分支快照 `273e3ff10cab`。官方资料与源码静态研究；热度、发行及社媒口径见[当日日报](../../daily/2026-10-22/ai-hotspots.md)。

## 定位

面向 Apple Silicon Mac 的会议录音与转写应用，捕获麦克风和系统音频，在本机做转写、说话人识别和摘要，不需会议机器人加入。README 的准确率与“私有”是作者描述，本轮只核文档及部分 MCP 实现。[README.md](https://github.com/scosman/Biscotti/blob/273e3ff10cab1b14314685da697bc5ac53eb19d1/README.md)

## 用法

要求 Apple Silicon M1 或更新、macOS `>=15`，建议 16 GB 内存；官方提供 Release DMG 与 Homebrew 安装入口，首次需下载模型并配置麦克风 / 系统音频等权限。日历用于提醒和身份匹配，应按需要启用。[README.md](https://github.com/scosman/Biscotti/blob/273e3ff10cab1b14314685da697bc5ac53eb19d1/README.md)

当前发行列表首项 `v1.1.0` 是 prerelease，`v1.0.0` 是正式版；main 上的 MCP 文档不能自动当作旧正式安装包已有的功能。若启用 MCP，文档入口为设置中的 MCP，地址 `http://127.0.0.1:8516/mcp`，默认关闭。[App/ConnectingMCP.md](https://github.com/scosman/Biscotti/blob/273e3ff10cab1b14314685da697bc5ac53eb19d1/App/ConnectingMCP.md)

## 原理

文档列出 Whisper V3 Turbo / WhisperKit 转写、Pyannote / SpeakerKit 说话人处理，以及本地 Gemma 4 / llama.cpp 摘要。身份匹配结合历史 voiceprint、已标记说话人、对话线索和日历信息；声纹近似匹配不等于可靠身份认证。[README.md](https://github.com/scosman/Biscotti/blob/273e3ff10cab1b14314685da697bc5ac53eb19d1/README.md)

MCP 服务经本机 HTTP 暴露会议搜索、摘要 / 笔记 / 转写；源码常量固定 loopback 与端口，并设请求体和连接上限。[App/ConnectingMCP.md](https://github.com/scosman/Biscotti/blob/273e3ff10cab1b14314685da697bc5ac53eb19d1/App/ConnectingMCP.md) [Packages/BiscottiKit/Sources/MCPServer/MCPServerConfiguration.swift](https://github.com/scosman/Biscotti/blob/273e3ff10cab1b14314685da697bc5ac53eb19d1/Packages/BiscottiKit/Sources/MCPServer/MCPServerConfiguration.swift)

## 价值

工程判断：适合想保留原音频、可编辑笔记和转写的个人工作流；可在预取模型后评估断网运行。使用价值取决于中文 / 混合语种、多人重叠和摘要事实的实际质量，而不是“本地”标签本身。

## 风险边界

- 文档明确：MCP 打开时本机任何应用可读取会议，其他 Agent 可能继续把材料发往云端。loopback 限制网络监听范围，不形成应用身份授权；关闭 MCP 和检查客户端数据出口是两件事。[App/ConnectingMCP.md](https://github.com/scosman/Biscotti/blob/273e3ff10cab1b14314685da697bc5ac53eb19d1/App/ConnectingMCP.md)
- 服务实现的 1 MiB 请求体、16 连接和超时限制针对资源占用，不等于会议访问控制。这里没有进行攻击或完整网络审计。[Packages/BiscottiKit/Sources/MCPServer/MCPServerConfiguration.swift](https://github.com/scosman/Biscotti/blob/273e3ff10cab1b14314685da697bc5ac53eb19d1/Packages/BiscottiKit/Sources/MCPServer/MCPServerConfiguration.swift) [Packages/BiscottiKit/Sources/MCPServer/HTTPListener.swift](https://github.com/scosman/Biscotti/blob/273e3ff10cab1b14314685da697bc5ac53eb19d1/Packages/BiscottiKit/Sources/MCPServer/HTTPListener.swift)
- 录音、转写、声纹和日历可形成集中敏感资料；应在参与者知情、获授权的场景使用，并验证导出、删除、备份与摘要误差。本轮不作特定司法辖区的合规结论。[README.md](https://github.com/scosman/Biscotti/blob/273e3ff10cab1b14314685da697bc5ac53eb19d1/README.md)
- 根许可 PolyForm Perimeter 1.0.1 含 Noncompete 条款，限制向他人提供竞争产品，不应按 MIT / Apache 自由复用推断；模型和依赖另有条款。[LICENSE.md](https://github.com/scosman/Biscotti/blob/273e3ff10cab1b14314685da697bc5ac53eb19d1/LICENSE.md)

## 补充建议

先录一段获同意的合成会议，留人工转写与角色真值，分别量化漏词、说话人混淆和摘要虚构；预取后断网测完整流程，再检查 MCP 启停与不同客户端读取范围。固定应用版本及模型，避免把 main 审计结论套到 v1.0.0。本轮未录音或安装应用。

## 参考资料

- [README.md](https://github.com/scosman/Biscotti/blob/273e3ff10cab1b14314685da697bc5ac53eb19d1/README.md)
- [LICENSE.md](https://github.com/scosman/Biscotti/blob/273e3ff10cab1b14314685da697bc5ac53eb19d1/LICENSE.md)
- [SECURITY.md](https://github.com/scosman/Biscotti/blob/273e3ff10cab1b14314685da697bc5ac53eb19d1/SECURITY.md)
- [App/ConnectingMCP.md](https://github.com/scosman/Biscotti/blob/273e3ff10cab1b14314685da697bc5ac53eb19d1/App/ConnectingMCP.md)
- [Packages/BiscottiKit/Sources/MCPServer/MCPServerConfiguration.swift](https://github.com/scosman/Biscotti/blob/273e3ff10cab1b14314685da697bc5ac53eb19d1/Packages/BiscottiKit/Sources/MCPServer/MCPServerConfiguration.swift)
- [Packages/BiscottiKit/Sources/MCPServer/HTTPListener.swift](https://github.com/scosman/Biscotti/blob/273e3ff10cab1b14314685da697bc5ac53eb19d1/Packages/BiscottiKit/Sources/MCPServer/HTTPListener.swift)
- [仓库 API](https://api.github.com/repos/scosman/Biscotti)
- [v1.1.0 Release（预发行）](https://github.com/scosman/Biscotti/releases/tag/v1.1.0)
