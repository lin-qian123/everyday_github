<!-- markdownlint-disable MD013 -->

# marketingskills（coreyhaines31/marketingskills）

> 记录日期：2026-09-07（Asia/Shanghai）。本页依据上游 README、skills 目录、release、伙伴披露、LICENSE 与 GitHub REST API 做静态整理；本轮未安装这些 skills，也未用真实营销账户验证转化、SEO、归因或广告效果。

## 定位

`marketingskills` 是面向 Claude Code、OpenAI Codex、Cursor、Windsurf 等 AI agents 的营销技能库，把产品营销作为共享上下文，再组织 CRO、文案、SEO/AEO、广告、分析、留存、定价、销售与 RevOps 等工作流。

2026-09-07 的 GitHub 官方综合 Trending 抓取显示约 `+355 stars today`；REST API 快照为 `47,481 stars / 7,384 forks / 106 open issues`，最新 release 为 `v2.11.1`，许可证为 MIT。

## 用法

上游推荐用兼容 Agent Skills 规范的 CLI 安装，可先列出技能或只安装所需子集：

```bash
npx skills add coreyhaines31/marketingskills --list
npx skills add coreyhaines31/marketingskills --skill cro copywriting
```

CLI 会根据宿主写入 `.agents/skills/` 或宿主专用目录。正式接入前应在测试仓库记录安装前后 diff，并逐个阅读准备启用的 `SKILL.md`、引用资料和工具集成。

## 原理

- **共享产品上下文**：其他技能先读取 `product-marketing`，尽量复用受众、定位、差异化与证据，而不是每次重新猜测。
- **按任务触发的技能文件**：每个目录通过触发描述、工作流、检查表和引用资料指导 agent 完成一种营销任务。
- **跨技能引用**：例如文案、CRO 与 A/B test，SEO audit、schema 与 AI SEO 彼此连接，形成可组合路径。
- **跨宿主分发**：兼容通用 `.agents/skills/`，也提供 Claude Code plugin、clone/copy、submodule 和 SkillKit 路径。
- **版本化发布**：release 与迁移说明记录 skill 重命名、上下文文件位置和内容更新。
- **伙伴披露**：仓库单独维护伙伴 registry 与规则，并在 README 显示赞助工具；这提高透明度，但不构成中立性或效果证明。

## 价值

- 把零散营销提示词转成可版本化、可审阅、可按任务启用的工程资产。
- 产品定位先行可以减少不同营销产物之间的口径漂移。
- 覆盖从研究、写作到测量、实验和留存的较完整链路，适合建立团队模板。
- MIT 许可与多种安装路径降低试用门槛，但第三方数据、平台规则和生成内容权利仍需分别审查。

## 风险边界

- Skill 是流程指导，不是市场事实、法律意见或转化效果保证；竞品、关键词、受众和渠道数据必须回到当日来源。
- 冷邮件、广告、tracking、截图、客户研究和 CRM 操作可能涉及隐私、反垃圾邮件、平台政策与外部副作用，不能让 agent 无审批直接发布或投放。
- SEO/AEO 建议会随搜索引擎和生成式搜索产品变化；仓库更新不能保证所有规则当前仍有效。
- 伙伴集成虽有披露，仍可能改变工具选择和数据流；采用前应检查 registry、价格、权限、数据保留与替代方案。
- 全量安装扩大 prompt 与供应链表面；自动更新后应复查新文件、脚本、外链和触发条件。
- AI 生成文案可能出现事实错误、品牌声线漂移、暗黑模式、歧视或知识产权问题，最终发布须由负责人审核。

## 补充建议

- 只安装当前任务需要的技能，固定 release/commit，并把本地定制与上游更新分开管理。
- 为 `product-marketing` 建事实来源、更新时间和负责人字段；未经证据支持的定位只标为假设。
- 对文案/CRO 使用预注册指标与真实实验，不把 agent 的启发式评分当成转化结果。
- 对任何写入广告平台、CRM、analytics 或邮件系统的工具设置只读优先、金额/受众限制与人工审批。
- 每次升级检查伙伴列表、数据外发、技能触发和安装目录 diff，再合并到主力工作区。

## 参考资料

- [GitHub 仓库](https://github.com/coreyhaines31/marketingskills)
- [GitHub REST API](https://api.github.com/repos/coreyhaines31/marketingskills)
- [v2.11.1 Release](https://github.com/coreyhaines31/marketingskills/releases/tag/v2.11.1)
- [Skills 目录](https://github.com/coreyhaines31/marketingskills/tree/main/skills)
- [伙伴规则](https://github.com/coreyhaines31/marketingskills/blob/main/tools/PARTNERS.md)
- [MIT License](https://github.com/coreyhaines31/marketingskills/blob/main/LICENSE)
