<!-- markdownlint-disable MD013 -->

# switch（sandbox-quantum/switch）

- 更新：2026-11-06（Asia/Shanghai）；官方 Python daily +215，为读取快照，不是自然日结算。
- GitHub API：3,938 stars / 281 forks / 529 open issues（含 PR）；仓库 ID `1302612528`。
- 核读基线：`3d35bf55d0eaf02c76b442b9cb4f71b826267160`；文档与抽样实现核验，不是安装运行、安全或性能认证。

## 定位

Switch 将 Slack、Teams、Discord、Telegram、Mattermost 的频道组织为人与 Agent 共用的 room，连接已有 Claude Code、Codex 等执行器。适合团队在原有聊天工具中交接问题、上下文与工作；模型和底层 Agent 仍需另行配置。

## 用法

1. 从固定的 `switch-console-v0.40.1` 发行页选择匹配系统与架构的 Console；该稳定版打包 Core 0.31.0。不要将列表顶部自动生成的 controller `dev` 预发行包当桌面安装包。
2. 按 README 打开 Console，由 switch-buddy 引导创建 Agent、频道及聊天集成。先用独立测试频道与只读工具，确认成员、room 和 Agent 可见范围。
3. 分别核对执行器的工作目录、模型凭据、文件 / shell 权限与远端部署方式。界面中的协作流程不会自动收窄执行器的实际权限。
4. Console 首次启动或 Settings → General 可关闭 Share usage data；Core 遥测由独立配置控制，修改托管服务的设置可能需重启。

本轮只核读文档与抽样实现，未安装 Console、登录聊天平台或派发 Agent。

## 原理

Console 将 session 与 room 绑定，一条 session 最多参加一个 room；监听器可在收到发给 Agent 的 room 活动时自动启动会话。持久 host 经服务器把带身份的事件送入 provider 适配器，文档还规定用命令收据与恢复 epoch 管理未知结果，避免隐式重发。room 共享上下文、工具执行和聊天桥接是不同层次，跨层仍需各自鉴权与恢复测试。

## 价值

团队可以保留讨论和交接轨迹，并替换模型或执行器。更有价值的验证对象是跨频道可见性、重复投递和中断恢复，而不是演示里多个机器人轮流说话。Trust / ROI 是另外介绍的产品能力，不能仅由此仓库存在推断所有保护已默认启用。

## 风险边界

- **许可需按完整文件理解**：根 LICENSE 为 Apache-2.0 加修改过的 Commons Clause，限制对软件及衍生品的 Sell，定义还覆盖以其功能为主要价值的收费托管 / 支持。API 因此标为 `NOASSERTION`；勿只写成无附加条件的 Apache-2.0。
- **自托管的数据出口**：聊天平台、模型、集成工具与可选远端 host 各自构成数据流；“上下文归你所有”不等于所有内容都不离开机器。
- **遥测分层**：README 说明 Console 默认开启、可退出；Core 仅 `TELEMETRY_ENABLED=true` 时开启，默认关闭。字段白名单和不收集内容是上游设计声明，本轮未抓包验证。
- **源码 / 制品分开**：今日 main 已包含后续变更；稳定桌面包、开发 controller 与 README 不能视为同一产品快照。自动会话启动也需要成本和停止条件。

## 补充建议

用两个测试 room、两个权限不同的用户和一个只读 Agent，先验证越权读取、撤销权限、中断恢复、未知收据与重复消息。对每个 provider 记录版本、凭据来源、预算和审批方式，再评估接入真实团队。保留完整许可证及依赖许可，涉及收费再分发时先明确适用条件。

## 参考资料

- [README.md](https://github.com/sandbox-quantum/switch/blob/3d35bf55d0eaf02c76b442b9cb4f71b826267160/README.md)
- [LICENSE](https://github.com/sandbox-quantum/switch/blob/3d35bf55d0eaf02c76b442b9cb4f71b826267160/LICENSE)
- [docs/TELEMETRY.md](https://github.com/sandbox-quantum/switch/blob/3d35bf55d0eaf02c76b442b9cb4f71b826267160/docs/TELEMETRY.md)
- [console/agents/architecture/switch-rooms.md](https://github.com/sandbox-quantum/switch/blob/3d35bf55d0eaf02c76b442b9cb4f71b826267160/console/agents/architecture/switch-rooms.md)
- [仓库与 API 快照](https://api.github.com/repos/sandbox-quantum/switch)；[发行列表](https://github.com/sandbox-quantum/switch/releases)。
- [稳定桌面发行 switch-console-v0.40.1](https://github.com/sandbox-quantum/switch/releases/tag/switch-console-v0.40.1)。
