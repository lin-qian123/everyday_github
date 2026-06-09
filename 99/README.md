# 99（Neovim AI Agent）

概览
- 99 是一个面向 Neovim 的 AI Agent 插件，强调“代理行为受控 + 代码上下文强相关”，主张在明确边界内完成任务，而不是让模型自由漫游整个代码库。
- 它依赖 OpenCode 作为后端执行/推理入口，提供更精细的上下文管控、规则注入与日志追踪能力。

为什么值得关注
- 作为 GitHub Trending 上靠前的 AI 工具之一，它代表了“编辑器内 AI Agent + 约束式工作流”的新一代方向。
- 和“无限制自动化”不同，99 的理念是“能力更强，但权限更小”，更适合工程团队在真实仓库里逐步落地。

工作原理（简化版）
- 99 在 Neovim 内部运行，以当前打开的文件/窗口/选择区为主上下文。
- 通过 AGENT.md / SKILL.md 这类规则文件注入团队约束，限制模型行为与可访问范围。
- 借助 OpenCode 进行任务执行（例如函数级别的代码修改、单文件变更、局部重构），在“强约束 + 可追溯”的框架内完成改动。

如何安装与使用（Lazy 示例）
1. 安装 OpenCode（99 依赖 OpenCode 作为后端）。
2. 在 Neovim 插件管理器（Lazy.nvim）中加入 99：

```lua
{
  "ThePrimeagen/99",
  config = function()
    local n = require("99")
    n.setup()
    vim.keymap.set("n", "<leader>9f", function()
      n.cmd("fun")
    end)
    vim.keymap.set("n", "<leader>9v", function()
      n.cmd("vet")
    end)
  end,
}
```

3. 在代码中使用快捷键触发 Agent 指令。
4. 可通过 `:99ls` 查看日志列表，` :99log <log>` 查看详细执行日志。
5. 在 `cmp` 自动补全中通过 `@` 触发技能提示（skills completion）。

推荐使用方式
- 在仓库根目录维护一份 `AGENT.md`，写清楚“允许改哪些文件、禁止做什么、格式化规则”等。
- 让 99 只处理“明确、可验证”的小任务（例如单文件改动、局部重构、测试修复），将大型变更拆成多个可审计步骤。
- 对“宽泛/探索型”需求可直接在 OpenCode 中交互，再将结果落回 99 进行受控修改。

已知限制/注意事项
- 仍处于早期阶段，功能/行为可能快速变化。
- 若缺少明确规则（如 AGENT.md），模型更容易偏离预期，因此建议从规则约束开始。

来源
- https://github.com/trending
- https://github-trending.com/repositories
- https://t.me/s/githubtrending
- https://byteiota.com/posts/2025-02-06-github-trending-repos/
