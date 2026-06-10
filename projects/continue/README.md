# continue

## 项目定位
`continue` 是一个开源 AI 编码工具项目，当前主线已经从早期的 IDE 助手，收敛到“把 AI 检查项做成仓库内可版本控制规则，并在 PR / CI 中执行”的工程化路线。

- GitHub：https://github.com/continuedev/continue
- 文档：https://docs.continue.dev/
- 记录日期：2026-06-10（Asia/Shanghai）

## 为什么值得关注

- OSSInsight AI Top 50（2026-06-10 抓取）中，`continuedev/continue` 仍在榜单内。
- GitHub 仓库页显示约 `33.6k stars`、`4.6k forks`。
- 当前 README 明确写出：该仓库“no longer actively maintained”，但同时把最终方向定义成 `Source-controlled AI checks, enforceable in CI`。

这说明它今天的价值，不在于“又一个聊天式补全工具”，而在于把 AI 审查逻辑写回代码仓库本身。

## 用法

官方文档当前给出的最短路径是：

1. 在 `continue.dev/check` 上对 PR 运行检查。
2. 在仓库内把检查项写成 `.continue/checks/` 下的 Markdown 文件。
3. 让每个检查作为 GitHub status check 出现在 PR 上，通过 / 失败并给出建议修复。

如果按产品形态看，它仍保留三种入口：

- CLI
- VS Code 扩展
- JetBrains 插件

但文档首页已经把重点放到“Write Your First Check / Run Checks in CI”，这比传统 IDE 对话更接近团队治理工具。

## 原理

`continue` 当前最值得借鉴的是三件事：

1. 把 AI 规则写成仓库文件  
   不把审查逻辑藏在某个人的提示词里，而是提交为可 review、可 diff、可演进的 Markdown 检查。

2. 把 AI 反馈接入 CI  
   AI 不只是在本地聊天窗口给建议，而是像 lint、test 一样进入 PR 状态流。

3. 把“建议”变成“可执行组织约束”  
   例如安全、风格、数据边界、文档完整性等要求，可以按仓库粒度长期积累。

它本质上是在把 AI 从个人副驾，转成团队可治理的质量层。

## 价值

- 对多人协作仓库，比单纯 IDE 补全更容易沉淀团队规则。
- 适合把安全、架构、接口、文档约束做成稳定检查模板。
- AI 检查写进 repo 后，更方便审计“规则是什么、何时修改、谁在维护”。

## 风险边界

- 当前官方 README 已明确说明该仓库为只读、非活跃维护状态，这意味着选型要非常谨慎。
- AI 检查容易产生误报或“形式正确但业务理解不够”的问题，不能替代人工评审。
- 如果检查项写得过泛，最终会退化成噪音，团队会快速绕过它。

## 补充建议

- 更适合把 `continue` 当作“规则文件 + CI 接口”思路来借鉴，而不是盲目押注其长期官方路线。
- 如果你已经在用 GitHub Actions、Danger、review bots，可以优先实验一两个高价值检查，例如 secrets、接口变更说明、迁移脚本风险。
- 采用时一定要把“误报处理”和“规则维护责任人”一起设计进去。

## 参考资料

- https://github.com/continuedev/continue
- https://docs.continue.dev/
- https://ossinsight.io/trending/ai
