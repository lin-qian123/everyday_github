# Fuxi

- 仓库：[fuxicodex/Fuxi](https://github.com/fuxicodex/Fuxi)
- 快照：2026-08-05 抓取；GitHub API 显示其创建于 2026-08-04，约 81 stars、7 forks，Apache-2.0。数字会随时间变化。
- 分类：Coding Agents 与终端助手

## 定位

Go 编写的单二进制终端 AI 开发助手，聚合多家模型提供方、文件与 shell 工具、MCP、后台任务和子 agent，并提供会话持久化与模型路由。

## 用法

可按 README 的 bootstrap 脚本安装，或从源码以 Go 构建；随后运行 `fuxi --version` 与 `fuxi doctor` 检查环境。配置 provider 前先阅读配置、费用、数据发送和自动更新行为，初次仅在非敏感仓库使用只读/预览任务。

## 原理

TUI 将请求交给可配置的模型层，并按快速、主力、推理等角色选择模型；故障时可切换 provider。工具层统一文件编辑、命令、搜索、LSP、MCP 与会话 checkpoint，持久 transcript 负责恢复上下文。

## 价值

对需要在同一终端调度多 provider、保留长会话和接入 MCP 的开发者，提供了较完整的本地入口。静态二进制和健康检查降低了部署摩擦，但不替代对每个 provider 的合规审查。

## 风险边界

安装脚本、自动更新、shell、浏览器/MCP 和多 provider API 都可能引入供应链、费用、数据外传与越权执行风险。仓库的“安全分类”和 checksum 声明应以实际版本、发布签名和网络行为另行核验。

## 补充建议

固定版本和校验和后再部署；将 API key 放入受控凭据存储，按仓库/环境分隔配置。为工具调用启用人工确认、命令 allow-list 和成本上限，并定期导出或清理敏感 transcript。

## 参考资料

- [项目 README](https://github.com/fuxicodex/Fuxi)
- [项目主页](https://www.fuxicode.com)
- [GitHub API 元数据快照](https://api.github.com/repos/fuxicodex/Fuxi)
