<!-- markdownlint-disable MD013 -->

# pstack（pstack-claude）（michael-denyer/pstack-claude）中文解读

> 上游仓库：<https://github.com/michael-denyer/pstack-claude> · 归类：Agent 框架与技能生态 · 证据快照：2026-10-17（Asia/Shanghai）。API：2,674 stars / 239 forks / 6 open issues；Release / package.json `v0.9.90` / `0.9.90`；MIT；保留原 pstack、cursor-team-kit、thermos 的许可与 NOTICE。本页为上游资料与相关代码的静态整理，未安装运行、复测性能或完成全面安全审计。

## 定位

pstack-claude 把 Lauren Tan 面向 Cursor 的 pstack 工作流移植到 Claude Code、Codex、Pi、Copilot 等宿主。核心入口 `poteto-mode` 根据任务选择调试、规划、实现、评审或持续维护流程；它是第三方技能 / 插件栈，不是模型或隔离执行环境。原上游位于 Cursor 的 plugins 仓库，本仓库新增的是独立维护的移植项目。

## 用法

先固定 release，审阅安装范围、hook、模型角色和脚本，再按上游 README 安装所用宿主的 marketplace 插件。首次用明确的小型缺陷调用 `poteto-mode`，检查是否给出复现、修改和回归证据。Claude Code / Codex / Copilot 插件带自动路由 hook，Codex 需在 `/hooks` 中信任；Pi 安装还会加载扩展。仅共享技能目录的安装不自动具备这些 hook / 工具，不能照搬全部体验。

## 原理

- 共享技能树描述任务 playbook，运行时映射把工具名、模型角色和调用方式适配到不同宿主。
- 原则技能、架构讨论、并行候选与多模型评审组合成工作流；模型 / effort 由 setup 和 override sheet 控制。
- `tools/forks.json` 标记与原上游不同的策略分支；PR 监控与编排脚本复用 GitHub CLI，并可能首次引导安装 Bun 依赖。

## 价值

- 把“先理解问题、后实现、再验证”沉淀成可查看的工程约定，适合跨宿主保持工作习惯。
- 运行时映射和已记录的兼容性限制比笼统宣称“所有 Agent 可用”更便于排错。
- 适合用同一真实缺陷比较修复质量、人工介入次数、token 和延迟；本次没有做这种效果对照。

## 风险边界

- README 称项目无自建服务器 / telemetry，但技能要求读取的源码和 session transcript 仍可能进入所选模型 provider；脚本还会使用本机 GitHub 登录权限。
- 多 Agent / 多模型会放大费用、上下文外发和工作区写入，评审人数不证明结论独立或正确。
- 上游明确区分 skill discovery 与真实 delegation / multi-model 验证；Prime Agent、Gemini CLI 等存在未验证范围，Copilot 还记录特定版本的 headless skill 发现问题。
- hook、用户级共享目录和自动依赖下载属于供应链与持久配置变更；文件 / worktree 分离不能代替 OS 权限隔离。

## 补充建议

先关闭自动路由，用一个测试仓库验证单条 bug 流程，再逐项启用 hook、并行和 PR 工具。固定宿主版本及角色模型，比较失败复现和验收结果，保留卸载 / 配置回滚路径；不要把“工作流完成”当成测试已实际执行。

## 参考资料

- 上游仓库：<https://github.com/michael-denyer/pstack-claude>
- GitHub REST API：<https://api.github.com/repos/michael-denyer/pstack-claude>
- 使用与兼容性：<https://github.com/michael-denyer/pstack-claude/blob/main/README.md>
- 运行时 / 依赖边界：<https://github.com/michael-denyer/pstack-claude/blob/main/docs/reference.md>
- 策略分支：<https://github.com/michael-denyer/pstack-claude/blob/main/tools/forks.json>
- 版本 manifest：<https://github.com/michael-denyer/pstack-claude/blob/main/package.json>
- 许可：<https://github.com/michael-denyer/pstack-claude/blob/main/LICENSE>
- 来源与署名：<https://github.com/michael-denyer/pstack-claude/blob/main/NOTICE.md>
- Releases：<https://github.com/michael-denyer/pstack-claude/releases>
