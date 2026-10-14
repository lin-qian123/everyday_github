<!-- markdownlint-disable MD013 -->

# JADX AI MCP（zinja-coder/jadx-ai-mcp）中文解读

> 上游仓库：<https://github.com/zinja-coder/jadx-ai-mcp> · 归类：Coding Agents 与终端助手 · 本页基于 2026-10-15 的 README、MCP transport / remote-binding 警告、POM、SECURITY、Release、许可证与 GitHub REST API 静态整理；未加载 APK、启动 JADX GUI / MCP server 或执行逆向与重命名操作。

## 定位

JADX AI MCP 是装进 JADX GUI 的 Java 插件，并配合独立 Python `jadx-mcp-server`，把反编译代码导航、类 / 方法查询、重命名、注释和 debug 信息暴露给 Claude、Codex 等 MCP client。它服务于 Android / Java 逆向分析，不是 APK 自动修复或漏洞结论证明器。

## 用法

用户先安装 JADX GUI 插件，再用 `uv` 启动独立 MCP bridge；默认 stdio 最安全，也可在本机 `127.0.0.1:8651` 运行 HTTP，连接 `127.0.0.1:8650` 的 JADX plugin。只有在专用隔离网络和额外认证 / TLS proxy 后才考虑远程地址，不能照抄 `--host 0.0.0.0` 示例到共享网络。

## 原理

- Java 插件嵌入 JADX GUI，访问当前 project / decompiler context，并开放查询、导航与重命名等能力。
- Python MCP server 将 LLM client 的 MCP tool call 转换为对插件服务的请求。
- `--host / --port` 控制 MCP server 的监听面，`--jadx-host / --jadx-port` 控制它查找 GUI plugin 的目标，两条连接必须分别建模。
- POM 当前为 `6.4.1`，依赖 JADX `1.5.5`、Javalin 和 Jackson；Release 标记为 `V6.4.1`。

## 价值

- Agent 能围绕真实 decompiler context 检索类、方法和调用关系，减少人工在 GUI 与聊天间搬运片段。
- 把语义重命名和注释回写到 JADX workspace，可持续积累分析上下文。
- stdio / loopback / remote 三种拓扑明确，适合在授权样本上构建可审阅的逆向助手。

## 风险边界

- 上游明确警告：非 localhost HTTP 是明文且无认证，网络中任何人都可调用全部工具、读取反编译代码、重命名类 / 方法并访问 debug 信息。
- MCP client 与 JADX plugin 是两个网络面；只保护其中一个端口不能形成端到端安全。
- 反编译输出可能不完整、错误或受混淆影响；Agent 的漏洞判断、调用链和语义命名都要回到 bytecode、运行时和人工证据。
- APK / 固件可能受版权、授权、商业秘密和计算机滥用法规约束；项目许可证只覆盖工具代码，不授予分析目标的权利。

## 补充建议

- 仅在断网逆向 VM 中使用自有或书面授权样本，默认 stdio / loopback，关闭端口转发和共享宿主发现。
- 用已知 ground truth APK 比较原始 JADX 与 Agent 辅助后的调用链、误报、遗漏和重命名可逆性。
- 固定 `V6.4.1`、JADX 版本与 Python bridge commit；保存 tool-call audit、原始 hash 和 workspace diff，任何修改均可回滚。

## 参考资料

- GitHub 仓库：<https://github.com/zinja-coder/jadx-ai-mcp>
- GitHub REST API：<https://api.github.com/repos/zinja-coder/jadx-ai-mcp>
- `V6.4.1` Release：<https://github.com/zinja-coder/jadx-ai-mcp/releases/tag/V6.4.1>
- README / remote warning：<https://github.com/zinja-coder/jadx-ai-mcp/blob/jadx-ai/README.md>
- POM：<https://github.com/zinja-coder/jadx-ai-mcp/blob/jadx-ai/pom.xml>
- SECURITY：<https://github.com/zinja-coder/jadx-ai-mcp/blob/jadx-ai/SECURITY.md>
- LICENSE：<https://github.com/zinja-coder/jadx-ai-mcp/blob/jadx-ai/LICENSE>
