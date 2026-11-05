<!-- markdownlint-disable MD013 -->

# gemini-skills（google-gemini/gemini-skills）

- 更新：2026-11-06（Asia/Shanghai）；官方 Python daily +12，为读取快照，不是自然日结算。
- GitHub API：4,403 stars / 482 forks / 14 open issues（含 PR）；仓库 ID `1151113612`。
- 核读基线：`7cfc690ba9c8efe36a5316e6d4000e2b6aa25dbf`；文档与抽样实现核验，不是安装运行、安全或性能认证。

## 定位

Google Gemini 组织的 API 开发技能库，将动态文档入口、SDK 用法与常见错误补入编码 Agent 的上下文。当前完整树包含四个技能：`gemini-api-dev`、`gemini-api-cli`、`gemini-live-api-dev`、`gemini-omni-flash-api`。Vertex AI 技能已迁至 google/skills，不能把旧路径当本库现存功能。

## 用法

在支持技能的编码助手中先浏览，再选择需要的单项：

```bash
npx skills add google-gemini/gemini-skills --list
npx skills add google-gemini/gemini-skills --skill gemini-api-dev
```

这是 README 的安装示例，会获取远端内容；希望可复现时应另保存所选 commit 与安装后文件。让 Agent 按任务读取对应的最新官方文档，再核实 SDK、模型、权限和配额。

`gemini-api-cli` 指 API 命令行客户端，区别于交互式 `@google/gemini-cli` 编码 Agent。技能文档说明凭据按命令参数、环境变量、系统 keychain、配置文件依次解析；环境变量可能覆盖刚配置的 key。这里只介绍路径，本轮未安装技能或 CLI、配置 key、调用付费 API。

## 原理

技能由带触发说明的 SKILL.md 与配套脚本组成，给模型提供 API 约束和检索指引，并不更新模型权重。开发技能要求写代码前抓取相关文档；Live 项目关注双向 WebSocket、会话及临时凭据，视频技能还附上传和生成脚本。因此“装入技能”与“API 调用正确且业务可用”之间仍需要实际验证。

## 价值

适合降低旧 SDK、废弃模型和错误参数导致的试错，也方便把 API 使用规范沉淀进代码审阅。README 的 87% / 96% 是作者对特定模型和评估设置的代码任务结果，不能当所有 Agent、所有项目的成功率或本轮复现实测。

## 风险边界

- **动态知识仍可能冲突**：当前 README 的视频延长上限写累计 40 秒，视频 SKILL.md 概览写 30 秒；本轮不裁定真实服务上限，实际请求须以当时官方 API 文档和账户能力确认。
- **存储和云端执行**：开发技能说明 Interactions 默认存储；关闭存储又影响历史串联 / 后台任务。托管 Agent、文件上传、语音视频和第三方集成都要逐项核对数据出口，不能把本地技能文件视为离线运行。
- **安装与凭据**：CLI 技能展示下载脚本再执行的安装方式；应先审核、固定版本。headless 场景禁用 keychain 后可能转为配置文件，须核权限与日志脱敏。
- **执行权限独立**：技能提示词不能替代宿主对 shell、文件、联网或计费的授权；生成的代码与媒体还需内容 / 质量验收。
- 根许可 Apache-2.0；README 明确不是受官方支持的 Google 产品，也不属于其开源漏洞奖励范围。组织归属和支持承诺须分开。

## 补充建议

先选一个技能，在可丢弃小工程中对照固定 SDK 测试结构化输出、工具调用、超时重试与凭据优先级；使用最小合成输入和明确预算。另建一份当前文档 / commit / 模型 / SDK 记录，遇到 30 / 40 秒一类差异先核官方服务，不让 Agent 自动猜参数。

## 参考资料

- [README.md](https://github.com/google-gemini/gemini-skills/blob/7cfc690ba9c8efe36a5316e6d4000e2b6aa25dbf/README.md)
- [LICENSE](https://github.com/google-gemini/gemini-skills/blob/7cfc690ba9c8efe36a5316e6d4000e2b6aa25dbf/LICENSE)
- [skills/gemini-api-dev/SKILL.md](https://github.com/google-gemini/gemini-skills/blob/7cfc690ba9c8efe36a5316e6d4000e2b6aa25dbf/skills/gemini-api-dev/SKILL.md)
- [skills/gemini-api-cli/SKILL.md](https://github.com/google-gemini/gemini-skills/blob/7cfc690ba9c8efe36a5316e6d4000e2b6aa25dbf/skills/gemini-api-cli/SKILL.md)
- [skills/gemini-live-api-dev/SKILL.md](https://github.com/google-gemini/gemini-skills/blob/7cfc690ba9c8efe36a5316e6d4000e2b6aa25dbf/skills/gemini-live-api-dev/SKILL.md)
- [skills/gemini-omni-flash-api/SKILL.md](https://github.com/google-gemini/gemini-skills/blob/7cfc690ba9c8efe36a5316e6d4000e2b6aa25dbf/skills/gemini-omni-flash-api/SKILL.md)
- [仓库与 API 快照](https://api.github.com/repos/google-gemini/gemini-skills)；[发行列表](https://github.com/google-gemini/gemini-skills/releases)。
