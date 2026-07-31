# hybrid-cli-ai

## 定位

`hybrid-cli-ai` 是跨平台自然语言终端助手：优先使用本地 Ollama，不可用时回退到 Groq Cloud，生成 shell 命令后默认展示并等待确认。截至 2026-08-01 的 GitHub API 快照，它创建于 2026-07-31，约 4 stars、0 forks、MIT；属于早期开发者信号。

## 用法

安装项目要求后，云端模式通过环境变量提供 `GROQ_API_KEY`；离线模式先安装 Ollama 并拉取模型，例如 `qwen2.5-coder:1.5b`。使用 `ai "列出今天修改的文件" --local` 预览建议命令；仅在理解命令影响后才使用 `--run` 跳过确认。

## 原理

工具先识别当前 shell 与系统，再选择本地或云端模型，清除模型返回的代码围栏和解释，只接受可执行命令形式，最后显示预览或执行。该流程减少误格式化，并不保证语义正确或安全。

## 价值

- 把本地与云端推理封装为同一终端入口，低配机器也可回退运行。
- 默认确认和历史记录有助于将自然语言到命令的过程变得可回看。

## 风险边界

- LLM 生成命令仍可能删除文件、泄露密钥、联网下载或执行错误操作；确认提示不是安全沙箱。
- 云端模式会把提示发送给服务商；命令、路径、日志和环境变量不得包含敏感信息。
- 小型本地模型更易生成错误命令，且仓库早期 star 数不能证明跨平台可靠性。

## 补充建议

在临时目录、只读数据和非管理员账号下测试；建立命令 allowlist 与审计日志，禁用自动执行。对高风险操作始终改用人工编写、review 过的脚本。

## 参考资料

- GitHub：<https://github.com/HereIsMuhammad/hybrid-cli-ai>
- GitHub API 快照：<https://api.github.com/repos/HereIsMuhammad/hybrid-cli-ai>
- Ollama：<https://ollama.com/>
