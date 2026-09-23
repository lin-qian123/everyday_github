<!-- markdownlint-disable MD013 -->

# Atomic-Chat（AtomicBot-ai/Atomic-Chat）

- GitHub：<https://github.com/AtomicBot-ai/Atomic-Chat>
- 抓取快照：2026-09-24，1,607 stars、190 forks、57 open issues
- 热度信号：GitHub TypeScript Trending 抓取时约 +30 当日 stars
- 版本与许可：API 为 `NOASSERTION`，根 `LICENSE` 为 Apache-2.0；latest Release `v2.0.44`，tags 已到 `v2.0.47`，根 package 仍为 `0.0.0`

## 定位

Atomic Chat 是跨桌面 / 移动端的本地 AI chat 与 inference engine，统一运行 GGUF / MLX 等 open-weight 模型，并在 `127.0.0.1:1337/v1` 暴露 OpenAI-compatible API。它既是 Tauri 聊天应用，也可作为 Codex、OpenCode、Goose 等 Agent / IDE 工具的本地模型后端。

## 用法

桌面端可下载 macOS、Windows、Linux 构建，iOS / Android 使用对应商店版本；在应用里下载并加载模型后，OpenAI SDK 只需把 `base_url` 改为本地端点。源码开发要求 Node.js、Yarn、Rust / Tauri；Apple Silicon 还可能需要 Metal toolchain。若使用 cloud provider 或 MCP，需要另行配置 key 和工具权限。

## 原理

前端与 Tauri host 组合多个 inference backend：Atomic 的 llama.cpp / TurboQuant fork、上游 llama.cpp，以及 Apple Silicon 的 MLX-VLM；上层用同一个 OpenAI-compatible API 屏蔽 backend 切换。MTP、DFlash、Flash Attention 和 KV-cache 量化作为可选加速路径，聊天、assistant、artifact、MCP 与 Agent integrations 复用该本地服务。

## 价值

它把模型下载、设备端推理、聊天 UI 和 Agent-compatible endpoint 集中到一个应用，适合隐私敏感试验、离线开发和本地模型对比。统一端点也减少不同 Agent 工具对 llama.cpp / MLX 的重复适配成本。

## 风险边界

- “local”只适用于本地模型 / loopback 路径；cloud provider、模型下载、MCP、外部工具和把 host 改为 `0.0.0.0` 都会改变数据与攻击面。
- 本地 API 默认无真实 key；暴露到 LAN 前必须加网络隔离、认证代理和访问日志，不能把 loopback 默认安全性外推到局域网。
- 30%--70%、3×、6× 和约 4.3× 等加速 / 内存数字均依赖模型、硬件、量化与 prompt，本轮未独立复现。
- 模型权重、llama.cpp / MLX 组件与应用源码可能适用不同许可证；根 Apache-2.0 不能替代逐模型审查。
- Release `v2.0.44`、tag `v2.0.47` 与根 package `0.0.0` 不一致，自动更新和客户端兼容需要固定构建核验。

## 补充建议

先在 loopback 上用低风险模型和固定 prompt 建立延迟、吞吐、峰值内存、工具调用、context overflow 与输出质量基线；显式关闭 cloud provider / 不需要的 MCP。若提供给其他主机，放在带认证、TLS、allowlist 和 rate limit 的反向代理后，并记录应用、backend、模型 hash 与量化格式。

## 参考资料

- [GitHub 仓库](https://github.com/AtomicBot-ai/Atomic-Chat)
- [GitHub REST API](https://api.github.com/repos/AtomicBot-ai/Atomic-Chat)
- [v2.0.44 Release](https://github.com/AtomicBot-ai/Atomic-Chat/releases/tag/v2.0.44)
- [本地 API 与 inference engines](https://github.com/AtomicBot-ai/Atomic-Chat#-use-it-as-an-api)
- [源码构建说明](https://github.com/AtomicBot-ai/Atomic-Chat#%EF%B8%8F-build-from-source)
- [LICENSE](https://github.com/AtomicBot-ai/Atomic-Chat/blob/main/LICENSE)
