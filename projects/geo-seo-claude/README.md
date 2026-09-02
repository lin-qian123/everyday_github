<!-- markdownlint-disable MD013 MD034 -->

# geo-seo-claude：面向 AI 搜索可见性审计的 Claude Code skill 套件

## 项目概览

- 上游仓库：https://github.com/zubair-trabzada/geo-seo-claude
- GitHub API 快照（2026-09-03）：10,169 stars、1,568 forks、25 个开放 issue
- 当前 release：未发布 GitHub Release；默认分支最近 push 为 2026-09-02
- 主要技术：Claude Code skills / subagents、Python scoring、robots.txt、JSON-LD、Markdown / PDF 报告
- 许可证：MIT

## 定位

geo-seo-claude 将 GEO（Generative Engine Optimization）与传统技术 SEO 审计封装为 Claude Code commands，覆盖引用友好度、AI crawlers、`llms.txt`、品牌提及、平台差异、schema、内容与报告生成。

它适合形成审计清单和候选报告，不是 ChatGPT、Perplexity、Google AI Overviews 等平台排名机制的官方测量工具，也不能证明优化会带来收录、引用或转化。

## 用法

上游提供远程安装脚本和手动 clone；Python 依赖安装到 `~/.claude/skills/geo/.venv/`。安装后可在 Claude Code 中运行 `/geo audit <url>`、`/geo citability <url>`、`/geo crawlers <url>`、`/geo schema <url>` 或生成 Markdown / PDF 报告。

安装脚本会写入用户级 Claude skills / agents 目录。应先下载审查脚本和 skill 内容，固定 commit，并在独立 profile 上试用，不直接修改生产站点或客户仓库。

## 原理

完整审计由多个 subagents 并行检查 AI visibility、平台 readiness、技术 SEO、内容和 schema，再聚合为 0–100 的复合 GEO 分数与行动清单。Python 脚本负责引用友好度评分、crawler / robots 检查、`llms.txt` 生成和 PDF 渲染。

CRM-lite 与月度报告数据保存在 `~/.geo-prospects/`，卸载 skill 时不会自动删除。分数阈值、段落长度和市场数据来自项目方法论，不是搜索平台公布的排名公式。

## 价值

- 将 GEO 与传统 SEO 检查拆成可复用、可读的 skills 和 subagents。
- robots、schema、内容和平台差异可在一份结构化报告中汇总。
- Markdown / PDF 输出适合人工审阅、留档和月度对比。
- 专用 venv 降低 Python 依赖直接污染系统环境的风险。

## 风险边界

- GEO 分数和“citation readiness”是启发式代理指标，不能证明真实平台引用或业务效果。
- README 中市场规模、引用重叠、最佳段落长度和 agency 定价等数字须回到原始研究逐项核验。
- 远程安装脚本会改用户级 agent 配置；skills、subagents 与依赖都属于供应链输入。
- 扫描客户站点、品牌与 prospect 会生成商业敏感数据；`~/.geo-prospects/` 需要单独删除与备份政策。
- 自动生成 `llms.txt`、schema 或内容若未经验证就发布，可能造成错误声明、搜索质量和合规问题。
- 本页依据上游 README 与 API 静态核验，未安装、未跑审计，也未验证分数与外部引用的相关性。

## 补充建议

1. 固定 commit 并人工审查 install / uninstall、skills、subagents 和 Python 依赖后再安装。
2. 用已知结构和已知缺陷的站点 golden set 评估各项检查，不只看复合总分。
3. 对 ChatGPT、Perplexity、Google AIO 等平台使用固定查询、地区、账号和时间窗口保存原始结果。
4. 将生成建议标为诊断、候选修改和已批准发布三种状态；禁止 agent 直接改生产站。
5. 把 `~/.geo-prospects/` 纳入权限、加密、保留期、导出和卸载清理流程。

## 参考资料

- 仓库与 README：https://github.com/zubair-trabzada/geo-seo-claude
- 安装脚本：https://github.com/zubair-trabzada/geo-seo-claude/blob/main/install.sh
- GEO scoring 方法：https://github.com/zubair-trabzada/geo-seo-claude#scoring-methodology
- 数据目录说明：https://github.com/zubair-trabzada/geo-seo-claude#data-storage
- 许可证：https://github.com/zubair-trabzada/geo-seo-claude/blob/main/LICENSE
