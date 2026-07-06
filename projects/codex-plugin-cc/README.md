<!-- markdownlint-disable MD013 -->

# codex-plugin-cc

## 定位

`codex-plugin-cc` 是 OpenAI 为 Claude Code 用户提供的插件，用来在 Claude Code 内直接调用 Codex 做代码审查、对抗式审查、任务委派、会话转移和后台任务管理。

它代表了一个很重要的趋势：coding agent 不再只是彼此竞争的独立入口，而开始通过插件、slash command 和后台任务机制互相调用。对开发者来说，这意味着可以在一个主工作流里引入另一个 agent 的判断和执行能力。

## 用法

项目 README 给出的安装路径是：

```bash
/plugin marketplace add openai/codex-plugin-cc
/plugin install codex@openai-codex
/reload-plugins
/codex:setup
```

常用命令包括：

- `/codex:review`：对当前改动或分支做只读 Codex 代码审查。
- `/codex:adversarial-review`：做更可定向的对抗式审查，适合挑战架构取舍、边界条件和隐藏假设。
- `/codex:rescue`：把 bug 调查、修复尝试或接续任务交给 Codex。
- `/codex:transfer`：把当前 Claude Code 会话转成可由 Codex 继续的持久线程。
- `/codex:status`、`/codex:result`、`/codex:cancel`：管理后台 Codex 任务。

## 原理

插件把 Claude Code 的插件系统、slash command、subagent 机制与本机 Codex CLI 连接起来。它并不把 Claude 和 Codex 混成一个模型，而是在当前仓库上下文中启动 Codex 任务，并提供状态查询、结果读取和会话转移。

关键设计点包括：

- 审查命令默认只读，降低误改风险。
- 后台执行适合多文件审查和长任务。
- rescue / transfer 把“换一个 agent 继续看”变成显式工作流。
- 支持 ChatGPT 订阅或 OpenAI API key，但会消耗 Codex 使用额度。

## 价值

- **跨 agent 复核**：让 Claude Code 用户在同一工作流里引入 Codex 审查。
- **降低切换成本**：不需要手动复制上下文到另一个终端或应用。
- **任务分流**：主 agent 可以继续推进，Codex 在后台做审查或救援。
- **工作流样本**：展示了 coding agent 之间通过插件市场和会话导入形成互操作层的方向。

## 风险边界

- 插件依赖 Claude Code 插件系统、Codex CLI、Node.js 和登录状态，环境问题会直接影响可用性。
- 后台任务会消耗 Codex 额度，长审查或多次 rescue 需要关注成本。
- 跨 agent 转移上下文时要注意仓库路径、会话来源和敏感信息。
- Codex 的审查结果仍然需要人工判断，不能把“第二个 agent 也同意”当成充分验证。

## 补充建议

- 在重要 PR 合并前，可把 `/codex:review --background` 作为第二视角审查。
- 对安全、数据迁移、权限、并发类改动，优先用 `/codex:adversarial-review` 明确要求挑战方案。
- 和 `herdr`、`gastown`、`agterm` 这类多 agent 管理层结合看，可以观察“多 agent 并行工作台”的工具链正在成形。

## 参考资料

- GitHub 仓库：<https://github.com/openai/codex-plugin-cc>
- Codex 定价说明：<https://developers.openai.com/codex/pricing>
- GitHub Trending：<https://github.com/trending>
