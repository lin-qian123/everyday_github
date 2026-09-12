<!-- markdownlint-disable MD013 -->

# hyperresearch（jordan-gibbs/hyperresearch）中文解读

> 证据快照：2026-09-13（Asia/Shanghai）。GitHub REST API 显示 3,019 stars、286 forks、11 open issues，最新 release 为 `v0.11.1`，MIT。本文未安装 Claude Code skills、启动多 agent 调研或复现上游 leaderboard 结果。

## 定位

hyperresearch 是把 Claude Code 组织成深度研究 agent 的 harness：从问题规范化、宽度搜索、引用追踪、证据缺口、三路草稿、反方审查、引文核对到最终润色，形成最长 16 步的可恢复流水线。

它同时维护一个 Markdown 为真值、SQLite 为可重建索引的长期研究 vault。网页、PDF、学术元数据、开放获取替代版本与 provenance 被保存下来，供后续运行全文或可选语义检索。

## 用法

上游的项目级安装路径为：

```bash
pip install hyperresearch
hyperresearch install
```

然后在 Claude Code 中调用 `/hyperresearch <问题>`。开始前应先选择 fast/full/premier/dissertation 等规模，设置来源时间窗、费用与并发预算，并用一项边界明确、可人工检查的问题验证生成的 `research/runs/` 和 `research/notes/`。

## 原理

- entry skill 固化原始研究问题，再按阶段加载独立 step skill，降低长上下文中静默漏步骤的风险。
- fetcher、source/loci analyst、draft orchestrator、synthesizer、多个 critic、patcher 和 cite-checker 承担不同角色；模型选择来自 profile 配置。
- crawl、学术聚合、引用追踪和 gap-fill 扩充语料；OpenAlex、Crossref、CORE、DOAB、ClinicalTrials.gov、SEC EDGAR、FRED 等结果按 DOI/标题去重。
- 每份来源保存 Markdown/YAML frontmatter，原始 PDF 可保存在 `research/raw/`；SQLite 只作搜索缓存，可由 Markdown 重建。
- 对付费墙或阻断页面，系统可尝试 Unpaywall、Europe PMC 等合法开放版本，并显式标记 substituted/rescued 与版本类型。

## 价值

- 把研究问题、来源、引用链、草稿、批评和修补保存在可检查目录中，比一次性聊天更利于复盘。
- 区分转载与独立来源、主动寻找反证、逐句检查引用，方向上有助于减少“多链接等于多证据”的错觉。
- Markdown 真值便于 Git 版本控制、人工编辑与工具退出后的长期可读性。
- 多档规模让快速事实核对与长篇调研共用一套 provenance 结构，而不必总是启动最大流水线。

## 风险边界

- README 所称领先 DeepResearch-Bench 的图是内部 stratified pilot 的前瞻投影，并明确等待第三方验证；不能写成已获公开 leaderboard 认证。
- 250+ 来源、300–450 来源或 4–8 小时运行意味着显著 token、API、浏览器和人工审阅成本；来源多不自动提高结论质量。
- cite-checker、critic 与多模型互审仍可能共享偏见、遗漏关键来源或错误理解证据，不能替代领域专家。
- 浏览器升级通道会使用真实 Chrome；登录态、下载、付费内容、robots/条款与 prompt injection 需要独立治理。
- 开放获取替代版本可能是 submitted/accepted manuscript，不等同于 version of record；引用关键表述需回查版本。
- 持久 vault 会长期保留抓取文本、元数据和研究兴趣，必须设计敏感数据、版权、删除和共享边界。

## 补充建议

1. 先用 fast 路径处理一个有已知答案的问题，核对每个 citation 是否支持所在句，而不是只看链接存在。
2. 为预算、并发、最大来源数、浏览器登录态和可访问域名设置硬上限；默认关闭真实账号升级通道。
3. 对每次运行保存 query、profile、模型、版本、来源清单和未解决缺口；不同版本稿件必须显式区分。
4. 将最终报告标为 agent 草稿，交由领域专家检查论证、数据口径、撤稿、版本和版权。

## 参考资料

- GitHub：<https://github.com/jordan-gibbs/hyperresearch>
- GitHub REST API：<https://api.github.com/repos/jordan-gibbs/hyperresearch>
- Releases：<https://github.com/jordan-gibbs/hyperresearch/releases>
- PyPI：<https://pypi.org/project/hyperresearch/>
- DeepResearch-Bench Leaderboard：<https://huggingface.co/spaces/muset-ai/DeepResearch-Bench-Leaderboard>
- LICENSE：<https://github.com/jordan-gibbs/hyperresearch/blob/main/LICENSE>
