<!-- markdownlint-disable MD013 -->

# Archify

> 上游仓库：[tt-a1i/archify](https://github.com/tt-a1i/archify) · 归类：Agent 框架与技能生态 · 本页基于 2026-08-27 的上游 README、项目页与 GitHub API 快照整理。

## 定位

Archify 是面向 Raven、Cursor、Claude Code、Codex CLI 和 OpenCode 的 agent skill：把代码库或系统描述转换成可交互、可分享的技术系统图。它覆盖 architecture、workflow、sequence、data flow 和 lifecycle 五类图形，产出自包含 HTML，并支持 PNG、SVG、WebM 与分享卡片导出。API 快照为 17,804 stars、1,232 forks、30 个开放 issue，MIT；GitHub Trending 抓取时显示约 +1,002 当日 stars。该数字是观察时点的公开关注度，不代表图形正确性、运行时架构真实性或生产成熟度。

## 用法

上游提供 `skills` CLI 安装路径，也可先临时使用，不把 skill 永久写入环境：

```sh
npx skills add tt-a1i/archify -g

# 或不安装到全局，直接让 Codex 使用
npx skills use tt-a1i/archify@archify --agent codex
```

安装后可以先要求 agent 分析仓库，再生成一个边界明确的高层图：

```text
Analyze this repository, then use archify to create a high-level runtime architecture diagram.
Show 8–12 core components, one primary path, external dependencies, and trust boundaries.
Put supporting detail in cards instead of adding more edges.
```

需要脚本化验收时，直接使用上游 Node CLI：

```sh
node archify/bin/archify.mjs validate workflow examples/agent-tool-call.workflow.json --quality showcase --json
node archify/bin/archify.mjs deliver workflow examples/agent-tool-call.workflow.json /tmp/workflow.html --quality showcase --json
```

## 原理

- agent 先依据图形类型把描述写成带 schema 的 typed JSON IR；schema、示例和品牌资料共同约束字段形状与节点语义。
- validator 对 schema、布局、HTML/SVG、路径和标签间距执行检查；只有通过检查的候选才交付，失败时返回结构化诊断与受支持的修复控制。
- viewer 将 JSON IR 渲染为单文件 HTML，交互层只使用已写入的节点和关系，支持搜索、上下游追踪、精确路径、语义角色比较和有限故事播放。
- 可选的 source-evidence 模式会把节点绑定到特定 Git commit 的文件和行号；普通图不会自动声称来自真实运行时或基础设施。

## 价值

- 将“请画一张架构图”的自然语言请求变成可审阅、可导出、可在聊天中迭代的交付物。
- 单文件 HTML 便于放入 README、PR、工单或演示文稿；深色/浅色主题和多种导出格式降低传播成本。
- typed IR、验证收据和 last-good 预览为架构变更审查提供了比纯截图更好的追踪入口。
- 对 agent 工具调用、数据流和部署关系，有限视图与路径追踪有助于把注意力放在主路径和边界上。

## 风险边界

- LLM 生成的图仍可能漏掉组件、误读代码或把意图写成事实；图通过布局/结构校验，不等于通过运行时、性能、安全或部署验证。
- “source evidence”只证明节点关联到指定版本的文件与行号，不证明该代码在当前环境被执行，也不证明所有拓扑都完整。
- Mermaid 输入主要通过提示转换，而不是完整的原生 Mermaid 解析器；复杂语法、隐含关系和动态配置可能被丢失或重写。
- skill 会读取仓库和可能的品牌/来源资料；使用真实代码前应限制工作区、网络、凭据和可写目录，避免把内部架构上传给 provider。
- 页面中的 finite motion、演示故事和视觉美化是表达层能力，不应被当作系统稳定性、流量影响或变更安全结论。

## 补充建议

1. 先在公开或合成仓库中，用固定 commit 生成 architecture 与 data-flow 两种图，并逐节点回到源码核验。
2. 对生产变更保留“来源版本、生成提示、JSON IR、validator 输出和人工审阅结论”，不要只保存最终 HTML 截图。
3. 将信任边界、外部依赖、认证路径、失败/回滚路径作为显式节点或关系；缺失时标为未知，而不是让 agent 补全。
4. 交付前单独做无障碍、导出清晰度、敏感信息脱漏和图例语义审查；架构图不能替代威胁建模或部署清单。

## 参考资料

- [上游 README / 安装、图形类型与验证流程](https://github.com/tt-a1i/archify)
- [Archify 项目页与 Proof Lab](https://tt-a1i.github.io/archify/)
- [Archify Skill 说明](https://github.com/tt-a1i/archify/blob/main/archify/SKILL.md)
- [GitHub API 元数据](https://api.github.com/repos/tt-a1i/archify)
- [GitHub Trending](https://github.com/trending)
