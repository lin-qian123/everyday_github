<!-- markdownlint-disable MD013 -->

# locally-uncensored：整合本地模型、媒体创作与 Agent 的桌面工作台

- 上游：[`PurpleDoubleD/locally-uncensored`](https://github.com/PurpleDoubleD/locally-uncensored)；仓库 ID：`1191052193`。
- 核读：2026-11-14（Asia/Shanghai）07 时段；主线固定于 [`3dff4291f8ad`](https://github.com/PurpleDoubleD/locally-uncensored/tree/3dff4291f8ad5a86078679e23c7a0a2cd2adf9b3)。
- 热度快照：官方 TypeScript daily +154；[API](https://api.github.com/repos/PurpleDoubleD/locally-uncensored) 为 4,187 stars / 666 forks / 24 open issues（含 PR），不代表实际用户或质量。

## 定位

LU 是一个把聊天、文档检索、图像 / 视频、Code、Agent、语音和可选远程访问放在同一桌面窗口的应用。本地路径连接 LU Engine、Ollama、LM Studio、ComfyUI 等；也可选用第三方 provider 或 LU Cloud。它是模型与工具的集成层，“本地”取决于实际选择的功能和后端。

当前稳定 [v3.0.10](https://github.com/PurpleDoubleD/locally-uncensored/releases/tag/v3.0.10) 于 UTC 11-05 发布，重点修复 3.0.8 / 3.0.9 丢失聊天后覆盖唯一完整备份的问题。本轮首次建档，不把旧版修复称作今日首发。

## 用法

从固定发行页选平台包。README 列 Windows 10 / 11、Linux、macOS 14+ Apple Silicon Beta 和 Android arm64；Intel Mac 不支持，iPhone 页面状态为商店审核中。macOS 上自动更新、Remote Access 和电脑控制的验证范围有限，不因有 DMG 就视作全功能验收。

首次向导检查已有推理引擎，按选择安装组件和模型；图像 / 视频另需相应 ComfyUI 或 Mac 后端与资源。先选一个硬件容纳的模型验证聊天，再开启工具或媒体功能。模型文件大小不能替代上下文、运行内存和显存估算。

源码开发的 `package.json` 要求 Node >=22；上游提供 `npm install`、`npm run dev` 和 `npm run tauri build`。这些会安装依赖、构建或启动应用，本轮未执行。已有 3.0.8 / 3.0.9 数据先复制保存，再按 3.0.10 的“Settings → Chat Backup → Restore chats from backup”流程检查可恢复内容；修复不能重建已无副本的数据。

## 原理

TypeScript 前端与 Tauri / Rust 宿主连接本机推理、媒体、文件和命令工具。聊天的长历史可压缩并保留历史视图；3.0.9 的可选 Recall 默认关闭，仅普通聊天可用，不涵盖 Agent / Code。媒体工作流由后端执行，工作台不自行保证每个模型 / 工作流兼容。

工具按类别、会话与单工具设置权限。桌面新安装的 shell、文件写入、MCP、图像、视频与 workflow 默认为 Ask First，Web / System 为 Auto；工作目录内文件读取不逐次询问。单工具 override 优先于普通类别设置；外部 MCP 已独立分类，不能只关闭 Terminal 就认定 MCP 无命令能力。

所谓 Sandbox 是 `~/agent-workspace` 下的工作目录和文件工具路径约束。源码的 shell 执行会设置工作目录后启动本机命令，仍拥有当前用户的系统能力；没有容器、虚拟机或网络过滤。这是产品明确披露的限制，不是本轮发现已被利用的漏洞。

## 价值

适合希望用统一界面管理本机引擎、模型、创作和受控工具调用的人，减少在多个后端之间复制配置的成本。其工程价值也在于公开版本修复、平台已测范围、工具权限及恢复入口，便于搭建自己的验收清单。

“Uncensored / No Filter”描述输出限制口径，不证明正确性、工具可靠性或模型适配。作者的竞品比较和少量提示测试属于上游陈述，不能当独立横评或一般效果结论。

## 风险边界

- **执行范围**：获批 shell 和外部 MCP 可访问本机与网络；Code 的 Bypass 会减少确认。停止当前回合也不保证已启动后台子任务同时结束，需看 Agents 面板。不要把模型输出或网页指令当成额外授权。
- **数据出口**：本地推理之外，模型 / 组件下载、更新、Web 搜索、页面抓取、BYOK provider、Cloud 和远程访问各自联网。隐私页还列 Cloud 切换计数与模型目录请求；不能用“无 analytics kit”推断零网络事件。密钥在可用时进系统 keychain，存在本地存储回退。
- **备份与平台**：3.0.10 补救聊天备份覆盖，仍需独立副本和恢复演练。3.0.9 的长视频条件主要来自单张 RTX 3060，部分量化选择只开始下载未完整运行；其他测试和平台不能据此推广。
- **发行与许可**：应用为 AGPL-3.0-only，模型和插件另核许可。上游称 Windows 首装器尚无生产 Authenticode 签名，而更新通道有独立 minisign 验证；macOS README 声称签名 / notarization，源码配置仍可见 ad-hoc 默认，发行流水线可覆盖，须核实际包。本轮未验二进制签名、哈希、流水线或独立安全性；SECURITY 明言尚无独立安全审计，不能直接采信“杀毒误报”等自述作安全结论。

## 补充建议

先用无敏感内容的可恢复项目检查文件读写、shell、MCP 与 provider 出口，分别确认全局、会话和单工具 override。需要运行不可信代码时，另提供真正隔离的环境。

固定应用、模型 revision、后端与工作流，分别验收聊天质量、检索来源、媒体完整视听、任务停止、备份恢复和远程撤权。共享日志前检查内容；部署前按模型与插件逐一核对可用条件，不把应用许可证延伸到全部权重。

## 参考资料

- [固定主线 README](https://github.com/PurpleDoubleD/locally-uncensored/blob/3dff4291f8ad5a86078679e23c7a0a2cd2adf9b3/README.md)、[package 元数据](https://github.com/PurpleDoubleD/locally-uncensored/blob/3dff4291f8ad5a86078679e23c7a0a2cd2adf9b3/package.json)、[3.0.9 的 Known limits](https://github.com/PurpleDoubleD/locally-uncensored/releases/tag/v3.0.9)。
- [Sandbox 说明（正文标注针对 3.0.6）](https://github.com/PurpleDoubleD/locally-uncensored/blob/3dff4291f8ad5a86078679e23c7a0a2cd2adf9b3/docs/guide/agent-sandbox/index.html)、[shell 实现](https://github.com/PurpleDoubleD/locally-uncensored/blob/3dff4291f8ad5a86078679e23c7a0a2cd2adf9b3/src-tauri/src/commands/shell.rs)。
- [桌面默认权限](https://github.com/PurpleDoubleD/locally-uncensored/blob/3dff4291f8ad5a86078679e23c7a0a2cd2adf9b3/src/api/mcp/types.ts)、[override / 迁移规则](https://github.com/PurpleDoubleD/locally-uncensored/blob/3dff4291f8ad5a86078679e23c7a0a2cd2adf9b3/src/stores/permissionStore.ts)、[权限界面](https://github.com/PurpleDoubleD/locally-uncensored/blob/3dff4291f8ad5a86078679e23c7a0a2cd2adf9b3/src/components/settings/PermissionSettings.tsx)。
- [隐私说明（10-27）](https://github.com/PurpleDoubleD/locally-uncensored/blob/3dff4291f8ad5a86078679e23c7a0a2cd2adf9b3/docs/privacy/index.html)、[安全与签名现状](https://github.com/PurpleDoubleD/locally-uncensored/blob/3dff4291f8ad5a86078679e23c7a0a2cd2adf9b3/SECURITY.md)、[Tauri 配置](https://github.com/PurpleDoubleD/locally-uncensored/blob/3dff4291f8ad5a86078679e23c7a0a2cd2adf9b3/src-tauri/tauri.conf.json)。
