<!-- markdownlint-disable MD013 -->

# lark-cli（larksuite/cli）中文解读

> 证据快照：2026-09-10（Asia/Shanghai）。GitHub REST API 显示 17,098 stars、1,376 forks、665 open issues，MIT；最新 release 与 package 版本均为 `v1.0.94` / `1.0.94`。本文未登录飞书 / Lark、未授予 OAuth scope，也未调用真实业务 API。

## 定位

`lark-cli` 是 larksuite 团队维护的官方 Lark / 飞书命令行工具，面向人类和 AI agents 统一访问 Messenger、Docs、Drive、Base、Sheets、Slides、Calendar、Mail、Tasks、Meetings、Approval、OKR 等业务域。

仓库把 200+ commands、shortcuts、raw API 与 26 个 agent skills 组织为三层命令系统，目标是让 agent 不必自己拼装所有开放平台请求。

## 用法

推荐安装与初始化入口为：

```bash
npx @larksuite/cli@latest install
lark-cli config init
lark-cli auth login --scope "calendar:calendar:read"
lark-cli calendar +agenda
```

AI agent 模式可通过 `config init --new` 生成浏览器授权链接；也可用 `auth login --no-wait` 获取 device code 后继续轮询。`--as user` 与 `--as bot` 会改变执行身份，必须在日志中显式记录。

## 原理

- Shortcuts 提供面向人和 agent 的高层命令、智能默认值、结构化输出与部分 dry-run preview。
- API commands 与平台 schema 同步，raw API 层保留完整 Open Platform 覆盖。
- OAuth 登录可按 domain 或 exact scope 授权，并提供 `auth status`、`check`、`scopes` 与多身份切换。
- Skills 将常见 Lark 工作流封装为 agent 可发现的操作说明；enterprise extension 可收窄命令面并接入集中凭据与审计。
- 默认 risk-control 会向精确的官方 Feishu / Lark HTTPS 域名发送 OS 类型和硬件型号，用于异常 API 活动识别。

## 价值

- 一个工具覆盖消息、文档、表格、日历、任务和审批，减少多个 MCP / 自定义脚本的不一致。
- 三层命令让高频任务保持简洁，同时保留原始 API 逃生口。
- exact scope 检查、user / bot 身份选择和 enterprise wrapper 为最小权限与集中审计提供了可操作入口。
- Markdown / structured output 适合 agent 读写，官方维护也降低了 schema 漂移的集成成本。

## 风险边界

- agent 会在已授权 scope 内以用户或 bot 身份行动；模型幻觉、prompt injection 或身份选择错误可能导致敏感数据泄露、误发消息、误改文档或错误审批。
- `--recommend` 是便利入口，不保证对具体任务最小；应优先按 exact scope 授权，并在调用前 `auth check`。
- “输入注入保护、输出清洗、keychain”不能覆盖群聊中其他用户的恶意内容；上游明确建议不要把高权限 bot 放入多人群聊。
- 默认 risk-control 会发送 OS 与 hardware model；关闭会减少该信号，也可能降低上游异常识别能力，需按组织政策决定。
- 结构化成功响应只证明 API 接受请求，不证明业务语义、收件人、金额、时间、权限或后续状态正确。

## 补充建议

1. 为测试 app 创建最小 scope 与假数据空间，先覆盖读取、proposal、dry-run / preview，再开放写入。
2. 对消息发送、共享、删除、审批、日历邀请和外部联系人操作设置 allowlist、二次确认和 post-readback。
3. 固定 release，记录 app ID、actor identity、tenant、scope、命令、request ID 与最终业务对象状态；日志中脱敏 token 和正文。
4. 企业接入优先用 extension wrapper 收窄命令面，并把凭据放入 Vault / 数据库，而不是散落在 agent workspace。

## 参考资料

- GitHub：<https://github.com/larksuite/cli>
- GitHub REST API：<https://api.github.com/repos/larksuite/cli>
- Releases：<https://github.com/larksuite/cli/releases>
- 中文 README：<https://github.com/larksuite/cli/blob/main/README.zh.md>
- Agent skills：<https://github.com/larksuite/cli/tree/main/skills>
- 企业嵌入：<https://open.larksuite.com/document/mcp_open_tools/feishu-cli/embed-feishu-cli-in-agent>
- LICENSE：<https://github.com/larksuite/cli/blob/main/LICENSE>
