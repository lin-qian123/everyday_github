<!-- markdownlint-disable MD013 -->

# GitHub Copilot CLI

> 更新：2026-10-21（Asia/Shanghai）。分类：Coding Agents 与终端助手。上游 `github/copilot-cli`；快照 `c66d206a3b37`（main）。本文为官方资料与源码静态研究；热度、发行时间及社媒限制见[当日日报](../../daily/2026-10-21/ai-hotspots.md)。

## 定位

GitHub 官方终端 Agent，可用自然语言理解、编辑和调试代码，并借助 GitHub 集成处理仓库、issue 和 PR。公开仓库主要提供文档、反馈与发行入口，不应直接称 CLI 本体为采用宽松许可的开源软件。[README.md](https://github.com/github/copilot-cli/blob/c66d206a3b37d29ec082d4d42e8f4b99a0839c25/README.md) [LICENSE.md](https://github.com/github/copilot-cli/blob/c66d206a3b37d29ec082d4d42e8f4b99a0839c25/LICENSE.md)

## 用法

上游列出 Linux、macOS、Windows；npm 安装入口为 `@github/copilot`，启动命令 `copilot`，按提示登录。订阅资格、组织策略与当前额度以官方页面为准；PAT 接入需匹配 Copilot Requests 权限。[README.md](https://github.com/github/copilot-cli/blob/c66d206a3b37d29ec082d4d42e8f4b99a0839c25/README.md)

先在可丢弃目录用只读问题试用，再审阅改动与工具权限；需要隔离时查看当前文档的 `/sandbox enable`。本轮只记录用法，没有安装或登录。[GitHub 当前官方文档](https://docs.github.com/en/copilot/concepts/copilot-surfaces/copilot-cli)

## 原理

终端会话将模型、工作区上下文与可执行工具结合，支持 MCP 扩展和 LSP 配置。交互与程序式入口可采用不同授权设置；README 的“每个动作都预览”不能覆盖所有自动授权模式。[README.md](https://github.com/github/copilot-cli/blob/c66d206a3b37d29ec082d4d42e8f4b99a0839c25/README.md) [GitHub 当前官方文档](https://docs.github.com/en/copilot/concepts/copilot-surfaces/copilot-cli)

## 价值

工程判断：适合已有 GitHub 工作流的团队评估从理解代码到形成 PR 的连续操作。有效指标是可接受改动、审阅时间、失败恢复和费用；终端原生体验不是正确性证据。

## 风险边界

- 官方文档明确 `--allow-all-tools` 可省略逐次审批，使工具拥有当前用户可用的文件和 shell 权限。sandbox 是可配置能力，不能默认为每次运行均生效。[GitHub 当前官方文档](https://docs.github.com/en/copilot/concepts/copilot-surfaces/copilot-cli)
- GitHub、模型、MCP 和本地命令分别具有身份、数据与写入权限；把能读 PR 与能推送 / 合并分开授权，并核有效配置。[README.md](https://github.com/github/copilot-cli/blob/c66d206a3b37d29ec082d4d42e8f4b99a0839c25/README.md)
- LICENSE 允许按条件运行和再分发未修改软件，但不授予修改、派生或任意独立分发权；API SPDX `NOASSERTION` 应回到正文解释。服务资格与隐私另受相应服务条款约束。[LICENSE.md](https://github.com/github/copilot-cli/blob/c66d206a3b37d29ec082d4d42e8f4b99a0839c25/LICENSE.md)

## 补充建议

固定安装版本、模型和授权配置，用测试仓库验拒绝命令、目录访问、MCP、取消与最终 diff。最新非预发行 Release `v1.0.101` 发布于 UTC 2026-10-20 18:49（上海 10 月 21 日），发行时间不能当成功能实测。

## 参考资料

- [README.md](https://github.com/github/copilot-cli/blob/c66d206a3b37d29ec082d4d42e8f4b99a0839c25/README.md)
- [LICENSE.md](https://github.com/github/copilot-cli/blob/c66d206a3b37d29ec082d4d42e8f4b99a0839c25/LICENSE.md)
- [仓库 API](https://api.github.com/repos/github/copilot-cli)
- [v1.0.101 Release](https://github.com/github/copilot-cli/releases/tag/v1.0.101)
