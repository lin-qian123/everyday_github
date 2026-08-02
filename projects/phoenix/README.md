# phoenix（不死鸟）

## 定位

`phoenix` 是 Hermes Agent 的第三方插件，试图在不修改 Hermes 核心的前提下增加模型路由、熔断、自愈、长任务守护、回复核验与隐私提醒。截至 2026-08-03 的 GitHub API 快照：项目创建于 2026-08-02，约 39 stars、6 forks；仓库 API 未返回 SPDX 字段，但项目 LICENSE 标示 CC BY-NC 4.0。

## 用法

从 Releases 下载发布包，在 macOS/Linux 执行 `bash install.sh` 或在 Windows 执行 `install.ps1`；安装器会复制插件到 `~/.hermes/plugins/phoenix_v7/` 并运行 `hermes phoenix-status`。先在无敏感任务中检查版本兼容、路由结果和失败恢复；卸载方式是删除该插件目录。

## 原理

插件通过 Hermes 官方钩子加载，使用四档加权规则选择模型；三态熔断器累计连续失败并冷却重试；“抗体库”记录错误模式；长任务通过 `/goal` 信号增加清单和高风险复核。README 声明这些模块有 198 项自动化测试，但本仓库未独立复跑。

## 价值

- 把成本、失败重试和高风险操作复核显式放入 agent 工作流。
- 保持为插件层，理论上可随卸载恢复，而不直接 fork/修改上游核心。

## 风险边界

- 模型路由、敏感词提醒和“幻觉核验”均是项目主张，不构成隐私、事实正确性或安全合规保证。
- CC BY-NC 4.0 对商业使用有限制；接入前应按组织用途确认授权。
- 自动降级模型可能改变数据出境、质量、延迟和账单；敏感内容应在发送前由策略阻断，而非仅事后提醒。

## 补充建议

固定一套低风险回归任务，对照启用前后的模型选择、费用、失败率和人工验收结果；将可发送的 provider、命令和数据类别写成外部策略，而不是只依赖插件规则。

## 参考资料

- GitHub：<https://github.com/xyaz1313/phoenix>
- Hermes Agent：<https://github.com/NousResearch/hermes-agent>
- GitHub API 快照：<https://api.github.com/repos/xyaz1313/phoenix>
