<!-- markdownlint-disable MD013 MD034 -->

# Hister：索引浏览历史与本地文件的个人搜索引擎

> 上游仓库：https://github.com/asciimoo/hister · 归类：RAG、检索与知识处理 · 本页基于 2026-09-21 的 README、官方文档、privacy 说明、release 与许可证静态整理；未安装浏览器扩展、导入历史或向远端 embedding endpoint 发送文档。

## 定位

Hister 是自托管个人搜索引擎：保存用户选择的访问页面与本地文件全文，提供 Web、TUI、CLI 和 MCP 查询。它兼顾传统全文检索与可选语义检索，让 AI assistant 能查询“我曾看过什么”，但不把个人浏览史自动等同于可靠知识库。

2026-09-21 的 GitHub 官方 Go Trending 抓取显示约 `+300 stars today`；REST API 快照为 `5,428 stars / 229 forks / 62 open issues`，AGPL-3.0，最新 release 为 `v0.19.0`（9 月 3 日）。

## 用法

下载 release 后可直接启动本地服务，再安装 Firefox / Chrome 扩展：

```sh
chmod +x hister
./hister listen
```

默认入口是 `http://127.0.0.1:4433`。用户可逐步启用新页面保存、浏览历史 / bookmark 导入、本地目录索引或站点 crawler；Homebrew、Docker 和 Nix 也是上游支持的安装路径。

## 原理

- 浏览器扩展把用户选择保存的页面正文发送到配置的 Hister server，并保留可检索 URL / metadata。
- 服务端建立全文 index，支持 field filter、phrase、wildcard、negation、alias 与优先级。
- browser history、bookmark、crawler、本地 directory 和 file import 进入同一检索面。
- Web、terminal 与 MCP client 复用同一服务；多用户模式按用户分离 documents 和 search results。
- semantic search 是可选能力，会把文档文本发送到用户选择的 embedding endpoint；默认无 telemetry 和 mandatory cloud sync。

## 价值

- 比只搜标题 / URL 的浏览器 history 更容易找回实际读过的段落和文件内容。
- 本地全文路径无需第三方向量服务；使用者可以按资料敏感度决定是否启用 semantic search。
- MCP 接口让 Agent 基于个人已见材料检索，减少重复公开搜索和手工复制上下文。
- 单一 Go 服务配合浏览器扩展，部署门槛低于完整企业知识平台。

## 风险边界

- 浏览历史和全文索引能暴露健康、财务、身份、公司内部和私人兴趣；self-hosted 不等于自动安全或最小保留。
- optional embedding 会把正文外发到所选 endpoint；favicon、crawler、下载资源与浏览器扩展也可能产生网络请求。
- 多用户分离是应用能力，不等于已证明的强租户隔离；部署到共享 / 公网服务必须补 TLS、认证、备份和访问审计。
- 历史网页会过时、被误读或含 prompt injection；被索引和被检索不能证明来源真实、当前有效或适合 Agent 执行。
- AGPL-3.0 对网络部署和修改分发有合规义务；本页未验证升级、删除、账户隔离或索引残留。

## 补充建议

1. 从专用本地 profile 和低敏感站点开始，先定义 allowlist / denylist、保留期与删除流程。
2. 默认关闭 semantic endpoint；确需启用时按 document class 过滤，并核对 provider 数据使用和地域条款。
3. 给 MCP 结果附 URL、抓取时间和片段位置，要求 Agent 将“历史内容”与“当前事实”分开。
4. 在共享部署前测试用户间查询、导出、删除、备份恢复、extension compromise 和恶意页面注入。

## 参考资料

- 上游 README：https://github.com/asciimoo/hister
- Quickstart：https://hister.org/docs/quickstart
- Privacy / intro：https://hister.org/docs/intro#privacy
- Configuration：https://hister.org/docs/configuration
- `v0.19.0` release：https://github.com/asciimoo/hister/releases/tag/v0.19.0
- GitHub REST API：https://api.github.com/repos/asciimoo/hister
- LICENSE：https://github.com/asciimoo/hister/blob/master/LICENSE
