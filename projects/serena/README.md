<!-- markdownlint-disable MD013 -->

# serena

- 主上游：[oraios/serena](https://github.com/oraios/serena)
- 分类：Coding Agents 与终端助手。
- 核验日期：2026-11-02（Asia/Shanghai）；默认分支 `main`，固定快照 `ede329aaf0c8`。
- [API](https://api.github.com/repos/oraios/serena) 快照：30,990 stars / 2,119 forks / 139 open issues（含 PR）；发行列表首项 [v2.1.0](https://github.com/oraios/serena/releases/tag/v2.1.0)（UTC 2026-10-19）。累计量不是今日增量，主线不等于发行包。

## 定位

Serena 为编码 Agent 提供符号检索、引用查找、编辑、重构与部分调试能力，通过 MCP 接入现有客户端。默认免费后端是语言服务器；付费 JetBrains 插件使用 IDE 语义能力，两者功能不完全相同。Serena 提供工具，仍需外部 LLM 决定怎样使用。[README.md](https://github.com/oraios/serena/blob/ede329aaf0c824bea75455a2926f01420d7aa620/README.md)

## 用法

当前上游推荐直接通过 uv 安装，提醒部分 marketplace 命令过旧。本轮核 PyPI / 正式版为 2.1.0，主线包版本已是 2.1.1.dev0：

```sh
uv tool install -p 3.13 "serena-agent==2.1.0"
serena init
serena start-mcp-server
```

stdio 模式通常由 MCP 客户端以子进程启动，最后一行是其启动命令；手动 HTTP 模式才自行管理服务生命周期。先在可回滚的测试仓库初始化，并核所需语言服务器依赖。不要把主线新配置直接视为 2.1.0 已支持。[README.md](https://github.com/oraios/serena/blob/ede329aaf0c824bea75455a2926f01420d7aa620/README.md)、[docs/02-usage/020_running.md](https://github.com/oraios/serena/blob/ede329aaf0c824bea75455a2926f01420d7aa620/docs/02-usage/020_running.md)、[pyproject.toml](https://github.com/oraios/serena/blob/ede329aaf0c824bea75455a2926f01420d7aa620/pyproject.toml)

## 原理

通过 LSP 或 JetBrains 获取符号与关系，避免单靠全文搜索和行号替换；对外可用逐工具接口，也可用 v2 的 Python REPL 接口组合操作。引用和重构能力受语言服务器 / IDE 支持限制；JetBrains 的调试、移动、inline 等不能自动算作免费 LSP 后端能力。[README.md](https://github.com/oraios/serena/blob/ede329aaf0c824bea75455a2926f01420d7aa620/README.md)

## 价值

适合跨文件导航、大仓库符号改名与有精确语义目标的修改。上游展示的是 Agent 执行约 20 项任务后的自评，不等于独立、盲测的质量或省 token 结论；需要与同模型、同上下文和工具条件的真实任务比较。[README.md](https://github.com/oraios/serena/blob/ede329aaf0c824bea75455a2926f01420d7aa620/README.md)

## 风险边界

- 信任模型假设本机、客户端、仓库、配置与依赖下载配置可信。untrusted project 只关闭部分仓库驱动能力，不限制 Agent 整体的读写或命令执行。[docs/02-usage/070_security.md](https://github.com/oraios/serena/blob/ede329aaf0c824bea75455a2926f01420d7aa620/docs/02-usage/070_security.md)
- REPL 执行的是 Python 代码；`excluded_apis`、`read_only` 等只能约束 Serena 自身操作，无法阻止代码以进程权限修改文件。工具接口的排除与 REPL 的 API 裁剪不能当成同一种隔离。[docs/02-usage/070_security.md](https://github.com/oraios/serena/blob/ede329aaf0c824bea75455a2926f01420d7aa620/docs/02-usage/070_security.md)
- Codex context 排除了部分通用 shell / 文件工具，因为宿主已有相应工具；这不等于撤销宿主或 REPL 的权限。MCP、dashboard、JetBrains、Project Server 的 localhost 默认各自核对，跨机访问需单独保护。[src/serena/resources/config/contexts/codex.yml](https://github.com/oraios/serena/blob/ede329aaf0c824bea75455a2926f01420d7aa620/src/serena/resources/config/contexts/codex.yml)、[docs/02-usage/070_security.md](https://github.com/oraios/serena/blob/ede329aaf0c824bea75455a2926f01420d7aa620/docs/02-usage/070_security.md)
- 当前 SolidLSP 为 MIT，Serena 应用为 GPL-3.0-or-later，组合包整体按 GPL；历史 MIT 截止点以前的版本保留原许可。付费插件与贡献 CLA 另看条款，API 的 NOASSERTION 不是“无许可”。[LICENSE](https://github.com/oraios/serena/blob/ede329aaf0c824bea75455a2926f01420d7aa620/LICENSE)、[docs/01-about/060_license.md](https://github.com/oraios/serena/blob/ede329aaf0c824bea75455a2926f01420d7aa620/docs/01-about/060_license.md)

## 补充建议

选一项跨文件 rename、一项引用检索和一项小修复，记录 backend、模型、tool / REPL 接口、耗时与独立测试结果。若任务要求强制只读，应使用具备真实文件权限限制的进程环境，再核宿主工具权限。本轮未安装 Serena、下载语言服务器、接入 MCP 或调用模型。

## 参考资料

- [README.md](https://github.com/oraios/serena/blob/ede329aaf0c824bea75455a2926f01420d7aa620/README.md)（固定 commit）。
- [pyproject.toml](https://github.com/oraios/serena/blob/ede329aaf0c824bea75455a2926f01420d7aa620/pyproject.toml)（固定 commit）。
- [docs/02-usage/020_running.md](https://github.com/oraios/serena/blob/ede329aaf0c824bea75455a2926f01420d7aa620/docs/02-usage/020_running.md)（固定 commit）。
- [docs/02-usage/070_security.md](https://github.com/oraios/serena/blob/ede329aaf0c824bea75455a2926f01420d7aa620/docs/02-usage/070_security.md)（固定 commit）。
- [src/serena/resources/config/contexts/codex.yml](https://github.com/oraios/serena/blob/ede329aaf0c824bea75455a2926f01420d7aa620/src/serena/resources/config/contexts/codex.yml)（固定 commit）。
- [docs/01-about/060_license.md](https://github.com/oraios/serena/blob/ede329aaf0c824bea75455a2926f01420d7aa620/docs/01-about/060_license.md)（固定 commit）。
- [LICENSE](https://github.com/oraios/serena/blob/ede329aaf0c824bea75455a2926f01420d7aa620/LICENSE)（固定 commit）。
- [仓库 API](https://api.github.com/repos/oraios/serena)、[发行列表](https://github.com/oraios/serena/releases)（动态状态）。
- [PyPI 2.1.0](https://pypi.org/project/serena-agent/2.1.0/)。
