<!-- markdownlint-disable MD013 MD034 -->

# Freebuff：以广告和访问层级支持的多入口 Coding Agent 产品组

> 上游仓库：https://github.com/CodebuffAI/freebuff · 归类：Coding Agents 与终端助手 · 本页基于 2026-09-18 的 README、中文 README、privacy 说明、package、SECURITY、LICENSE 与 REST API 静态整理；未登录、未运行 included models，也未验证“免费”额度。

## 定位

Freebuff 把 Desktop、CLI、Web、Cloud 和 Chat 五个入口放在同一 TypeScript / Bun monorepo 中：本地并行 coding agents、终端改码、浏览器建站、GitHub cloud agent 与研究聊天共享一组专用 agents 和模型目录。上游称 included models 由文本广告支持，无需用户 API key。

2026-09-18 的 GitHub 官方 TypeScript Trending 抓取显示约 `+76 stars today`；REST API 快照为 `12,274 stars / 1,314 forks / 325 open issues`，Apache-2.0，无 GitHub Release。npm `freebuff` 快照为 `0.0.176`，根 monorepo package 为 `1.0.0`。

## 用法

CLI 的最小入口为：

```sh
npm install -g freebuff
cd path/to/project
freebuff
```

源码开发要求 Bun `1.3.14`、Docker 与 `.env.local`；Desktop 也可调用本机已有的 Claude Code / Codex 及其 provider 账号，这与 Freebuff included catalog 是两条数据和计费路径。

## 原理

- file-finding agents 先定位代码上下文，再由 implementation / review agents 编辑、执行命令和检查结果。
- Desktop 为并行任务提供独立 workspace；Web / Cloud 提供托管 sandbox、preview、terminal 与 deployment workflow。
- research / browser agents 读取网页或测试应用；底层 Codebuff framework 暴露自定义 agent 与 SDK。
- included model catalog 按 full / limited access、capacity 与地区动态路由；README 明确部分请求可落到量化模型或 fallback model。
- README 内嵌的数据使用声明称 prompts、messages、agent traces、code、files 与 repository data 会用于提供服务，并可能用于广告个性化；被标记的模型/功能还可能允许训练或评估使用。

## 价值

- 同一产品组覆盖本地 CLI、桌面并行和托管 GitHub workflow，适合比较不同执行面的权衡。
- included models 降低试用门槛，用户也可在 Desktop 复用已有 provider account。
- agents、tools、SDK、evals 与 runtime 在公开 monorepo 中，工程行为比纯闭源 SaaS 更可检查。
- Apache-2.0 允许二次研究与封装，但托管服务条款和模型数据政策仍须另看。

## 风险边界

- “free / no API key”不等于无交换条件：访问层级、地区、capacity、文本广告、referral / bounty 与数据使用政策会动态影响服务。
- 上游明确可能分析 prompt / message 做广告个性化，特定模型或功能还可能将提交用于训练、测试或改进；不应默认放入私有代码、secret 或客户数据。
- Cloud 连接 GitHub repository 会扩大 OAuth、写权限、部署和第三方 sandbox 范围；公开源码不证明 hosted backend 与当前 checkout 完全相同。
- 模型目录、fallback、量化版本和每日 session 会变化，同名模型不保证固定权重、延迟或重现性。
- Agent 可改文件和运行命令；workspace 隔离不是 OS 级 sandbox，也不能替代 diff、测试、secret scanner 与人工审查。
- 本页未运行 npm package、Desktop 或 Cloud，未验证额度、广告展示、数据删除、模型路由、sandbox 隔离或跨平台安装。

## 补充建议

1. 首次只用无 secret 的公开副本仓库，逐页读取当前 privacy notice、模型 data-use 标签、OAuth scopes 与删除政策。
2. 锁定 npm 版本，关闭自动部署，限制 GitHub token 到测试仓库，并在每次写入后做 diff / test / post-readback。
3. 把 included catalog 与本地 Claude Code / Codex 路径分开抓包和记账，记录实际 provider、fallback、session 与地域差异。
4. 需要处理机密代码时优先使用经组织批准的本地或企业 provider，不依赖“free”标签推断隐私和合规。

## 参考资料

- 上游 README：https://github.com/CodebuffAI/freebuff
- 中文 README：https://github.com/CodebuffAI/freebuff/blob/main/README.zh-CN.md
- Privacy Policy：https://freebuff.com/privacy-policy
- 贡献 / 开发说明：https://github.com/CodebuffAI/freebuff/blob/main/CONTRIBUTING.md
- GitHub REST API：https://api.github.com/repos/CodebuffAI/freebuff
- LICENSE：https://github.com/CodebuffAI/freebuff/blob/main/LICENSE
