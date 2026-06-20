# palmier-pro（palmier-io/palmier-pro）

- GitHub: https://github.com/palmier-io/palmier-pro
- 记录日期: 2026-06-20 (Asia/Shanghai)

## 定位

`palmier-pro` 是一个面向 macOS 的开源 AI 视频编辑器，核心卖点不是“再做一个视频生成按钮”，而是把时间线编辑器、内置生成式模型能力和 MCP 接口合到同一应用里，让用户与 Claude / Codex / Cursor 之类 agent 一起改视频项目。

## 热度信号

1. GitHub API 在 2026-06-20 抓取时显示约 `1.9k stars`、`188 forks`，并进入 GitHub Trending 日榜。
2. 官方 README 的定位非常直白：`The video editor built for AI.`，并明确写出 `You and your agent can generate and edit videos together inside the timeline.`。
3. 项目 README 还直接给出 Claude Code、Codex、Cursor、Claude Desktop 的 MCP 接入方式，说明它不是只做 UI，而是在认真做 agent 协作入口。

## 用法

### 1) 直接下载 macOS 应用

README 提供最新 DMG 下载入口，并注明当前要求：

- `macOS 26 (Tahoe)`
- `Apple Silicon`

### 2) 用内置 MCP server 接给 agent

应用打开后会暴露本地 MCP server：

```text
http://127.0.0.1:19789/mcp
```

Codex 的接入命令是：

```bash
codex mcp add palmier-pro --url http://127.0.0.1:19789/mcp
```

Claude Code 的接入命令是：

```bash
claude mcp add --transport http palmier-pro http://127.0.0.1:19789/mcp
```

### 3) 在时间线里直接生成或编辑内容

按照 README 的描述，编辑器内可调用视频和图像生成模型，也可以让外部 agent 通过 MCP 与时间线工程协同工作。

## 原理

1. 项目主体是 Swift 原生视频编辑器，目标体验对标 Premiere Pro，但把 AI 功能嵌入编辑流程而不是外挂在外部网页。
2. 应用在本地打开时同时提供 MCP 接口，使外部 agent 能以结构化方式访问当前时间线与编辑上下文。
3. README 把能力划分得很清楚：编辑器本体、MCP server、agent chat 是开源的，而生成式 AI 处理部分是闭源的。
4. 这意味着它本质上是一种“本地创作工作站 + agent 协作层 + 订阅式生成服务”的混合产品结构。

## 价值

- 它代表了一个很具体的新方向：AI 工具不再停留在网页生成 demo，而是开始反向进入专业创作软件工作流。
- 对经常做短视频、产品演示、教程视频或营销素材的团队来说，这种“时间线 + agent”协作模式很有现实吸引力。
- MCP 接口的存在也让它比很多封闭式创作 SaaS 更值得持续观察。

## 风险边界

- 当前只支持 `macOS 26 (Tahoe)` 与 Apple Silicon，适用面很窄。
- README 明确说明生成式 AI 处理部分闭源，所以它不是一个完全开源的端到端视频生成系统。
- 创作类工具通常还会涉及素材版权、模型商用许可、输出合规和订阅成本，不能只看编辑器表层功能。

## 补充建议

1. 若你关心的是“本地视频编辑器 + agent”这一形态，可以先只评估开源编辑器和 MCP 协作能力，不急着绑定其订阅式生成能力。
2. 对团队落地而言，重点看时间线对象是否足够可编程、MCP 暴露的操作粒度是否够细，以及导出链路是否稳定。
3. 如果你已经在跟 `OpenMontage`、`LTX-2` 这类项目，`palmier-pro` 很适合作为“生成之后如何进入人工精修与协同编辑”这一步的补充观察点。

## 参考资料

- https://github.com/palmier-io/palmier-pro
- https://github.com/trending
- https://www.instagram.com/palmier.io
- https://x.com/Palmier_io
