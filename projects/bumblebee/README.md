# bumblebee

- GitHub：<https://github.com/perplexityai/bumblebee>
- 抓取时间：2026-07-03（Asia/Shanghai）
- 今日信号：GitHub API 显示该仓库创建于 2026-05-20，抓取时约 `4.7k stars / 421 forks`；README 明确覆盖 MCP 配置、agent skills lock 文件和开发者端点供应链暴露排查。

## 定位

`bumblebee` 是 Perplexity 开源的只读开发者端点清点工具，面向供应链事件响应。它扫描 macOS / Linux 开发机器上的包管理器、编辑器扩展、浏览器扩展、MCP 配置和 agent skill lock 文件，把“这台机器是否暴露在某个已知风险组件上”转换成结构化 NDJSON 记录。

它不是传统 SBOM 生成器，也不是 EDR。它更适合在已经知道某个包、扩展或版本有风险时，快速找出哪些开发者机器本地元数据里出现了匹配项。

## 用法

安装：

```bash
go install github.com/perplexityai/bumblebee/cmd/bumblebee@latest
```

自检：

```bash
bumblebee selftest
```

典型扫描：

```bash
bumblebee scan --profile baseline > inventory.ndjson

bumblebee scan --profile project \
  --root "$HOME/code" \
  --root "$HOME/Developer"

bumblebee scan --profile deep \
  --root "$HOME" \
  --exposure-catalog ./catalog.json \
  --max-duration 10m
```

## 原理

项目采用单个 Go 静态二进制，读取本地元数据而不执行包管理器命令：

- npm / pnpm / Yarn / Bun lockfile 与安装元数据。
- PyPI、Go modules、RubyGems、Composer、Homebrew。
- VS Code、Cursor、Windsurf、VSCodium 等编辑器扩展。
- Chromium / Firefox 浏览器扩展。
- MCP host JSON 配置，以及 `skills` / agent skill lock 文件。

它输出组件记录和扫描摘要；当提供 exposure catalog 时，只输出或标记匹配风险项。

## 价值

- 对 AI 开发团队：MCP server、agent skill、编辑器扩展和本地包依赖正在成为新的供应链入口，bumblebee 把这些入口纳入统一清点。
- 对安全响应：在事件发生后，可以比人工询问或全盘 grep 更快地找出受影响端点。
- 对 agent 生态：补足“agent 能装工具/技能之后，谁来清点和验证本地暴露面”的治理环节。

## 风险边界

- 它只读元数据，不代表能证明代码实际执行过，也不能替代 EDR、网络检测或依赖审计。
- 非 JSON 配置和 loose `SKILL.md` 目录在当前版本覆盖有限，可能漏掉部分 agent 配置。
- 深度扫描 `$HOME` 仍需注意隐私和性能，团队部署应明确扫描范围和数据保留策略。

## 补充建议

- 与 Cloudflare `security-audit-skill`、NVIDIA `SkillSpector`、`nvidia-skills`、`agents` 放在一起看：它们分别覆盖代码审计、技能安全扫描、技能目录和端点暴露清点。
- 对 MCP 重度使用团队，建议先用 `baseline` 盘点全局配置，再用 `project` 扫描主要代码目录。
- 后续观察它是否会支持 Codex `config.toml`、Continue YAML 等更多 agent 配置格式。

## 参考资料

- GitHub 仓库：<https://github.com/perplexityai/bumblebee>
- Inventory sources 文档：<https://github.com/perplexityai/bumblebee/blob/main/docs/inventory-sources.md>
- Transport 文档：<https://github.com/perplexityai/bumblebee/blob/main/docs/transport.md>
