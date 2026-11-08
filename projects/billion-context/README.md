<!-- markdownlint-disable MD013 -->

# billion-context（ranxianglei/billion-context）中文解读

> 上游：[ranxianglei/billion-context](https://github.com/ranxianglei/billion-context) · 分类：Coding Agents 与终端助手 · 核验：2026-11-09，仓库 ID 1324949198，主线 SHA `848f59b9963f293b8beac5b95bb861a7dcf25a0c`。本页为文档与抽样源码静态核读，未安装运行、登录或调用模型 / 云资源。

## 定位

面向 coding agents 的上下文压缩代理、原生插件与 launcher，在模型请求中提供增量摘要、按需恢复、关键词搜索和上下文状态。由原 2026-10-13 页面原位更新到 v0.1.213 / 当前主线；它不扩大模型的物理 context window，“月级会话 / 省 5 倍 token”仍是条件性的作者目标或宣传。

## 用法

官方支持 npm 包与 `bili <client>` launcher、`bili plugin install <client>` 或 `/bili/` base URL 路由；应固定 `billion-context@0.1.213` 和宿主版本，用测试会话先核安装写入、代理命中和恢复。

**不同宿主不能套同一流程**：当前 README 说明 Codex 插件仅安装 MCP 工具伴随进程，既不自动启动代理，也不自动改路由；完整接入需启动代理并配置路由，或使用相应 launcher。pi / OpenCode 等原生插件与旧 standalone 扩展互斥，安装器备份为 `.bili-bak`，项目内旧扩展可能仍需人工移除。这里记录第三方接入说明，本轮没有修改任何客户端配置。

## 原理

代理解析上游协议并关联 session / 分支，把已消费消息范围折叠成摘要；`decompress` 可恢复保存的原消息，`search_context` 检索摘要与可见消息，`acp_status` 显示状态。恢复能力依赖原始持久数据仍在，摘要本身并非信息论无损。

原生模式、URL rewrite、证书 MITM 的接入 seam 不同；session 身份、并发子任务和 prefix cache 都需要宿主适配。当前配置支持 SQLite / MySQL 状态和独立日志；升级磁盘包与重启已注入的宿主是两个步骤。

## 价值

把长会话压缩策略、范围和 cache 使用暴露给开发者观察，适合在固定任务上研究信息丢失、恢复率、延迟和总成本。多宿主支持有利于比较，但不保证所有宿主版本功能对等。

## 风险边界

- 代理可见模型请求、响应和凭据相关流量；部分 launcher 需要证书 MITM 和本地 CA。默认 loopback，开放 LAN 的代理仍无认证，应核入口和网络隔离；管理端点的 loopback 限制不能代替模型入口认证。
- 当前 README 明确记录 Claude Desktop Code tab 覆盖 base URL、绕过代理但可能禁用 native compact 的组合问题；CLI 经自定义 base URL 也可能失去账户绑定能力。均是作者报告的版本相关限制，不能推断本机是否受影响。
- 默认 autoUpdate 开；关键 advisory watcher 独立于它，关闭前者后仍可能按 advisory 安装修复 / 回滚版本，需另外核 `BILI_ADVISORY_CHECK`。远端公告与 release-notes 检查又是不同流量。
- README 仍写 Early、mock 测试和后续真实模型集成里程碑；不能据发行数量或 mock 通过认定真实模型、并行 session、缓存与成本已全面验证。
- 日志、持久 session / 原消息和数据库包含上下文；`ACP_LOG_FILE=off` 只关闭日志文件，不等于清除所有状态或 stderr。
- 根 LICENSE 仍是 MIT 加产品表面署名附加条款，API 为 NOASSERTION；不能简写成无附加要求的标准 MIT。

## 补充建议

比较原始链路与压缩链路的任务成功率、遗漏 / 错引、原文恢复、TTFT、cache hit、所有模型调用和账单总额。用明确 session ID 测并发、fork 与宿主重启；检查代理确实命中。正式接入前审 CA、状态备份、日志保留以及 auto-update / advisory 的独立开关，按目标宿主发行重新验收。

## 参考资料

- [上游](https://github.com/ranxianglei/billion-context)、[仓库 API](https://api.github.com/repos/ranxianglei/billion-context)、[v0.1.213](https://github.com/ranxianglei/billion-context/releases/tag/v0.1.213)。
- [README 与已知宿主边界](https://github.com/ranxianglei/billion-context/blob/848f59b9963f293b8beac5b95bb861a7dcf25a0c/README.md)、[版本](https://github.com/ranxianglei/billion-context/blob/848f59b9963f293b8beac5b95bb861a7dcf25a0c/package.json)、[clients](https://github.com/ranxianglei/billion-context/blob/848f59b9963f293b8beac5b95bb861a7dcf25a0c/docs/clients.md)、[配置 / 更新 / 状态](https://github.com/ranxianglei/billion-context/blob/848f59b9963f293b8beac5b95bb861a7dcf25a0c/docs/configuration.md)、[LICENSE 附加条款](https://github.com/ranxianglei/billion-context/blob/848f59b9963f293b8beac5b95bb861a7dcf25a0c/LICENSE)。
- 原根目录 [CONFIGURATION.md](https://github.com/ranxianglei/billion-context/blob/848f59b9963f293b8beac5b95bb861a7dcf25a0c/CONFIGURATION.md) 已为迁移提示，正文在 docs/configuration.md，旧页引用已同步修正。
