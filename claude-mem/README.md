# claude-mem

概览
claude-mem 是一款 Claude Code 插件，用于“自动记录、压缩并回放”你在编码会话中的上下文。它会捕捉 Claude 的操作与观察，生成可检索的摘要，并在未来会话中自动注入相关记忆，从而减少重复解释与上下文丢失。

核心能力
- 持久记忆：跨会话保存上下文并自动注入。
- 自动压缩：将会话过程压缩为可检索摘要。
- 搜索工具：提供基于 MCP 的记忆检索工具链。
- 本地可视化：内置本地 Web UI 观察与检索记忆。

原理与架构（基于公开说明的归纳）
claude-mem 通过生命周期钩子捕捉会话事件，将观察与摘要写入本地数据库，并提供检索与“逐层展开”的上下文注入流程，做到 token 成本可控的记忆回放。

快速上手
- 在 Claude Code 中安装插件：
  - `/plugin marketplace add thedotmack/claude-mem`
  - `/plugin install claude-mem`
- 重启 Claude Code，后续会话将自动加载历史记忆。

使用场景
- 多天持续编码项目，减少重复解释。
- 团队协作下的长期上下文维护。

风险与注意事项
- 记忆会持久化本地数据，建议使用隐私标签或配置排除敏感信息。

参考链接
- https://github.com/thedotmack/claude-mem
- https://claude-mem.ai/
