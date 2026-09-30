<!-- markdownlint-disable MD013 -->

# OpenKB（VectifyAI/OpenKB）

> 上游仓库：<https://github.com/VectifyAI/OpenKB> · 归类：RAG、检索与知识处理 · 本页基于 2026-10-01 的 GitHub API、README、`pyproject.toml`、示例与发行信息静态整理，未导入真实文档、调用模型或复验检索质量。

- 抓取快照：4,679 stars、491 forks、85 open issues。
- 热度信号：GitHub Python Trending 抓取时约 +46 当日 stars。
- 版本与许可：Apache-2.0；latest Release 为 `v0.4.5`，首个 tag 为 `v0.5.0-rc1`。

## 定位

OpenKB 是一个 CLI 与 Web Workbench，把 PDF、Office、Markdown、网页等原始资料编译成 Markdown wiki、概念页、实体页和交叉链接，再提供 query、chat、知识图和 Skill / slide generator。长 PDF 借助 PageIndex 的树状索引做“无向量库”检索，短文档则转换后交给 LLM 阅读。

## 用法

Python 3.10+ 可用 `pip install openkb` 安装；在知识库目录执行 `openkb init`、`openkb add <文件或 URL>`、`openkb query` 或 `openkb chat`。Web 入口需安装 `openkb[web]` 并启动 `openkb-web`；认证默认关闭，只适合环回地址，若外部暴露必须设置 `OPENKB_API_TOKEN` 和反向代理安全策略。

## 原理

短文档通过 MarkItDown 转 Markdown，长 PDF 由 PageIndex 生成层次树与摘要；LLM 读取新来源以及既有概念 / 实体页，更新 wiki、索引和日志。生成层再从编译后的 wiki 产出带引用回答、会话、Agent Skill、HTML deck 或可视化。模型接入经 LiteLLM，依赖文件对 PageIndex、MarkItDown、LiteLLM 等采用精确版本固定。

## 价值

它把“一次查询临时拼上下文”变成可审阅、可版本化的知识资产，Markdown / Obsidian 兼容也便于人工修订和 Git 审查。对长报告、论文集或内部手册，概念页与交叉链接能减少重复整理；Skill Factory 则提供从知识库到可分发 Agent 资产的明确出口。

## 风险边界

- wiki、概念合并、冲突标记与引用仍由模型生成；结构化、带链接不等于事实正确或来源覆盖完整。
- `recompile` 会重写概念页，手工修改可能被覆盖；删除、回滚与来源撤回应在版本控制副本中验证。
- “local”只描述本地程序和默认 PageIndex 路径；LLM provider、URL 抓取与可选 PageIndex Cloud 仍可能外发文档、图片或查询。
- Web UI 默认无认证；错误绑定到公网可能暴露整套知识库和生成入口。
- Skill / deck 输出会继承资料中的错误、敏感信息、提示注入和版权限制，不能因“编译”而自动安全或可再分发。
- 本轮未复跑检索 benchmark，也未验证多模态、长文档扩展性或 LiteLLM 固定版本的完整供应链安全。

## 补充建议

先在脱敏小型语料库固定 commit、模型、prompt 和预期问答集，比较原文、wiki 页与回答引用；将 `raw/`、生成 wiki 和配置分层备份。默认只绑定 `127.0.0.1`，外部服务再加 token、TLS、网络 allowlist 与审计。对 Skill / slide 导出增加敏感信息扫描、来源许可检查和人工事实复核。

## 参考资料

- [GitHub 仓库](https://github.com/VectifyAI/OpenKB)
- [GitHub REST API](https://api.github.com/repos/VectifyAI/OpenKB)
- [README](https://github.com/VectifyAI/OpenKB/blob/main/README.md)
- [项目配置与固定依赖](https://github.com/VectifyAI/OpenKB/blob/main/pyproject.toml)
- [REST API / Workbench 示例](https://github.com/VectifyAI/OpenKB/blob/main/examples/rest-api/README.md)
- [v0.4.5 Release](https://github.com/VectifyAI/OpenKB/releases/tag/v0.4.5)
- [LICENSE](https://github.com/VectifyAI/OpenKB/blob/main/LICENSE)
