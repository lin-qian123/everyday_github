<!-- markdownlint-disable MD013 -->

# Open Ontologies（fabio-rovai/open-ontologies）

> 上游仓库：<https://github.com/fabio-rovai/open-ontologies> · 归类：RAG、检索与知识处理 · 本页基于 2026-10-08 的 GitHub API、README、architecture / assurance / checker 文档与源码静态整理，未把任何本体变更应用到生产图谱，也未独立重跑 Lean / Isabelle 证明链。

- 抓取快照：912 stars、117 forks、19 open issues。
- 热度信号：GitHub Rust Trending 抓取时约 +110 当日 stars；最后 push 为 2026-10-01。
- 版本与许可：最新 Release / tag `v2.0.1`，MIT；本页固定审计 commit `9b2dfc24ebeb`。

## 定位

Open Ontologies 是一个单二进制语义变更与审计引擎：在本体进入生产前计算语义 diff、blast radius、保守扩展、推理后果和风险，并生成可由独立 checker 重验的 certificate。它不是可视化 ontology editor，也不把所有 reasoner 结论都包装成“已证明”。

## 用法

先在临时目录以 persistent storage 加载一份小型 RDF / OWL fixture，运行 `plan`、`reason --certificate` 与 `oo-cert`，再故意篡改 derivation 验证 checker 会 exit 1。生产流程应固定输入哈希、rule table、profile、engine / Lean 版本，在 `plan` 和 `apply` 之间加入人工审查，并预演 version / rollback。

## 原理

Rust engine 用 Oxigraph / SQLite 管理 triple、lineage、version、lint 与 embedding，支持 RDFS、OWL-RL、SHACL、SWRL / RIF / Horn、SPARQL 与多格式 ingest。前向推理可输出“结论—规则—前提”证书，由 core Lean 4 checker 在不共享 engine 代码的情况下重算；用户规则会得到不同 verdict，未被 checker 覆盖的 DL / unsat 结果只保留为 engine 或外部 prover opinion。

## 价值

它补足文本 diff 看不到的语义后果：一条 domain / range 变化可能给大量实例新增类型，而文件行数几乎不变。证书、拒绝伪造样例、assumption 标签和离线复核让审核人能区分“测量”“外部 prover 意见”“在内建规则下可证明”和“在用户规则下成立”。

## 风险边界

- Certificate 只证明 checker 覆盖的规则与给定 asserted graph 下的 entailment，不证明输入事实真实、规则业务正确、本体完整或生产变更安全。
- OWL-DL tableaux、SHACL 测量、外部 prover 与部分 contradiction 路径并非都带同等级证书；上游明确某些 unsatisfiability 回答没有保证。
- MCP / REST 暴露 load、clear、update、apply、rollback、remote SPARQL 和数据库 ingest；未经认证与最小权限部署会直接影响知识资产。
- `plan` 与 `apply` 之间的源数据、imports、远端 endpoint 或 policy 漂移会让已审计划失效，必须以 digest / lock 重验。
- blast radius 和 risk score 是实现定义的指标，不等于业务影响、监管合规或不会丢失关键 entailment。
- 作者展示的 benchmark、proof count 与跨 reasoner 结果未在本轮复测，不能外推到任意大本体、所有 OWL 语义或实时 SLA。

## 补充建议

把“输入真实性、规则审批、engine 输出、certificate 验证、业务验收”分成五个 gate；CI 用独立 runner 构建 checker，并对篡改前提、篡改规则、imports 漂移和 rollback 做负测试。生产 apply 只允许专用服务账号写入，且先保存可恢复快照与 lineage artifact。

## 参考资料

- [GitHub 仓库](https://github.com/fabio-rovai/open-ontologies)
- [GitHub REST API](https://api.github.com/repos/fabio-rovai/open-ontologies)
- [中文 README](https://github.com/fabio-rovai/open-ontologies/blob/main/README.zh-CN.md)
- [架构说明](https://github.com/fabio-rovai/open-ontologies/blob/main/docs/architecture.md)
- [Assurance architecture](https://github.com/fabio-rovai/open-ontologies/blob/main/docs/assurance-architecture.md)
- [Independent rechecking](https://github.com/fabio-rovai/open-ontologies/blob/main/docs/independent-rechecking.md)
- [Trusted computing base](https://github.com/fabio-rovai/open-ontologies/blob/main/docs/trusted-computing-base.md)
- [v2.0.1 Release](https://github.com/fabio-rovai/open-ontologies/releases/tag/v2.0.1)
