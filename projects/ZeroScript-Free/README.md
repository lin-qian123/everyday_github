<!-- markdownlint-disable MD013 -->

# ZeroScript Free（sebattfg/ZeroScript-Free）

> 上游仓库：<https://github.com/sebattfg/ZeroScript-Free> · 归类：Coding Agents 与终端助手 · 本页基于 2026-10-06 的 GitHub API、README、浏览器扩展 manifest、Bridge 源码、Release 与 LICENSE 静态整理，未安装扩展、登录聊天站点、连接 Roblox Studio 或执行 Luau。

- 抓取快照：307 stars、43 forks、66 open issues。
- 热度信号：GitHub JavaScript Trending 抓取时约 +6 当日 stars。
- 版本与许可：GPL-3.0；GitHub Release / tag 与扩展 manifest 均为 `v1.5.5` / `1.5.5`。

## 定位

ZeroScript Free 用浏览器扩展和本机 Bridge，把 ChatGPT、DeepSeek、Gemini、Kimi、GLM、Qwen、Arena 或 Meta AI 的网页聊天变成 Roblox Studio Agent。模型可读取 / 修改脚本、检查实例树、执行 Luau、控制 play-test，并通过 Studio 内置 MCP 生成或插入资产。

## 用法

用户从 Release 下载 zip，以开发者模式加载 `zeroscript-extension`，在 Roblox Studio 中启用 MCP server，再运行 Windows / macOS Bridge。随后在受支持的网页聊天中点击 `Start session`，由扩展解析模型输出并通过 `127.0.0.1` Bridge 转发给 Studio。上游固定 YouTube 教程可用于核对安装步骤。

## 原理

Manifest V3 扩展向八类聊天域注入 provider-specific content script，并获得这些域及本机 HTTP / WebSocket 的 host 权限。扩展把网页模型回复解析成工具命令，Python Bridge 连接 Roblox Studio MCP server、回传工具结果和截图，最终继续驱动同一聊天回合。

## 价值

它复用网页端模型订阅而不要求单独 API key，并把 Studio 原生 MCP 接到多种聊天前端，降低 Roblox 初学者试用 Agent 编程的门槛。Bridge / extension / Studio 三层结构与 GPL 源码也便于检查具体权限路径。

## 风险边界

- Agent 能改脚本、执行 Luau、插入资产和控制测试，等同于对当前 Place 的高权限开发者；必须使用版本控制和可丢弃副本，不能把聊天确认当作沙箱。
- 扩展运行在真实登录的模型网页并读取 / 写入聊天 DOM；网页改版会造成解析漂移，prompt injection 或错误工具块可能被转成真实 Studio 动作。
- “无需 API key”不等于本地或私密：项目代码、截图、工具结果和提示仍进入所选网页模型及其账号日志。
- 开发者模式加载未签名扩展、双击脚本与本机 Bridge 都扩大供应链面；Release 制品需要校验来源，Bridge 端口不可暴露到非本机网络。
- Creator Store 资产、生成素材和 Roblox 项目内容有各自许可与平台规则；自动插入不代表可商用或无恶意脚本。
- 本轮未测试八个 provider 的 DOM 兼容性、Studio MCP 鉴权、长会话工具正确率、截图配额或 `v1.5.5` Release 制品。

## 补充建议

在新的 Roblox 测试 Place 和专用浏览器 profile 中固定 `v1.5.5`，先禁用发布、付费资产和外部 HTTP；每轮动作前后保存 Place / Git diff，并把删除、批量改脚本、资产插入和 play-test 外联设为人工确认。若 Bridge 可配置监听地址，强制 loopback 并用主机防火墙阻止局域网访问。

## 参考资料

- [GitHub 仓库](https://github.com/sebattfg/ZeroScript-Free)
- [GitHub REST API](https://api.github.com/repos/sebattfg/ZeroScript-Free)
- [README 与安装路径](https://github.com/sebattfg/ZeroScript-Free/blob/master/README.md)
- [扩展 manifest 与权限](https://github.com/sebattfg/ZeroScript-Free/blob/master/zeroscript-extension/manifest.json)
- [本机 Bridge 源码](https://github.com/sebattfg/ZeroScript-Free/blob/master/bridge.py)
- [`v1.5.5` Release](https://github.com/sebattfg/ZeroScript-Free/releases/tag/v1.5.5)
- [上游固定安装视频](https://www.youtube.com/watch?v=kPKiZLZ9_Ps)
- [GPL-3.0 LICENSE](https://github.com/sebattfg/ZeroScript-Free/blob/master/LICENSE)
