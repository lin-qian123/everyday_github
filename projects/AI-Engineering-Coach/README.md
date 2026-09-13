<!-- markdownlint-disable MD013 -->

# AI Engineer Coach（microsoft/AI-Engineering-Coach）中文解读

> 证据快照：2026-09-14（Asia/Shanghai）。GitHub REST API 显示 4,021 stars、552 forks、40 open issues，API 许可证为 MIT，未发布 GitHub Release；根 `package.json` 版本为 `0.1.0`。README 徽章写 VS Code 1.115+，但当前 `package.json` 要求 `^1.125.0`，实际安装应以构建时 manifest 为准。本文未构建 VSIX、读取本地会话日志或运行其评分规则。

## 定位

AI Engineer Coach 是一个本地读取 AI coding assistant 会话日志的 VS Code 扩展与 GitHub Copilot App canvas。它把多个 harness 的使用记录整理成时间线、输出量、活动模式、反模式、context health 和学习建议，目标是让“怎样与 coding agent 协作”从主观感受变成可审查的本地仪表盘。

它是实践分析与 coaching 工具，不是代码质量证明、员工绩效系统或精确费用账单。仓库也明确声明它是 Microsoft 员工维护的开源社区项目，不属于正式 Microsoft 产品或支持服务。

## 用法

当前没有 marketplace 包或 GitHub Release，需要自行构建 VSIX：

```bash
git clone https://github.com/microsoft/AI-Engineering-Coach.git
cd AI-Engineering-Coach
npm ci
npm run package
code --install-extension ai-engineer-coach-*.vsix
```

安装后运行 `AI Engineer Coach: Open Dashboard`。也可在 GitHub Copilot App 项目中执行 `npm install && npm run build`，再打开仓库注册的 canvas；两种模式的可用功能并不完全相同。

## 原理

- 解析本地 VS Code、Xcode、Claude、Codex、OpenCode 与 GitHub Copilot 等会话记录，再归一化为统一活动、workspace、model 和 harness 视图。
- 用 45 条可编辑 Markdown 规则识别 prompt quality、session hygiene、code review、tool mastery 与 context management 反模式。
- 以 webview/canvas 呈现趋势、时间线、代码输出量、活动热图、context map 和导出摘要。
- Skill Finder 从重复 prompt 中寻找可复用 skill；部分 context review、quiz 与规则编译功能会显式调用 VS Code 内置语言模型 API。
- GitHub App 页面会把本地 session 与 issue/PR 线索做近似关联；上游将 issue credit 定义为相对估算，而非计费数字。

## 价值

- 将长会话、并发 session 和 workspace 切换可视化，便于发现上下文碎片化和重复劳动。
- 规则可查看、编辑和现场测试，比单一黑箱“生产力分数”更容易追溯。
- 跨多个 harness 观察同一人的工作方式，可减少只看单个 provider 用量造成的偏差。
- 本地、只读分析适合先在个人环境试验，再判断哪些指标值得进入团队流程。

## 风险边界

- 本地 session 日志可能含源码、prompt、文件路径、身份和密钥片段；“不上传 telemetry”不等于日志本身没有敏感性，导出与截图也可能泄露信息。
- 可编辑规则和 practice score 是启发式代理指标，不能直接推导代码正确性、工程产出、个人能力或绩效。
- 可选 AI 功能会通过 VS Code 内置模型接口处理选定内容；具体 provider、保留和网络路径应按当前宿主配置独立核验。
- README 与 `package.json` 的 VS Code 最低版本不一致，且无 Release/marketplace 包；构建依赖、commit 与扩展权限必须固定后再试用。
- “AI 生成代码量”依赖日志和归因口径，不能自动识别代码是否被人工重写、是否有用或是否最终进入生产。

## 补充建议

1. 先在脱敏测试 profile 和副本 workspace 中构建，记录 commit、Node/npm、VS Code 版本与 VSIX 哈希。
2. 抽样回读 session→图表→规则命中的证据链，分别统计误报、漏报和跨 harness 字段缺失。
3. 默认关闭可选 AI review，只在确认 provider 数据流后用非敏感日志测试。
4. 团队使用时只共享聚合趋势，不把 score 作为个人考核；对导出文件设置保留、访问和删除策略。

## 参考资料

- GitHub：<https://github.com/microsoft/AI-Engineering-Coach>
- GitHub REST API：<https://api.github.com/repos/microsoft/AI-Engineering-Coach>
- README：<https://github.com/microsoft/AI-Engineering-Coach/blob/main/README.md>
- `package.json`：<https://github.com/microsoft/AI-Engineering-Coach/blob/main/package.json>
- 隐私与功能说明：<https://github.com/microsoft/AI-Engineering-Coach#privacy>
- LICENSE：<https://github.com/microsoft/AI-Engineering-Coach/blob/main/LICENSE>
