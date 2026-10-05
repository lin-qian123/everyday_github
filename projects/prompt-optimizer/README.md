<!-- markdownlint-disable MD013 -->

# Prompt Optimizer（linshenkx/prompt-optimizer）

> 上游仓库：<https://github.com/linshenkx/prompt-optimizer> · 归类：前端、UI 与 Agent 交互层 · 本页基于 2026-10-06 的 GitHub API、中英文 README、用户文档、Release、manifest 与 LICENSE 静态整理，未输入 API key、连接模型、安装扩展 / 桌面端或复测提示词优化效果。

- 抓取快照：36,510 stars、4,207 forks、9 open issues。
- 热度信号：GitHub TypeScript Trending 抓取时约 +153 当日 stars；仓库创建于 2025 年，属于成熟项目再次上榜。
- 版本与许可：根 LICENSE / manifest 为 AGPL-3.0；GitHub API 显示 `NOASSERTION`；Release 与根 manifest 均为 `v2.11.10` / `2.11.10`。

## 定位

Prompt Optimizer 是可在 Web、桌面、浏览器扩展与 Docker 中使用的提示词工作台，覆盖系统提示、用户提示、图像提示、变量模板、版本收藏、单结果 / 多结果评测和多 provider 模型管理，并可通过 MCP 暴露优化能力。

## 用法

轻量路径是在在线版的 Model Manager 配置自己拥有的 provider API key，再进行优化、测试和比较；需要本地模型、跨域访问或更强控制时可使用桌面版或自托管 Docker。Docker 版可通过 `/mcp` 暴露 MCP 服务，自部署应设置访问认证、限制网络监听与 CORS，并避免把 `VITE_*` API key 注入公开前端构建。

## 原理

项目把 core、UI、Web、extension、desktop 与 MCP server 分成 pnpm workspace。提示词通过模板、变量和多轮优化形成候选，再调用选定模型做分析、评测与比较；应用数据主要保存在当前浏览器或本地客户端，模型请求直接发送到用户选择的 provider，自托管 MCP 则在服务端读取配置并代理调用。

## 价值

它把“写提示词”扩展为可保存、可比较、可回放的资产流程，并同时覆盖文本、图像、function calling 与多轮对话。多入口和 provider 可替换性适合团队建立自己的评测样例，而不是只凭一次看起来更好的回答判断优化成功。

## 风险边界

- “纯客户端”只表示项目不额外中转 Web 请求；prompt、参考图和输出仍会发送给选定模型 provider，受其保留、训练和地区政策约束。
- 浏览器 / 桌面存储、导出备份与日志可能包含 API key、内部 prompt、客户数据或图片；公开截图、问题单和备份前必须脱敏。
- 单模型自评、同源模型优化与比较容易产生循环偏好；结构更长或评分更高不等于任务准确率、稳健性或成本更优。
- Docker MCP 会形成可网络访问的模型调用面；历史部署文档出现宽松 CORS 示例，密码也不能替代 TLS、来源限制和速率控制。
- 图像优化 / 生成会处理参考图和文案，版权、肖像、品牌与生成输出权利需要单独确认。
- 本轮未运行作者测试、验证浏览器扩展权限、桌面自动更新、MCP 认证或 `v2.11.10` 的 provider 兼容矩阵。

## 补充建议

先用去敏 fixture 建立“原提示 / 候选 / 盲测 rubric / token / 延迟 / 费用”记录，至少用独立评审模型或人工盲评复核。自托管时固定 `v2.11.10`，把 MCP 绑定在受控网络并配置认证、TLS、CORS allowlist 和限流；备份文件按 secret 处理，公开部署中不要写入 `VITE_*` 私钥。

## 参考资料

- [GitHub 仓库](https://github.com/linshenkx/prompt-optimizer)
- [GitHub REST API](https://api.github.com/repos/linshenkx/prompt-optimizer)
- [中文 README](https://github.com/linshenkx/prompt-optimizer/blob/develop/README.zh-CN.md)
- [测试与评测文档](https://github.com/linshenkx/prompt-optimizer/blob/develop/mkdocs/docs/en/user/testing-evaluation.md)
- [常见问题与数据位置](https://github.com/linshenkx/prompt-optimizer/blob/develop/mkdocs/docs/en/help/common-questions.md)
- [Docker / MCP 架构记录](https://github.com/linshenkx/prompt-optimizer/blob/develop/docs/deployment/docker-mcp-integration.md)
- [`v2.11.10` Release](https://github.com/linshenkx/prompt-optimizer/releases/tag/v2.11.10)
- [根 manifest](https://github.com/linshenkx/prompt-optimizer/blob/develop/package.json)
- [AGPL-3.0 LICENSE](https://github.com/linshenkx/prompt-optimizer/blob/develop/LICENSE)
