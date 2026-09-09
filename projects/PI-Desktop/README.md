<!-- markdownlint-disable MD013 -->

# PI-Desktop（vastsa/PI-Desktop）中文解读

> 证据快照：2026-09-10（Asia/Shanghai）。GitHub REST API 显示 1,634 stars、153 forks、45 open issues，LGPL-3.0；最新稳定 release 为 `v0.14.5`，而 main 根 package 为 `0.14.6-rc.4`。README 明确标注 Early Preview。本文未安装或运行项目。

## 定位

PI-Desktop 是一个 local-first、跨平台的 AI coding-agent 桌面工作区，以 Electron 前端、Rust host core 与 pi Agent Harness 组合项目、会话、diff、预览、模型、skills、MCP、subagents 和插件。

它的目标不是替代某个特定编辑器，而是给长时程 coding agent 一个独立控制面，并通过 Agent、Plan、Goal 三种模式设置不同的人机闸门。

## 用法

最直接的入口是从 GitHub Releases 下载 macOS、Windows 或 Linux 构建：

1. 在 Settings 中配置 OpenAI、Anthropic、本地模型、gateway 或兼容 API 的凭据。
2. 打开一个本地项目目录。
3. 选择 Agent、Plan 或 Goal 模式。
4. 在 Review panel 中检查文件 diff、命令输出和预览，再决定是否接受结果。

准备评估时应固定 `v0.14.5`，不要把 main 上的 `0.14.6-rc.4` 当作已发布稳定版本。

## 原理

- React renderer 展示聊天、项目、review、设置与工作面板，并关闭 Node integration。
- Electron main 负责桌面生命周期和各组件编排。
- Rust host core 持有文件系统、SQLite、secrets、权限和其他高权限 workspace 操作。
- pi Agent sidecar 运行模型交互、streaming 与 agent loop；模型既可以在本地，也可以经云端 provider。
- 插件可增加 tools、commands、panels、skills、MCP、subagents、themes 与 resident services。

## 价值

- 把多仓库、多 session、review 和长任务从散落的终端窗口收拢到一个可观察界面。
- BYOK 与多 provider 让模型选择和执行工作区解耦。
- UI、host core 与 agent sidecar 的职责分离，为权限、secret 与 renderer 攻击面提供了比单体 Electron 应用更清晰的审计位置。
- Plan / Goal gate 有助于把“批准路径”与“批准结果”区别开来。

## 风险边界

- README 明确说明项目仍是 Early Preview；API、插件接口和桌面行为可能变化。
- 权限层、进程分离和 diff review 不等于 OS sandbox；agent 仍可能以用户授权执行高影响命令或读取敏感文件。
- 插件进程虽受 permission gate 且与 renderer 分离，仍是用户信任代码；插件 marketplace 不能视为逐项安全背书。
- local-first 不等于离线：云端模型 / gateway 会产生代码、prompt 和元数据外发，取决于 provider 配置。
- diff 可见不等于行为正确；生成文件、数据库变更、网络副作用和终端命令需要独立日志与回读。

## 补充建议

1. 先在 disposable clone 或独立测试目录使用固定 release，记录默认配置、数据目录、网络连接和卸载残留。
2. 初次仅接入一个低权限模型 endpoint；对 shell、Git、外部网络和 MCP 写操作保留逐次批准。
3. 安装插件前审阅 package 来源、权限、resident service、更新机制和数据出口，并验证禁用 / 卸载是否完全。
4. 用失败命令、恶意仓库提示、symlink、超大 diff 和 provider 断连测试权限层与恢复路径。

## 参考资料

- GitHub：<https://github.com/vastsa/PI-Desktop>
- GitHub REST API：<https://api.github.com/repos/vastsa/PI-Desktop>
- Releases：<https://github.com/vastsa/PI-Desktop/releases>
- 文档：<https://pi-docs.aiuo.net/>
- 架构说明：<https://github.com/vastsa/PI-Desktop/blob/main/docs/spec/02-architecture/01-architecture.md>
- LICENSE：<https://github.com/vastsa/PI-Desktop/blob/main/LICENSE>
