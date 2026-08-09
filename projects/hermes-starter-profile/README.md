<!-- markdownlint-disable MD013 -->

# hermes-starter-profile

- 仓库：[teknium1/hermes-starter-profile](https://github.com/teknium1/hermes-starter-profile)
- 快照：2026-08-10 抓取；GitHub API 显示其创建于 2026-08-09，约 26 stars、3 forks，MIT。数字会随时间变化。
- 分类：Agent 框架与技能生态

## 定位

为 Hermes Agent 新用户提供的最小权限 profile。它保留对话、网页搜索、图像理解/生成和文本转语音的入口，而默认关闭终端、文件、浏览器控制、自动化、记忆、skill 管理和 subagent。

## 用法

先安装 Hermes Agent，再运行 `hermes profile install github.com/teknium1/hermes-starter-profile --alias`；README 建议用 `starter-hermes setup --portal` 或 `starter-hermes model` 选择 provider，之后以 `starter-hermes chat` 对话。安装前应查看 profile 预览，并以 `starter-hermes status`、`starter-hermes tools` 检查实际生效的 provider 与工具。

## 原理

profile 是独立的配置空间，拥有自己的模型选择、凭据、会话、人格和工具设置。该仓库通过限制工具集合而非修改模型来缩小首次试用的操作面；其审计脚本用于确认受限基线仍解析为预期工具集。

## 价值

它把“先试聊天和媒体能力、后按需开放高风险动作”做成可安装配置，适合培训、演示和对 agent 权限模型的入门验证。独立 profile 也避免直接覆写用户原有 Hermes 配置。

## 风险边界

受限 profile 不是操作系统沙箱；可用的搜索、图像、语音仍受实际 provider 的数据和账户条款约束。安装脚本、profile 更新和 provider 授权都应先审阅；26 stars 仅是早期信号，不能替代供应链、隐私或隔离评估。

## 补充建议

在单独的测试 profile 与独立账号中试用，固定并审阅安装时的配置差异。仅在确有需求且了解数据流后逐项开放工具；保留 `starter-hermes` 而非裸 `hermes` 的调用路径，避免意外落到权限更宽的默认 profile。

## 参考资料

- [项目 README](https://github.com/teknium1/hermes-starter-profile)
- [权限与隐私设计说明](https://github.com/teknium1/hermes-starter-profile/blob/main/DESIGN.md)
- [GitHub API 元数据快照](https://api.github.com/repos/teknium1/hermes-starter-profile)
