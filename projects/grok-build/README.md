<!-- markdownlint-disable MD013 -->

# grok-build

## 定位

`xai-org/grok-build` 是 xAI/SpaceXAI 公开的终端 AI coding agent harness 与 TUI。仓库 README 描述它可以理解代码库、编辑文件、执行 shell、搜索网页，并支持交互式 TUI、headless/CI 和 Agent Client Protocol 嵌入编辑器。

## 用法

官方 README 给出预编译安装脚本，也支持从 Rust 源码构建。典型入口是安装 `grok` CLI 后在项目目录内启动 TUI，或按文档配置认证、模型和 headless 运行。

作为 coding agent 使用前，应先在 disposable worktree、临时仓库或 VM/sandbox 中验证权限范围、命令审批、网络访问和回滚流程。

## 原理

项目主体是 Rust 代码，README 说明仓库周期性从 SpaceXAI monorepo 同步，并用 `SOURCE_REV` 记录来源提交。其核心是把终端交互、agent runtime、代码库上下文、命令执行和任务状态管理放进同一个 CLI/TUI。

## 价值

- 大厂/模型厂商直接开源 coding agent harness，说明终端 agent 已成为平台入口。
- 支持交互、headless 和 ACP，覆盖个人开发、脚本化和编辑器集成三类场景。
- Rust 实现和公开源码有利于研究 agent runtime、TUI 事件流和权限模型。
- 对 Codex、Claude Code、Gemini CLI、opencode 等工具形成新的可比较样本。

## 风险边界

- 新仓库热度很高，但真实工程稳定性、权限治理和成本表现仍需长期验证。
- coding agent 可以改文件和运行命令，不能直接在敏感仓库或生产凭据环境里试用。
- README 中的品牌、同步来源和二进制发布链路都需要以官方域名和 release 为准，避免第三方包冒充。
- headless/CI 模式尤其需要审查 secret 暴露、网络访问和失败回滚。

## 补充建议

- 与 Codex、Claude Code、opencode 在同一历史 bugfix 集合上做对照，记录成功率、耗时、token/额度和 diff 质量。
- 优先阅读认证、权限和 headless 文档，再考虑 CI 集成。
- 观察 ACP 是否会成为多编辑器 agent 接入的事实接口。

## 参考资料

- GitHub: <https://github.com/xai-org/grok-build>
- Documentation: <https://docs.x.ai/build/overview>
- CLI page: <https://x.ai/cli>
