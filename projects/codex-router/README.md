<!-- markdownlint-disable MD013 -->

# codex-router

## 定位

`codex-router` 是一个社区维护的 Codex 外部模型路由器，让用户在保留原生 GPT 模型和 ChatGPT 登录的同时，把 Kimi、DeepSeek 等外部模型加入 Codex model picker。它属于 Codex 周边配置 / 模型路由层，而不是独立 coding agent。

## 今日信号

- GitHub：<https://github.com/duolahypercho/codex-router>
- 创建时间：2026-07-19。
- 抓取时约 107 stars、9 forks。
- 语言 / 许可证：JavaScript，MIT。
- Topics：`codex`、`deepseek`、`kimi`、`litellm`、`model-router`。

## 用法

项目提供 guided installer。macOS / Linux 用户可通过 install script 安装，Windows 通过 PowerShell 安装。安装器会检测已有认证、选择启用 provider、设置服务、运行 doctor，并要求用户自行重启 Codex。README 强调不要在聊天中粘贴 API key，API key 输入走隐藏终端 prompt。

## 原理

codex-router 在本地维护 provider catalog 与 routing service，把特定模型标签映射到 Kimi OAuth、Kimi API 或 DeepSeek API 等后端。它尽量只迁移识别过的旧版本，并提供 rollback snapshot、doctor、support bundle 和 provider enable / disable 命令。

## 价值

- 对 Codex 重度用户而言，它把“多模型实验”从手工改配置变成可诊断、可回滚的安装流程。
- 体现了 coding agent 生态的一个新趋势：模型选择权、成本控制和 provider routing 正在成为用户侧基础设施。
- 其“不要把密钥发给 agent”的安装约束值得作为同类工具的最低安全线。

## 风险边界

- 社区项目，不隶属于 OpenAI、Moonshot、DeepSeek 或 OpenRouter。
- 路由层会接触本地 Codex 配置、provider token 和模型调用链，必须仔细审查脚本和文件权限。
- 外部模型能力、计费、上下文限制和数据保留策略由各 provider 控制，不能按 Codex 原生模型假设。

## 补充建议

- 后续跟踪它是否支持更多 provider，以及 Codex App / CLI 更新后是否仍稳定。
- 适合与 `klaatcode`、`dao-code`、`Rapid-MLX` 一起观察“成本工程 + 模型路由”路线。
- 对团队环境，应优先用集中密钥管理和受控配置，而不是每台机器手工安装。

## 参考资料

- GitHub 仓库：<https://github.com/duolahypercho/codex-router>
- README：<https://github.com/duolahypercho/codex-router#readme>
- Codex：<https://developers.openai.com/codex/>
