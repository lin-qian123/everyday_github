<!-- markdownlint-disable MD013 -->

# SkillSpector：在安装前检查 Agent 技能与 MCP 风险

- 主上游：[NVIDIA/SkillSpector](https://github.com/NVIDIA/SkillSpector)；repository ID `1187630119`。
- 采样日期：2026-10-27（Asia/Shanghai）；首次建档 2026-06-26，本轮刷新原页；分类：Agent 框架与技能生态。
- API 累计快照：22,132 stars / 1,932 forks / 175 open issues（含 PR 口径），与榜单日增分开。
- 默认分支 `main`；本页主线静态依据固定在 `d7338f58200a9ae2a24810cee08911ab68b107a7`。发行 API 首项 [v2.13.1](https://github.com/NVIDIA/SkillSpector/releases/tag/v2.13.1)，UTC 2026-10-23T09:40:35Z，正式发行标记。
- 核验层级：读取一手文档、许可、元数据与所列部分实现；未安装运行上游、调用模型或复现实验。

## 定位

SkillSpector 是 NVIDIA 的 Agent 技能扫描器，面向技能包、脚本、依赖、提示词及部分 MCP 输入，组合静态检测和可选模型分析。它适合安装前筛查与 CI 复扫；扫描器给出的 SAFE / safe_to_install 不能证明目标安全，也不会自动限制技能执行权限。

## 用法

在 Python ≥3.12、<3.15 的隔离环境固定源码或发行。上游提供 uv tool 安装，运行本地静态基线可用以下入口，本轮未执行：

```bash
uv tool install git+https://github.com/NVIDIA/skillspector.git
skillspector scan ./my-skill/ --no-llm --format json --output report.json
```

语义扫描再明确 provider、模型、数据出口和预算。接 MCP 需要额外安装 `skillspector[mcp]`；本地 stdio 与 HTTP 的目标范围不同。CI 应按自己的阈值配置，并考虑 `--fail-on-incomplete`、`--min-coverage`、`--fail-on-findings`，不能只看进程退出为零。

## 原理

摄取仓库、URL、压缩包或本地路径后，流水线解析文本 / AST / 依赖与特征，检查注入、数据外传、过量权限、记忆污染及 MCP 工具风险；可选 LLM 补充语义检查，再合并 finding、抑制基线、风险分数和终端 / JSON / Markdown / SARIF 报告。OSV 查询用于已知依赖漏洞，下载、解析、嵌套容器和分析时间有各自预算。

## 价值

适合把技能安装从“看 stars 决定”改成可追踪的来源、扫描、人工复核和后续重扫。MCP 接口可把检查放入 Agent 工作流，结构化报告也方便比较版本；收益仍取决于规则覆盖、误报处理和调用方是否执行策略。

## 风险边界

- README 的 26.1% 漏洞 / 5.2% 可能恶意比例限定于研究数据中 31,132 个已分析技能，不能外推为今天整个生态的真实比例；本轮未复现数据集标注或误报率。
- `--no-llm` 跳过模型分析，**不等于禁网**：远程输入、依赖来源和 OSV 查询仍可能联网。语义扫描可把技能内容发送至所选 provider，缺凭据 / 失败时需查真实扫描模式。
- CLI 的“不完整即失败”和“有 finding 即失败”默认均未开启。MCP 同时给出 `llm_requested`、`llm_available`、`llm_used`、`scan_mode` 和要求满足状态；低分不应掩盖未完成分析或被抑制的 finding。
- HTTP MCP 无内置认证，绑定限制为 loopback，并拒绝本地路径、带凭据的 URL 及非 HTTPS 目标；可达端口的本机调用者仍可触发扫描。stdio 的本地权限更广，远程代理需要独立认证。README 还保留 stdio 初始化 hang 的已知问题说明。
- 当前发行首项 v2.13.1，但所查主线 pyproject 版本字符串为 2.12.0；固定安装来源、commit 和包版本分别记录。代码 Apache-2.0，依赖与模型服务另计。

## 补充建议

用包含已知良性、恶性和边界样本的离线副本校准 finding，再在有网络出口记录的环境测试联网分析。CI 同时保存固定输入身份、扫描模式、完整性、覆盖率、抑制规则与原始 finding；复核后才授权安装。把扫描结果和宿主权限控制分开验收。

## 参考资料

- [README.md](https://github.com/NVIDIA/SkillSpector/blob/d7338f58200a9ae2a24810cee08911ab68b107a7/README.md)。
- [pyproject.toml](https://github.com/NVIDIA/SkillSpector/blob/d7338f58200a9ae2a24810cee08911ab68b107a7/pyproject.toml)。
- [src/skillspector/cli.py](https://github.com/NVIDIA/SkillSpector/blob/d7338f58200a9ae2a24810cee08911ab68b107a7/src/skillspector/cli.py)。
- [src/skillspector/mcp_server.py](https://github.com/NVIDIA/SkillSpector/blob/d7338f58200a9ae2a24810cee08911ab68b107a7/src/skillspector/mcp_server.py)。
- [docs/ANALYSIS_RESOURCE_BOUNDS.md](https://github.com/NVIDIA/SkillSpector/blob/d7338f58200a9ae2a24810cee08911ab68b107a7/docs/ANALYSIS_RESOURCE_BOUNDS.md)。
- [LICENSE](https://github.com/NVIDIA/SkillSpector/blob/d7338f58200a9ae2a24810cee08911ab68b107a7/LICENSE)。
- [仓库 API](https://api.github.com/repos/NVIDIA/SkillSpector)、[发行 API](https://api.github.com/repos/NVIDIA/SkillSpector/releases?per_page=1)；动态元数据仅代表本轮采样。
- 事实依据为以上一手材料；价值、风险判断与建议为本库工程分析，未写作实测结论。
