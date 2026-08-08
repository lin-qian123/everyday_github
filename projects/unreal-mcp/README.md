<!-- markdownlint-disable MD013 -->

# unreal-mcp

- 仓库：[ZiggyMar/unreal-mcp](https://github.com/ZiggyMar/unreal-mcp)
- 快照：2026-08-09 抓取；GitHub API 显示其创建于 2026-08-08，约 23 stars、0 forks，MIT。数字会随时间变化。
- 分类：Agent 框架与技能生态

## 定位

面向 Unreal Engine 5.6/5.8 的本地 MCP Server。它让 MCP client 读取、搜索和编辑 Blueprint，重点是用分级摘要、增量索引和 diff 编辑避免把冗长的引擎 JSON 直接塞进模型上下文。

## 用法

需要 Node.js 18+ 与 UE 5.6/5.8 项目。按 README 将 `UnrealMCPBridge` 放到项目 `Plugins/`，在 `mcp-server` 执行 `npm install && npm run build`，再把生成的 `dist/index.js` 注册到 MCP client；打开 Unreal Editor 后先以 `unreal_ping` 验证本地连接。

## 原理

C++ Editor plugin 通过 Unreal 的 Kismet2、EdGraph 与 AssetRegistry API 暴露本地 TCP bridge；Node/TypeScript MCP server 将工具调用转换为 bridge 请求。项目将 Blueprint、函数、变量和跨资产引用建为持久索引，由 AssetRegistry 增量更新；读取先给小型摘要，写操作以 node ID 与差异为单位并置于可撤销 transaction。

## 价值

大型 Blueprint 工程常因序列化体积而难以供 agent 理解。若索引和引用关系正确，该项目可降低重复扫描与上下文成本，并让 agent 在既有工程中定位影响范围、进行可回滚的小步修改。

## 风险边界

它直接操作编辑器资产；即使写入带 Undo，也可能生成错误图、编译失败或污染版本控制。兼容性只覆盖 README 所称的 UE 5.6/5.8；其“已 live 验证”的范围是作者报告，不能推及你的插件、蓝图规模或团队流程。不要把本地 TCP 接口暴露到不可信网络。

## 补充建议

在副本项目和独立 Git 分支上先只启用读取工具，核对索引结果与编辑器实际内容。随后用小蓝图演练“创建—编译—保存—撤销”，把每次写入都纳入源码控制和人工 code review；限制 MCP host 的监听地址、插件来源和 agent 文件权限。

## 参考资料

- [项目 README](https://github.com/ZiggyMar/unreal-mcp)
- [架构说明](https://github.com/ZiggyMar/unreal-mcp/blob/main/ARCHITECTURE.md)
- [GitHub API 元数据快照](https://api.github.com/repos/ZiggyMar/unreal-mcp)
