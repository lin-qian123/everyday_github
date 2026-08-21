<!-- markdownlint-disable MD013 -->

# claudish-to-english

> 上游仓库：[Leutenegger/claudish-to-english](https://github.com/Leutenegger/claudish-to-english) · 归类：Coding Agents 与终端助手 · 本页基于 2026-08-22 的上游 README 与 GitHub API 快照整理。

## 定位

`claudish-to-english` 是 Claude Code 插件：它通过显示 hook 将每条助手回复重写为更易读的自然语言，默认调用本地 Ollama，也可选择 Codex CLI、Anthropic API 或任意 OpenAI 兼容端点。默认模式只影响屏幕显示，原始 transcript 保持不变；另一个 Markdown 改写 hook 是显式 opt-in，可能实际修改文件。

API 快照：约 579 stars、61 forks、0 个开放 issue；创建于 2026-08-21；许可证 MIT。这是一天内的早期公开关注信号，不是 GitHub Trending 排名、质量、安全性或生产成熟度证明。

## 用法

先阅读 hook、provider 和权限配置，并在临时 Claude Code profile 中试用。上游给出的安装方式为：

```sh
/plugin marketplace add gvzdv/claudish-to-english
/plugin install claudish-to-english@gvzdv-plugins

# 不安装、仅本次会话加载
claude --plugin-dir /path/to/claudish-to-english
```

默认本地路径需要运行中的 Ollama、已下载模型、`jq` 与 `curl`。例如可在用户的 Claude Code `settings.json` 中指定模型与显示模式：

```json
{
  "env": {
    "CLAUDISH_MODEL": "gemma4:26b-mlx",
    "CLAUDISH_MODE": "append"
  }
}
```

会话内可用 `/claudish off`、`/claudish append`、`/claudish replace`、`/claudish language 简体中文` 等命令调整。Windows 不能直接使用 README 所列的 MLX 默认模型，必须改成适合本机的非 MLX Ollama tag。

## 原理

- `MessageDisplay` hook 先缓存流式输出，等回复完成后把原文交给选定 provider 生成改写，再以 append 或 replace 模式显示；失败、超时、缺 key 或模型不可用时 fail-open，显示原文。
- 可选的 `PostToolUse` hook 仅在 `CLAUDISH_MD_DIR` 指定目录下处理 Markdown；它有独立的超时与覆盖模式，因而从“显示变换”进入了真实文件写入路径。
- provider 层可调用本地 Ollama、已登录的 Codex CLI、Anthropic 或 OpenAI 兼容 API；状态开关存于 `~/.claude/` 的 flag 文件，并在每条消息时重新读取。

## 价值

- 将术语密集或冗长的输出转成可读文本，同时保留原始 transcript，适合在不改变 agent 实际上下文的情况下改善阅读体验。
- 本地 Ollama 默认路径可避免把改写内容交给云端 provider；fail-open 设计也避免改写故障阻断主会话。
- 提供语言、样式、模型和文件范围的配置，能作为“原文—显示层—可选交付物改写”分离的可审查案例。

## 风险边界

- 改写可能遗漏限定条件、数字、命令或否定词；它不能代替阅读原文，更不能作为技术、医疗、法律或安全结论的唯一依据。
- 选择 Anthropic、OpenAI 或兼容云端时，助手消息；若启用 Markdown hook，文件内容也会离开本机。API key、代理 URL、日志保留与数据处理条款须单独审计。
- 插件 hook 运行在用户环境中；安装前应审查脚本、固定 revision，并谨慎处理 `~/.claude/` 配置与 provider 凭据。
- Markdown hook 会修改文件。`CLAUDISH_MD_DIR` 应指向副本或草稿目录，版本控制与人工 diff 审阅不可省略。

## 补充建议

1. 先只启用显示 hook，并用含命令、数字、否定、代码块和中英文混排的固定样例对照原文，量化遗漏和误改。
2. 使用本地小模型时记录模型 tag、响应延迟、内存占用与失败率；云端 provider 则单列数据外发审批与成本上限。
3. 若确实要启用文件改写，限制到 `agent-drafts/`，要求 Git diff、人审和可回滚备份；不要直接覆盖正式规范或研究记录。
4. 为 hook 与 provider 更新设回归测试，确认超时、断网和错误凭据均能保持原文而非截断内容。

## 参考资料

- [上游 README 与安装说明](https://github.com/Leutenegger/claudish-to-english)
- [GitHub API 元数据](https://api.github.com/repos/Leutenegger/claudish-to-english)
- [Claude Code plugins 文档](https://docs.anthropic.com/en/docs/claude-code/plugins)
- [Ollama 文档](https://docs.ollama.com/)
