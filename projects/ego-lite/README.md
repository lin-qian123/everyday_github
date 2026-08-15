<!-- markdownlint-disable MD013 -->

# ego-lite

## 定位

[`citrolabs/ego-lite`](https://github.com/citrolabs/ego-lite) 是面向外部 coding agent 的 macOS 浏览器与 `ego-browser` skill。它把 agent 任务放到独立的 browser Space，并宣称可迁移 Chrome 数据，让用户继续使用原标签页。它属于“带真实登录态的浏览器自动化”路线，而不是通用浏览器库；适合在得到明确授权时探索并行网页任务，但天然涉及 cookie、账号权限和真实业务操作。

## 用法

上游提供 macOS 安装包，也可只安装 skill：

```bash
npx skills add citrolabs/ego-lite
```

安装应用后，向已支持的 agent 调用 `ego-browser`，例如：

```text
ego-browser 在测试站点中搜索一条指定记录；不要提交、发送或删除任何内容。
```

首次启动时的 Chrome 数据迁移会决定 agent 是否可访问既有登录态。应只导入专用测试 profile，而非主力浏览器 profile；Windows/Linux 仍在其上游路线图中。

## 原理

- `ego-browser` 向 agent 暴露 snapshot、fill、click、wait、navigate、capture 等页面内 JavaScript 工具；agent 组织脚本并一次运行，而非频繁 CLI 往返。
- 每个 agent 任务在独立 Space 中执行，目的是避免抢占人类的标签页；Space 隔离不等同于账号、站点权限或数据隔离。
- 上游称 Chrome 数据留在本机、只记录迁移同意状态，并声称其 benchmark 在四个任务上优于 `agent-browser`。这些是作者声明，须以版本固定、可复现实验和网络流量检查验证。

## 价值

- 解决传统自动化常见的“额外浏览器、重新登录、人机抢标签页”摩擦，适合授权的重复网页收集与测试工作流。
- 兼容 Claude Code、Codex、Cursor 或自定义 agent 的定位，降低为每种 agent 重写浏览器适配层的成本。
- GitHub API 于 2026-08-16 的快照为约 10.9k stars、557 forks、MIT；GitHub Trending 当时显示约 +546 stars/day。数字只能证明观察时的公开关注度，不能推断安全性或基准结论。

## 风险边界

- 迁移 Chrome profile 可能暴露会话 cookie、已登录身份、书签、扩展数据和站点权限；“本地存储”也不等于没有外发风险，agent 的提示、动作和页面数据仍须核查。
- agent 可在真实网站代表用户进行高影响动作。转账、下单、发布、招聘、医疗、删除、隐私设置等操作必须禁用或改为人工最终确认。
- 站点条款、反自动化机制、robots 约束及组织政策仍适用；不得用它绕过验证码、访问控制或数据使用限制。
- README 中的速度、token 和成功率比较来自项目方，未见本仓库独立复现；浏览器、模型、网络、登录状态不同会显著改变结果。

## 补充建议

1. 用单独 macOS 用户、专用浏览器 profile、测试账号和最小权限 token 试运行，避免导入生产会话。
2. 先允许只读任务；将写操作限制为预览、审批、回滚和审计完整的站点。
3. 抓取并审查安装、首次启动和任务执行期间的网络连接、文件访问与 skill 写入位置。
4. 用自身代表性网页任务比较成功率、耗时、失败恢复和人工干预次数，不采用项目方宣传数字作为选型结论。

## 参考资料

- [GitHub 仓库](https://github.com/citrolabs/ego-lite)
- [上游安装与 Quick Start](https://github.com/citrolabs/ego-lite#quick-start)
- [官方文档](https://lite.ego.app/document/)
- [官方 X 观察入口](https://x.com/ego_agent)
- [GitHub REST API 元数据快照](https://api.github.com/repos/citrolabs/ego-lite)
