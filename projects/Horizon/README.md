<!-- markdownlint-disable MD013 -->

# Horizon：以 Profile 配置个人新闻采集与双语日报

- 上游：[Thysrael/Horizon](https://github.com/Thysrael/Horizon)；repository ID `1162410458`。
- 更新：2026-11-05（Asia/Shanghai）；分类：RAG、检索与知识处理。
- 固定 main SHA：`d7406f738c711df82b8f060fa1d5e9999d36cca0`；API 12,457 stars / 1,817 forks / 26 open issues（含 PR）；综合 daily +121。
- 根许可 MIT；发行列表为空。本轮为文档 / 配置 / 抽样实现静态核读，未安装、登录采集、调用模型或发布日报。

## 定位

把 RSS、GitHub、Hacker News、Reddit、Telegram、X 等来源汇总为个人日报的 Python 工具。Profile 决定内容适用范围、评分和呈现区块，运行配置决定订阅、阈值、去重与配额；目标是把个人阅读偏好显式化。

## 用法

需要 Python 3.11+ 和所选模型凭据；本地安装后先检查示例信息源，再配置运行：

```sh
git clone https://github.com/Thysrael/Horizon.git
cd Horizon
git checkout d7406f738c711df82b8f060fa1d5e9999d36cca0
uv sync
cp .env.example .env
cp data/config.example.json data/config.json
# 编辑 provider / 密钥环境变量和信息源，先保持邮件与 Webhook 关闭
uv run horizon --hours 24
```

交互配置入口为 `uv run horizon-wizard`；也支持 Docker。`--data-dir` 改变状态、日报与默认配置目录，`--config` 仅改变配置文件位置，二者不能混为一项。日报默认写到 `data/summaries/`。

测试依赖需 `uv sync --extra dev`，金融源 OpenBB、X 的 twitter extra 按需安装；后者还需要 Playwright 浏览器及系统依赖，默认 Dockerfile 不包含这些组件。上游的 GitHub Actions 每日模板当前以 `.disabled` 结尾，须自行配置和启用。

## 原理

- 收集条目后路由到一个 Profile；显式 profile 直接采用，省略或 `auto` 则由 AI 从候选中匹配。
- 分析、评分、筛选与主题去重之后，为选中条目生成摘要、背景、方案等区块，再按 Profile / 类别限额组织日报。
- 可选 Web 搜索补背景，历史 BM25 搜索提供以前日报的最多三个短结果；当前提示词明确历史摘要不是独立验证，日期为日报日期。
- enrichment 要求区分原始事实、社区观点和外部语境，并引用精确工具结果 ID；`url_security.py` 对 HTTP 目标和重定向逐跳做公开地址检查。
- 输出为 Markdown / Pages，也可通过邮件、微信或 Webhook 分发；MCP 是拆分调用采集、分析、生成阶段的另一入口。

## 价值

可用于个人研究雷达和小团队订阅初筛，尤其适合把“新闻看背景、长文看方法”等阅读标准保存为配置。与纯关键词订阅相比，Profile 提供可调整的筛选口径；实际召回、重复率和事实保留仍需对照人工样本。

## 风险边界

- AI 评分、自动分类与合并可能漏掉低热度原始材料，或把相近主题误并；分数不是重要性或真实性的客观指标。
- 提示词中的证据规则与 URL 防护只是局部措施，不证明提示注入、所有采集器、DNS 时序或外部内容均已安全；本轮未做攻击复现。
- 历史日报是模型处理后的派生文本，不能循环引用成第二个独立来源；“社区讨论”须回查实际评论，而不是由模型补全。
- 模型 API、搜索服务、X 登录态、Telegram、邮件与 Webhook 有不同数据出口。自托管采集不代表全文、摘要与订阅者资料都留在本机。
- 示例启用多类公共源，X / 邮件 / Webhook 等另有开关；复制配置后逐项审查抓取范围、费用与接收方，再启用定时发布。
- README 的赞助价格和模型品质属于商业宣传，本页未验证，不作为选型依据。MIT 许可也不授予被采集内容的再分发权。

## 补充建议

从两三个公开 RSS 开始，用固定时间窗和模型保存原始 URL、抓取时间、Profile、评分、合并关系与最终摘要。人工抽查漏报、错并、引用和讨论来源，再扩展采集；自动投递应另验收目的地与敏感信息过滤。

## 参考资料

- [中文 README](https://github.com/Thysrael/Horizon/blob/d7406f738c711df82b8f060fa1d5e9999d36cca0/README_zh.md)、[Python 依赖](https://github.com/Thysrael/Horizon/blob/d7406f738c711df82b8f060fa1d5e9999d36cca0/pyproject.toml)。
- [示例配置](https://github.com/Thysrael/Horizon/blob/d7406f738c711df82b8f060fa1d5e9999d36cca0/data/config.example.json)、[enrichment 证据提示](https://github.com/Thysrael/Horizon/blob/d7406f738c711df82b8f060fa1d5e9999d36cca0/src/ai/prompting/enrichment.py)、[URL 检查](https://github.com/Thysrael/Horizon/blob/d7406f738c711df82b8f060fa1d5e9999d36cca0/src/url_security.py)。
- [安全报告说明](https://github.com/Thysrael/Horizon/blob/d7406f738c711df82b8f060fa1d5e9999d36cca0/SECURITY.md)、[API](https://api.github.com/repos/Thysrael/Horizon)。
