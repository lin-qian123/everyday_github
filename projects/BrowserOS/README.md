<!-- markdownlint-disable MD013 MD034 -->

# BrowserOS：把真实登录态浏览器交给人和 AI agents 的本地工作台

## 项目概览

- 上游仓库：https://github.com/browseros-ai/BrowserOS
- GitHub API 快照（2026-09-03）：13,503 stars、1,421 forks、89 个开放 issue
- 当前 release：`ext-agent/v0.0.146.0`
- 主要技术：Chromium fork、Rust / TypeScript / Go、CDP、MCP、桌面 dashboard
- 许可证：AGPL-3.0

## 定位

同一仓库包含两个入口：BrowserOS neo 是供 Claude Code、Codex 等外部 agents 驱动的第二浏览器；BrowserOS 是带内置 agent 的 Chromium fork。二者都强调本地运行、复用真实登录态、可观察和回放浏览器任务。

这与无状态 CI 浏览器不同：它的价值恰恰来自真实 cookies、账号和网页权限，因此也具有更高的业务副作用与隐私风险。

## 用法

上游为 macOS、Windows 与 Linux 提供安装包。BrowserOS neo 可导入 Chrome 的登录、书签和扩展，并一键连接 Claude Code、Codex、Cursor 等 MCP clients；BrowserOS 则允许配置云端 provider、OAuth，或使用 Ollama / LM Studio。

建议先新建专用浏览器身份和测试账号，不要导入日常 Chrome profile。只给 agent 打开一个受控站点和只读任务，验证 session 录像、action timeline、MCP 工具、删除与网络出口后再扩展。

## 原理

Chromium fork 提供浏览器本体；Rust backend / Bun server 暴露 MCP 与 JSON API，扩展页面展示并行 agent、当前动作和回放记录，Go CLI 负责终端控制。每个 agent 可在独立 tab 工作，但仍共享同一浏览器产品与账户环境。

BrowserOS neo 把 sessions、screenshots 和 history 写到本机 `~/.browserclaw/`。这是一条数据位置声明，不代表内容已加密、最小化或不会被所连接的云模型和目标网站接收。

## 价值

- 让外部 agents 使用已有登录态处理邮件、CRM、报表等真实网页流程。
- dashboard 与本地回放比纯 headless 执行更容易人工观察和追责。
- 支持多种 agent harness、MCP 与本地模型，减少单一模型锁定。
- BrowserOS 与 neo 分开“人主导”和“agent 主导”的浏览入口。

## 风险边界

- 真实登录态意味着 agent 可能发帖、删除、购买、下载或修改企业数据；独立 tab 不是账号和权限隔离。
- 导入密码、cookies、扩展与历史会扩大攻击面；恶意页面、提示注入和被污染扩展可影响任务。
- 本地录像、截图和 timeline 可能包含邮件、token、客户资料与个人信息，需要加密、访问控制和保留期。
- 使用云 provider 时页面内容和指令可能外发；“runs on your machine”不等于端到端离线。
- AGPL-3.0 对修改、部署和网络使用的义务需按实际方案审查。
- 本页依据上游 README、release 与 API，未安装，也未验证 token 节省、隐私和自动化成功率主张。

## 补充建议

1. 创建专用 OS 用户、浏览器 profile 和测试账号，禁止导入主力密码库与支付方式。
2. 对发帖、邮件、支付、删除、上传和权限变更实行 preview + 人工确认 + 结果截图。
3. 检查 `~/.browserclaw/` 的文件权限、加密、清理、备份和 crash 恢复，不把录像当作无害日志。
4. 用提示注入、跨 tab 污染、OAuth 过期和恶意下载样本做回归，并限制 MCP 可达站点。
5. 分开评估 BrowserOS 与 BrowserOS neo，不从一个入口的体验外推另一个入口。

## 参考资料

- 仓库与 README：https://github.com/browseros-ai/BrowserOS
- Releases：https://github.com/browseros-ai/BrowserOS/releases
- 官方站点：https://www.browseros.com/
- BrowserOS neo 文档：https://docs.browseros.com/neo
- 官方 X 账号：https://x.com/browserOS_ai
- 官方演示：https://www.youtube.com/watch?v=SoSFev5R5dI
