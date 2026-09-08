<!-- markdownlint-disable MD013 MD034 -->

# feynman（advaitpaliwal/feynman）

> 记录日期：2026-09-09（Asia/Shanghai）。本页依据上游 README、docs、release、LICENSE、GitHub REST API 与公开 YouTube 项目视频做静态整理；本轮未安装 CLI、未检索论文、未审计代码、未运行复现实验或连接 GPU / cloud provider。

## 定位

`feynman` 是面向科研工作的开源 AI research agent 与本地 workbench。它提供 paper access、literature review、citation / method / reproducibility 排名、paper-vs-code audit、replication planning、training recipe、watch、draft 与多 agent deep research，并连接 alphaXiv、OpenAlex、arXiv、Europe PMC、Hugging Face 及大量生命科学数据源。

2026-09-09 的 GitHub 官方 TypeScript Trending 抓取显示约 `+268 stars today`；REST API 快照为 `9,233 stars / 1,053 forks / 6 open issues`，MIT；最新 GitHub release 为 `v0.3.48`（2026-09-06）。默认分支 `package.json` 已是 `0.3.49`，说明 main 与最新 release 并非同一快照，复现实验应锁定具体版本。

## 用法

上游提供原生 installer 和 npm 两条路径：

```bash
curl -fsSL https://feynman.is/install | bash -s -- 0.3.48
# 或
npm install -g @advaitpaliwal/feynman@0.3.48
```

安装后可用 `feynman rank <topic>`、`feynman paper <id>`、`feynman deepresearch <topic>`、`feynman lit <topic-or-lab>`、`feynman audit <paper>`、`feynman replicate <claim>` 与 `feynman serve`。上游也提供 skills-only 安装；因 installer 会下载运行时和资源，生产研究环境应先审阅脚本、校验 release 与 SHA-256，再在隔离 profile 中试用。

## 原理

- **Pi runtime**：以 Pi agent runtime、package / extension / skill 模型承载研究工作流和工具。
- **研究分解**：Researcher、Reviewer、Writer、Verifier 四类 agent 分担检索、内部批评、写作和引用 / URL 验证。
- **多源论文链**：按 DOI、arXiv、OpenAlex、PMID/PMCID 或标题解析论文，组织 citation graph、开放获取候选与 full text。
- **证据型排序**：PaperRank 综合 citation、method、reproducibility 与 provenance；可扩展引用、补 full text、critique 和 synthesis。
- **本地 workbench**：项目、session、artifact、lineage、provenance、compute、connector、credential state 等记录存入用户目录下的本地状态。
- **显式 execution choice**：`replicate` 先规划，按 README 只在用户选择 Docker、Modal、RunPod 等环境后执行。

## 价值

- 把论文发现、全文访问、证据排序、代码审计和复现计划放进一条可续接科研工作流。
- 引用、来源、artifact lineage 与 verification 入口有助于把研究输出从聊天文本沉淀成可追溯资产。
- 同时覆盖通用 ML 与大量生命科学数据库，适合复杂跨源检索和候选筛选。
- Skills-only、CLI 与 workbench 三种形态便于按权限和使用深度分阶段采用。

## 风险边界

- “source-grounded”不等于事实正确：检索覆盖、全文版本、引用语境、元数据映射、模型摘要和结论综合都可能出错。
- PaperRank 是阅读优先级工具，不是论文质量、可复现性或科学真假的客观排名；citation count 还受领域和时间偏差影响。
- `replicate`、`autoresearch` 与 remote compute 可能下载代码 / 数据、执行不可信依赖并产生 GPU 费用；计划和日志不是成功复现证据。
- Workbench、论文全文、研究假设、API key、SSH/BYOC、cloud bucket 和 session state 可能包含未公开研究或受限数据。
- 一行 installer、skills installer 与 package update 都是供应链入口；main `0.3.49` 与最新 release `v0.3.48` 需要明确区分。
- 第三方 YouTube 视频可说明传播存在，但其功能描述、安装安全与“replicate”叙事不是本仓库独立验收。

## 补充建议

- 用 10–20 篇熟悉论文建立 benchmark：逐项检查元数据、合法全文、引用是否支撑、claim-code 对齐、版本与 negative result。
- 将“找到来源、下载全文、运行代码、复现实验、支持结论”设为不同状态，禁止自动升级证据等级。
- 在容器和假凭据中固定 release，先验证 installer diff、网络出口、artifact 删除、失败恢复与 cloud cost ceiling。
- 对敏感或未发表研究建立 project-level access、加密、retention、export 与删除测试，并人工审阅最终 synthesis。

## 参考资料

- GitHub 仓库：https://github.com/advaitpaliwal/feynman
- GitHub REST API：https://api.github.com/repos/advaitpaliwal/feynman
- 官方文档：https://feynman.is/docs
- `v0.3.48` release：https://github.com/advaitpaliwal/feynman/releases/tag/v0.3.48
- Release notes：https://github.com/advaitpaliwal/feynman/blob/main/RELEASES.md
- LICENSE：https://github.com/advaitpaliwal/feynman/blob/main/LICENSE
- 第三方 YouTube 项目视频：https://www.youtube.com/watch?v=EAk4hAuFTqs
