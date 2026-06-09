# impeccable（pbakaus/impeccable）项目速览与上手指南

- GitHub: https://github.com/pbakaus/impeccable
- 更新日期: 2026-03-25（Asia/Shanghai）

## 1. 为什么今天值得跟踪

`impeccable` 是一个面向 AI 编程助手的“前端设计语言 + 指令体系”项目。它把“如何让模型产出更好 UI”从零散 prompt，做成可安装、可复用、可治理的技能包。

- 热度信号（仓库页可见）：`13.2k stars`、`542 forks`（抓取时间：2026-03-25）
- 结构信号：同时提供 `.codex/.claude/.cursor/.gemini/.opencode/.pi` 等多生态目录，说明其定位是“跨 agent 通用设计能力层”。

## 2. 项目在做什么（核心定位）

从 README 可提炼出三个核心层：

1. `frontend-design` 扩展技能
- 覆盖 `typography`、`color-and-contrast`、`spatial-design`、`motion-design`、`interaction-design`、`responsive-design`、`ux-writing` 七个专项参考。

2. 20 个可执行设计命令
- 如 `/audit`、`/critique`、`/normalize`、`/polish`、`/distill`、`/harden`、`/animate`。
- 作用是把“设计评审/修复/打磨”流程标准化，而非每次手写长 prompt。

3. 反模式（Anti-patterns）白名单化约束
- 明确告诉模型“不要做什么”（如过度模板化字体、卡片套卡片、灰字压彩底等），减少 AI 生成“同质化 UI”。

## 3. 怎么用（可直接执行）

### 安装方式 A：官网下载（README 推荐）

1. 打开 `https://impeccable.style`
2. 下载对应工具的 ZIP
3. 解压到你的项目

### 安装方式 B：从仓库复制

Claude Code：

```bash
# 项目级
cp -r dist/claude-code/.claude your-project/

# 全局级
cp -r dist/claude-code/.claude/* ~/.claude/
```

Codex CLI：

```bash
cp -r dist/codex/.codex/* ~/.codex/
```

Cursor：

```bash
cp -r dist/cursor/.cursor your-project/
```

Gemini CLI：

```bash
cp -r dist/gemini/.gemini your-project/
```

## 4. 原理是什么（工程视角）

它的本质是“把设计能力做成可版本化中间层”：

1. 规范化输入
- 通过固定命令与技能上下文，减少模型每次重新理解任务的随机性。

2. 显式约束输出
- 反模式库相当于“负向规则集”，在生成阶段提前压制常见劣化设计。

3. 可组合工作流
- 例如 `/audit -> /normalize -> /polish`，从诊断到修复到收尾形成闭环。

4. 跨工具迁移
- 同一套设计策略能映射到不同 AI harness，降低团队切换成本。

## 5. 适用场景

- 需要批量产出落地网页/前端组件，并保持视觉质量一致。
- 团队内多人使用不同 AI 编程工具，但希望共享统一设计标准。
- 希望把“设计评审经验”沉淀成可审计资产，而非口头经验。

## 6. 风险与注意事项

- 语义对齐风险：同一命令在不同 agent 中仍可能有行为差异，建议做小样本验收。
- 质量上限风险：技能能显著提升平均质量，但不能替代高质量设计判断。
- 维护风险：当设计系统升级时，技能与反模式规则需同步维护。

## 7. 信息来源

- 仓库主页与 README（星标、安装、命令、反模式）：https://github.com/pbakaus/impeccable
- 官方站点（分发入口）：https://impeccable.style
