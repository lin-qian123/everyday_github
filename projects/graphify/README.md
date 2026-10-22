<!-- markdownlint-disable MD013 -->

# graphify

- 主上游：[Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify)
- 分类：RAG、检索与知识处理。
- 核验日期：2026-10-23（Asia/Shanghai）；主线快照 `c588b72d9369`。
- [API](https://api.github.com/repos/Graphify-Labs/graphify) 快照：132,892 stars / 12,717 forks / 1,601 open issues；发行列表首项 [v0.9.94](https://github.com/Graphify-Labs/graphify/releases/tag/v0.9.94)（UTC 2026-10-22，正式）。累计值不代表今日增量。

## 定位

Graphify 将代码与相关文档转为可查询知识图谱，供编码助手按节点、路径和证据理解工程。本轮更新既有页面，主上游为 Graphify-Labs/graphify；旧 safishamsi 地址的 API 迁移目标与新地址 repository ID 同为 `1200597263`，属于同一仓库，不计新增。[当前仓库](https://github.com/Graphify-Labs/graphify)、[旧 API](https://api.github.com/repos/safishamsi/graphify)

## 用法

官方 PyPI 包名是双 y 的 `graphifyy`，CLI 仍叫 `graphify`。当前默认分支为 `v8`，正式发行和 manifest 为 0.9.94，Python 下限 3.10。示例：

```bash
uv tool install graphifyy==0.9.94
graphify install --platform codex --project
```

安装集成会写入项目技能 / 指令文件，运行前审查改动；Codex 会话使用 `$graphify`，其他助手的调用语法见 README。先选择公开小仓库、限制扫描范围，完成图谱构建后再使用 `graphify query`、`path`、`explain`。[用法与发行差异](https://github.com/Graphify-Labs/graphify/blob/c588b72d936927790a87ad009955078ed40562a3/README.md)、[manifest](https://github.com/Graphify-Labs/graphify/blob/c588b72d936927790a87ad009955078ed40562a3/pyproject.toml)

## 原理

代码通过 tree-sitter 等本地解析抽取结构关系；文档、PDF、图片可走可选模型语义抽取，音视频可先本地转写，再融合图结构与社区划分。查询可返回关系路径与证据，仍应区分直接抽取和语义推断。代码图不是运行时动态依赖与业务因果的完整证明。

## 价值

适合跨模块理解、找影响面与减少重复读取。README 的 Recall@10、零 LLM credits 或 Cloud 节省 token 宣传各自有实验范围；本轮未复现实验，不能把单项检索指标或宣传比例推广到全部 Agent 任务。

## 风险边界

- AST 代码抽取与语义资料抽取的数据流不同。README 说明混合资料可送至助手 / 配置模型；自动检测 provider 可能由环境中的 key 决定。需固定 backend；禁用模型用 `GRAPHIFY_BACKEND=none`，代码扫描范围用 `--code-only`。[隐私说明](https://github.com/Graphify-Labs/graphify/blob/c588b72d936927790a87ad009955078ed40562a3/README.md)
- “无遥测”不代表没有本地记录：query / path / explain 和 MCP query 默认写 `~/.cache/graphify-queries.log`；可用 `GRAPHIFY_QUERY_LOG_DISABLE=1` 关闭。日志有问题文本等字段，默认不保存完整子图响应。
- 本地 CLI skill 安装与 MCP 连接是两条不同接入方式；安装 skill 不会自动建立 MCP。HTTP MCP 为可选网络监听，SSRF / 路径防护属于上游安全设计，本轮未做攻击验证。[安全模型](https://github.com/Graphify-Labs/graphify/blob/c588b72d936927790a87ad009955078ed40562a3/SECURITY.md)
- Graphify Cloud 有跨库、持续记忆与连接器等另外的数据边界；本页开源快照采用 Apache-2.0，不能据此推断 Cloud 服务条款。[LICENSE](https://github.com/Graphify-Labs/graphify/blob/c588b72d936927790a87ad009955078ed40562a3/LICENSE)

## 补充建议

先做禁用 LLM 的公开代码图，抽查已知 import / call 链的误报漏报；需要语义资料时再测 provider 与来源引用。将 skill / hook 写入文件、日志位置和模型数据出口纳入项目配置记录。原 2026-04 页面已在原路径更新，历史说明由 Git 保留。本轮未安装、构建图谱或连接 Cloud。

## 参考资料

- [README.md](https://github.com/Graphify-Labs/graphify/blob/c588b72d936927790a87ad009955078ed40562a3/README.md)（固定 commit）。
- [SECURITY.md](https://github.com/Graphify-Labs/graphify/blob/c588b72d936927790a87ad009955078ed40562a3/SECURITY.md)（固定 commit）。
- [pyproject.toml](https://github.com/Graphify-Labs/graphify/blob/c588b72d936927790a87ad009955078ed40562a3/pyproject.toml)（固定 commit）。
- [LICENSE](https://github.com/Graphify-Labs/graphify/blob/c588b72d936927790a87ad009955078ed40562a3/LICENSE)（固定 commit）。
- [正式发行列表](https://github.com/Graphify-Labs/graphify/releases)、[仓库 API](https://api.github.com/repos/Graphify-Labs/graphify)（动态状态）。
