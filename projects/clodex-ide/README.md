# clodex-ide

## 定位

`clodex-ide` 是一个本地优先、强调受控执行的开源 agentic IDE。它把 AI 任务、代码与 Git 工具、终端、浏览器、记忆、模型路由和执行策略放进 Electron 工作区，核心主张是“模型输出是不可信输入，权限来自显式策略、隔离运行时和用户审查”。

截至 2026-07-18 抓取时，仓库约 `833` stars、`149` forks，主要语言为 TypeScript，许可证为 `AGPL-3.0`。仓库 README 明确标注当前为 Technical Preview，公开桌面包是未签名的社区测试构建。

## 用法

- 面向想在本机使用多模型 coding agent、但又希望保留审查与执行边界的开发者。
- 支持 BYOK 接入 OpenAI、Anthropic、Google、自定义 OpenAI-compatible endpoint 或本地 Ollama。
- 社区构建提供 macOS、Windows、Linux 安装包，但 README 要求下载同版本 `SHA256SUMS.txt` 并校验安装包。
- 首次启动需要完成隐私/遥测选择，再配置模型 provider 并打开本地项目。

## 原理

项目把 IDE 视为 agent 的治理外壳，而不是简单聊天面板。它把任务、代码编辑、终端执行、浏览器、模型供应商、运行时隔离、隐私选择和审计材料组合到同一桌面应用中，并用 feature gate 区分已验证能力与尚未推广的执行 lane。

## 价值

- 把 agentic coding 从 CLI 单点体验推进到完整桌面工作区。
- 强调本地优先和 BYOK，降低对单一云端平台的绑定。
- 对 unsigned community build、遥测范围、安装校验和 feature gate 做了较细说明，适合作为“安全感更强的 agent IDE”样本观察。

## 风险边界

- 仍是技术预览，不应当按生产级 IDE 评估稳定性。
- 桌面安装包未 notarize / Authenticode 签名，必须自行校验 hash 与来源。
- AGPL-3.0 对商用集成有合规要求。
- 项目由个人/小团队主导，长期维护能力需要继续观察。

## 补充建议

- 后续重点看是否形成稳定 release、自动更新和签名链路。
- 关注其“受控执行”是否能拿出真实任务日志和失败案例，而不只是安全叙事。
- 可与 `codex`、`claude-code`、`OpenHands`、`Godcoder`、`Codex-X` 横向比较桌面 IDE、CLI agent 和配置控制面的边界。

## 参考资料

- GitHub: <https://github.com/mereyabdenbekuly-ctrl/clodex-ide>
- Website: <https://ide.clodex.xyz>
- Community prerelease: <https://github.com/mereyabdenbekuly-ctrl/clodex-ide/releases/tag/v1.16.0-communityobserved7>
