<!-- markdownlint-disable MD013 MD034 -->

# Plannotator：给 Agent 计划、文档与 Diff 加人工批注

> 上游仓库：https://github.com/backnotprop/plannotator · 归类：前端、UI 与 Agent 交互层 · 本页基于 2026-09-19 的 README、隐私 / 安装说明、package、release、LICENSE 与 REST API 静态整理；未安装 hooks、调用 Ask AI 或上传分享内容。

## 定位

Plannotator 是一个本地优先的人工审阅界面：Agent 给出计划、Markdown、HTML 或代码 diff 后，工具在浏览器中打开可批注视图，用户可高亮、删除、评论和给出建议，再把结构化反馈送回 Claude Code、Codex、OpenCode、Pi、Copilot CLI 等宿主。它补的是“计划模式只有终端文本、反馈粒度太粗”这一交互缺口。

2026-09-19 的 GitHub 官方 TypeScript Trending 抓取显示约 `+33 stars today`；REST API 快照为 `8,789 stars / 660 forks / 164 open issues`，API 标记 Apache-2.0，根 package 声明 `MIT OR Apache-2.0`。最新 release 为 `v0.27.16`（9 月 18 日）。

## 用法

macOS / Linux / WSL 的完整安装器会检测宿主并写入相应 hooks、skills 和命令：

```sh
curl -fsSL https://plannotator.ai/install.sh | bash
```

只装二进制可加 `--minimal`；安装后可使用 `!plannotator review`、`$plannotator-review` 或各宿主的 slash command。典型入口包括审阅未提交改动、GitHub PR、GitLab MR、URL、Markdown、HTML，以及 Agent 的上一条回复。

## 原理

- CLI / hook 监听计划或任务结束事件，启动本地浏览器 review surface，并把标注转成宿主可继续处理的反馈文本。
- 代码审阅支持 Git、GitButler、Jujutsu、Perforce、GitHub 与 GitLab；文档审阅保存本地历史和决策归档。
- 本地模式默认不采集 usage telemetry；每次界面加载会访问 GitHub 检查新版本，目前没有关闭此请求的设置。
- Ask AI / review agents 把所选问题及相关计划、文档、仓库或 diff 发给用户配置的模型 provider。
- 小型 Markdown 分享把压缩内容放在 URL fragment 中但不加密；大型 Markdown / raw HTML 用 AES-256-GCM 加密后上传 ciphertext，密钥仍在完整 URL 的 fragment 中。
- hosted Workspaces 是独立产品，不能沿用开源本地模式的存储假设。

## 价值

- 将“同意 / 拒绝整个计划”细化为针对句子、代码行和视觉结果的反馈，降低反复重写长提示词的成本。
- 在 Agent 真正执行前保留人工决策记录，适合需求澄清、计划评审和高影响改动的审阅闸门。
- 同一交互模型覆盖计划、文档、HTML 与 diff，便于团队形成统一的审阅习惯。
- 提供 TUI、浏览器和多个 Agent 宿主适配，能在不替换现有 Coding Agent 的情况下增强人机协作。

## 风险边界

- 一键安装器会下载二进制并修改多个宿主的 hook、skill、command 和配置；应先审阅脚本、锁版本或使用 `--minimal`。
- URL annotation 默认可经 Jina Reader 抓取页面；GitHub / GitLab 审阅调用已认证 CLI；Ask AI 会外发所选内容。
- 小分享不是加密数据，只是放在 fragment；任何获得完整 URL 的人或消息服务都能读取。大型分享虽加密，完整链接仍等同解密能力。
- 开源本地模式、share portal 与 hosted Workspaces 是三种不同数据边界，不能混写为“所有内容始终只在本地”。
- 自动打开 review surface 不证明计划正确；用户可能在时间压力下机械批准，Agent 也可能错误解释批注。
- 本页未验证卸载恢复、浏览器绑定、provider payload、短链实现、hook 竞态或 Windows 原生支持。

## 补充建议

1. 先用 `--minimal` 和副本仓库试验，记录安装 / 卸载前后的宿主配置差异，再决定是否启用自动 hook。
2. 涉及私有代码时禁用分享和 Ask AI，或使用经过批准的自托管服务；把完整分享 URL 按 secret 管理。
3. 给批注结果增加“接受后重述”和写后 diff 回读，确认 Agent 没有遗漏、反转或扩大用户意见。
4. 在团队内区分开源本地审阅、legacy 分享和 hosted Workspaces 的保留、访问控制与删除策略。

## 参考资料

- 上游 README：https://github.com/backnotprop/plannotator
- `v0.27.16` release：https://github.com/backnotprop/plannotator/releases/tag/v0.27.16
- 官方安装文档：https://docs.plannotator.ai/open-source/start/installation
- 官方隐私说明：https://plannotator.ai/privacy
- GitHub REST API：https://api.github.com/repos/backnotprop/plannotator
- LICENSE：https://github.com/backnotprop/plannotator/blob/main/LICENSE-APACHE
