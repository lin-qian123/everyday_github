<!-- markdownlint-disable MD013 -->

# fable5-mode

## 定位

`cozytab/fable5-mode` 是一个面向 Claude Code 的 skill 与 guard hooks 组合，目标是把“先规划、再执行、再验证”的工作纪律机械化地注入模型工作流。它的核心叙事是：输出质量不只来自模型能力，也来自可执行的工作流程纪律。

## 用法

README 给出的基础安装方式是把仓库克隆到 Claude skills 目录：

```bash
git clone https://github.com/cozytab/fable5-mode \
  "${CLAUDE_CONFIG_DIR:-$HOME/.claude}/skills/fable-mode"

bash "${CLAUDE_CONFIG_DIR:-$HOME/.claude}/skills/fable-mode/install.sh"
```

使用时在 Claude Code 中请求 “use fable mode” 或 “用 fable 模式”。如果在项目中创建 `.fable/LEDGER.md`，可以打开更强的任务卡和验收约束。

## 原理

项目把工作流拆成六个杠杆：Plan Gate、小任务卡执行、对抗式自检、真实产品验证、上下文卫生和 checkpoint autonomy。hook 层用于把部分规则从提示词建议变成硬约束，例如没有计划不允许展开、没有验收命令不允许宣称完成。

## 价值

- 把 coding agent 常见的“边写边想、未验证即完成”问题显式约束起来。
- 对长任务、重构、迁移和高风险改动更有价值。
- 可作为 Claude Code skill 生态中“流程纪律层”的代表案例。
- 对 Codex / Cursor / Copilot 等其他 agent 也有方法论借鉴意义。

## 风险边界

- 它不能提升模型本身的推理上限，只能降低流程失误。
- 小任务会因为计划、验收和 hook 检查增加时间成本。
- hook 如果设计过强，可能误阻断合理探索或快速修复。
- README 中使用的 Fable 5 / Opus 4.8 叙事需要结合实际可用模型与平台状态复核。

## 补充建议

- 适合放在团队规范或高风险仓库中试点，而不是所有日常小修都启用。
- 将验收命令写成可机器执行的测试、lint、构建或端到端检查。
- 对失败两次后的升级路径做团队约定，避免 agent 在局部循环中消耗预算。

## 参考资料

- GitHub: <https://github.com/cozytab/fable5-mode>
- Claude Code: <https://claude.com/claude-code>
