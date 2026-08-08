<!-- markdownlint-disable MD013 -->

# Cove Sensory MCP

- 仓库：[moonlin1213/cove-sensory-mcp](https://github.com/moonlin1213/cove-sensory-mcp)
- 快照：2026-08-09 抓取；GitHub API 显示其创建于 2026-08-08，约 15 stars、4 forks，Apache-2.0。数字会随时间变化。
- 分类：语音、视频与多模态

## 定位

一个本地 stdio MCP server，为文本型 agent 提供受显式授权的图像、视频、音频和音乐感知能力。它是感知层，不提供常驻监控、播放、记忆、人格或自动调用策略。

## 用法

项目要求 Python 3.11+、Git 和 `uv`：克隆后运行 `uv sync --locked`、`uv run cove-sensory-mcp doctor`，再用 `print-config` 输出适配 Codex、Claude 等 client 的本地 MCP 配置。以交互式 `configure` 将密钥放入系统凭据库、逐个授权可读目录；视频/音频处理另需系统 FFmpeg。

## 原理

server 只允许配置根目录内的绝对本地路径，或直接 HTTPS 媒体 URL，并阻断重定向、私网、localhost、凭据和元数据端点。它把获授权媒体按能力分派给 Gemini、MiniMax-M3 或通过自检的自定义 provider；provider 能力、密钥存在性和诊断结果由状态工具以脱敏形式返回。

## 价值

将媒体访问、provider 选择和路径边界收敛到一个本地 MCP 层，可避免 agent 任意读取磁盘或把所有内容交给同一云端服务。状态检查、自检和显式根目录也便于在复杂多 agent 工作流中暴露配置错误。

## 风险边界

“本地 MCP”不等于媒体不出设备：被选择的 provider 会接收媒体，适用其地区、保留、计费与隐私政策。模型描述也不等同于内容鉴定。自定义 provider、FFmpeg 二进制和所有被授权路径均扩大供应链与数据暴露面。

## 补充建议

只授权一个专门的临时媒体目录，先以非敏感小样本完成 `doctor` 和自检。对每个 provider 单独确认数据处理条款与预算，保留请求审计但不要记录密钥或原始敏感媒体；生产用途应再加人工复核和内容访问审批。

## 参考资料

- [项目 README](https://github.com/moonlin1213/cove-sensory-mcp)
- [安全说明](https://github.com/moonlin1213/cove-sensory-mcp/blob/main/SECURITY.md)
- [GitHub API 元数据快照](https://api.github.com/repos/moonlin1213/cove-sensory-mcp)
