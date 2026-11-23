<!-- markdownlint-disable MD013 -->

# DaVinci Resolve MCP Server

> 更新：2026-11-24（Asia/Shanghai）。分类：语音、视频与多模态。上游 `samuelgursky/davinci-resolve-mcp`，仓库 ID `950355259`；固定主干 `d7dcfc7eca0d0d131ac4a7433484724ec864e276`，对应 v5.4.0。本文为资料与局部源码静态核读，未安装、连接 Resolve、处理媒体或验收功能；热度见[当日日报](../../daily/2026-11-24/ai-hotspots.md)。

## 定位

把 Resolve 官方 Scripting API 和剪辑工作流封装为 MCP，供 Agent 管理媒体池、时间线、标记、调色、Fusion 和交付。默认 compound 模式按动作分组，README 当前列 37 个工具；`--full` 为 390 个细粒度工具。另有可选 Node 离线服务器处理项目文件，不能混同为实时编辑器的全部能力。[README](https://github.com/samuelgursky/davinci-resolve-mcp/blob/d7dcfc7eca0d0d131ac4a7433484724ec864e276/README.md)

## 用法

官方快捷入口是 `npx davinci-resolve-mcp setup`，会安装用户目录副本、建立 Python 环境并可写 MCP 客户端配置；本轮没有执行。npm 5.4.0 元数据要求 Node `>=20.9`；Python 3.10–3.12 是上游建议的低风险范围，较新 Python 与 Resolve 版本须配对。复现实验应固定源码 SHA，使用 `python install.py` 前先检查安装目标与客户端配置变更。[package.json](https://github.com/samuelgursky/davinci-resolve-mcp/blob/d7dcfc7eca0d0d131ac4a7433484724ec864e276/package.json)、[npm 5.4.0 元数据](https://registry.npmjs.org/davinci-resolve-mcp/5.4.0)

Studio 外部脚本设为 Local，先在一次性项目里只读核版本、媒体池与时间线。免费版不是一律可用或一律不可用：上游提供 authenticated loopback 的 in-app bridge，记录了 21.0.x 路径；免费 21.1 不再列出 Python 脚本，Console 路径仍未确认。旧视频中的“必须 Studio”也不能代替当前版本兼容矩阵。[README](https://github.com/samuelgursky/davinci-resolve-mcp/blob/d7dcfc7eca0d0d131ac4a7433484724ec864e276/README.md)

## 原理

stdio MCP 以当前系统用户身份调用 Resolve；compound 层组合 API、确认 token、时间线归档和审计。默认不监听网络，可选控制面板与 HTTP transport 使用 token。面板限定 loopback；transport 可通过环境变量扩大监听范围，wildcard 且无 Host allowlist 时只剩 bearer gate，不能从“默认本机”推断任何配置都只在本机。[SECURITY.md](https://github.com/samuelgursky/davinci-resolve-mcp/blob/d7dcfc7eca0d0d131ac4a7433484724ec864e276/SECURITY.md)

v5.4.0 新增可插拔 transport provider，补 Resolve 19.x 的播放状态、按钮与播放中捕帧缺口；它是管理员指定的本机可执行程序，不随包附带。未配置返回 `PROVIDER_MISSING`；捕帧默认 `refuse`，`live` 取最新帧，`pause` 才请求暂停、精确取帧及恢复。实现检查回传路径与文件存在，但 provider 自报 verdict 仍须目标机器验收。[provider 实现](https://github.com/samuelgursky/davinci-resolve-mcp/blob/d7dcfc7eca0d0d131ac4a7433484724ec864e276/src/utils/transport_provider.py)、[v5.4.0](https://github.com/samuelgursky/davinci-resolve-mcp/releases/tag/v5.4.0)

## 价值

适合重复性素材整理、标记、项目状态查询和可审阅的编辑计划。API 查询、计划、执行和结果读回可形成追踪链；“调用成功”还需对应实际帧、声音和保存后的工程，不能直接当成剪辑质量或艺术验收。

## 风险边界

- **分析默认包含写入。** `analyze_media` 默认执行视觉 / 转写并回写项目摘要与媒体池标记；`host_chat_paths` 把抽帧绝对路径交给宿主模型，需 `commit_vision` 完成。`publish_metadata=false`、`timed_markers=no`、`dry_run=true` 等用途不同，不能把“源媒体不改”理解成整个项目只读或素材不外发。[分析指南](https://github.com/samuelgursky/davinci-resolve-mcp/blob/d7dcfc7eca0d0d131ac4a7433484724ec864e276/docs/guides/media-analysis-guide.md)
- **护栏有默认值和覆盖范围。** `_safe_mode_enabled()` 缺省为 false；启用后针对已识别的高 / 严重风险动作，存在显式 override。compound 归档在非 strict 情况下失败可继续；代码默认 strict 包括删轨及 ripple 删片，`delete_timelines` 走归档 / 确认 gate，README 把它也列为默认 strict，文字有出入。granular 执行 safe mode / 审计而不做归档，需分别验证恢复。[destructive_hook.py](https://github.com/samuelgursky/davinci-resolve-mcp/blob/d7dcfc7eca0d0d131ac4a7433484724ec864e276/src/utils/destructive_hook.py)
- **100% 有限定分母。** 361/361 是随附 legacy API 基线的覆盖；349/361（96.7%）是上游历史 live 测试覆盖，349/349（100%）是已测方法通过率，并非新版全部 API、所有动作与版本成功。README 旧 badge 93.6%、参考页旧工具数 36/365 与正文 37/390 并存，不能混算；本轮未复跑。[覆盖说明](https://github.com/samuelgursky/davinci-resolve-mcp/blob/d7dcfc7eca0d0d131ac4a7433484724ec864e276/docs/reference/api-coverage.md)
- **新 provider 的验收有限。** 发行说明将修复前 Studio 19.1.3 的实机检查与后续路径等修复的离线测试分开；4521 个离线测试的作者报告不等于本轮运行或全平台实测。[发行说明](https://github.com/samuelgursky/davinci-resolve-mcp/releases/tag/v5.4.0)
- 代码为 MIT；Resolve、本机可执行 provider、FFmpeg 与可选模型 / 权重分别有自己的条件和数据路径。[LICENSE](https://github.com/samuelgursky/davinci-resolve-mcp/blob/d7dcfc7eca0d0d131ac4a7433484724ec864e276/LICENSE)

## 补充建议

用公开测试片与工程副本，从只读清单 → 单标记写入 → 保存 / 重开 → 时间线归档恢复逐项验收。先关闭不需要的分析与发布选项，再核实际媒体、日志和模型路径；对 provider 另测缺失、超时、状态不一致及恢复失败。完整回看 / 回听交付片后，再讨论自动剪辑收益。

## 参考资料

- [上游仓库](https://github.com/samuelgursky/davinci-resolve-mcp)、[仓库 API](https://api.github.com/repos/samuelgursky/davinci-resolve-mcp)、[v5.4.0](https://github.com/samuelgursky/davinci-resolve-mcp/releases/tag/v5.4.0)
- 固定 SHA 的 [README](https://github.com/samuelgursky/davinci-resolve-mcp/blob/d7dcfc7eca0d0d131ac4a7433484724ec864e276/README.md)、[安全策略](https://github.com/samuelgursky/davinci-resolve-mcp/blob/d7dcfc7eca0d0d131ac4a7433484724ec864e276/SECURITY.md)、[权限 / 归档实现](https://github.com/samuelgursky/davinci-resolve-mcp/blob/d7dcfc7eca0d0d131ac4a7433484724ec864e276/src/utils/destructive_hook.py)、[transport provider](https://github.com/samuelgursky/davinci-resolve-mcp/blob/d7dcfc7eca0d0d131ac4a7433484724ec864e276/src/utils/transport_provider.py)
- [覆盖口径](https://github.com/samuelgursky/davinci-resolve-mcp/blob/d7dcfc7eca0d0d131ac4a7433484724ec864e276/docs/reference/api-coverage.md)、[分析指南](https://github.com/samuelgursky/davinci-resolve-mcp/blob/d7dcfc7eca0d0d131ac4a7433484724ec864e276/docs/guides/media-analysis-guide.md)、[npm 版本元数据](https://registry.npmjs.org/davinci-resolve-mcp/5.4.0)
