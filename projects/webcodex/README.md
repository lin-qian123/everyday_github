<!-- markdownlint-disable MD013 -->

# WebCodex（yyjeqhc/webcodex）中文解读

> 证据快照：2026-09-11（Asia/Shanghai）。GitHub REST API 显示 650 stars、81 forks、4 open issues，Apache-2.0；最新 GitHub release 与 Cargo workspace 版本为 `v0.4.1` / `0.4.1`。本文未安装 Desktop、创建 tunnel 或让远端 agent 修改本机仓库。

## 定位

WebCodex 让 ChatGPT、Claude 等 cloud AI client 通过 MCP/HTTPS 连接用户自己的开发机器，并由本地 Runner 读取仓库、编辑代码、运行 Git、compiler、test 和长时程 command。代码无需复制到托管 workspace，但远端模型仍可能看到任务所需的代码/工具输出。

它提供 regular Server + Runner 的完整长期模式，也提供一次性 `share` 的单项目临时 restricted 模式；两者的能力与生命周期不同。

## 用法

几分钟试用可在无敏感信息的仓库运行：

```bash
cd /path/to/your/repository
npx --yes @yyjeqhc/webcodex share
```

命令生成临时公网 HTTPS MCP endpoint 和 credential，进程退出即失效。日常完整模式应按 Desktop 或 Full Setup 文档安装 regular Server + Runner、注册精确 project roots，再连接 AI client。源码构建入口为 `cargo build --release --workspace --bins`。

## 原理

- AI client 通过 MCP/HTTPS 访问 Server；Server 将任务与 tool call 交给持有真实文件、Git 和 toolchain 的 Runner。
- project registration、workspace boundary、auth scope 和 tool contract 限制可达对象；Runtime Console 用于观察、取消、接受或拒绝支持的任务。
- `share` 创建临时单项目 surface；regular mode 可持久连接多个 project、保留长任务和证据。
- Cloudflare Tunnel、OpenAI Secure MCP Tunnel 或公网 HTTPS 只解决 reachability，不会自动收窄 regular Server/Runner 的执行权限。
- Rust workspace 拆分 server、runner、store、process、persistent shell、validation 和 tool contract；release 提供多平台 native artifact 与 npm wrapper。

## 价值

- 复用已经配置好的真实 checkout、compiler、test、Git 和本地依赖，不必重建 cloud workspace。
- 将长任务、工具输出与人工 review surface 保持可观察，适合远程监督本机开发环境。
- 临时 share 与长期 Server/Runner 两种模式便于先小范围验证，再扩展。
- 明确的 project root、auth 和 Runner ownership 为连接 cloud agent 与本地高权限工具提供了可审计结构。

## 风险边界

- WebCodex 能读写文件并执行命令；project boundary 不是 OS sandbox，仓库脚本、symlink、toolchain 和进程仍可能越过预期影响范围。
- “代码留在本机”只表示文件存储位置，不代表 prompt、代码片段、diff、命令输出或 secret 从未发送给模型/provider。
- tunnel 只是网络传输面，不会改变 full mode authority。临时 query-token URL 本身是 secret，不能进入聊天记录、日志或截图。
- 远端长期 Server、多用户、OAuth、Runner pairing、reverse proxy 与 service account 都需要独立 threat model。
- release CI 与自报 validation 证明有限构建/测试路径，不等于任意项目、shell command 或 malicious repository 安全。

## 补充建议

1. 先在 disposable repo 用 `share` 做只读结构检查，再做一个小改动并用 Git diff 人工验收。
2. regular mode 只注册明确项目根，使用专用低权限系统账户，隔离 SSH/cloud credentials 与主工作目录。
3. 对命令、网络、secret、symlink、后台进程和 destructive Git 操作设置额外 policy；tunnel credential 定期轮换。
4. 把“agent 返回完成”与实际 test、artifact、exit code、Git diff 和人工 review 分开记录。

## 参考资料

- GitHub：<https://github.com/yyjeqhc/webcodex>
- GitHub REST API：<https://api.github.com/repos/yyjeqhc/webcodex>
- Releases：<https://github.com/yyjeqhc/webcodex/releases>
- Quick Trial：<https://github.com/yyjeqhc/webcodex/blob/main/docs/QUICK_START.md>
- Full Setup：<https://github.com/yyjeqhc/webcodex/blob/main/docs/PERSONAL_SETUP.md>
- MCP 与认证：<https://github.com/yyjeqhc/webcodex/blob/main/docs/MCP.md>
- SECURITY：<https://github.com/yyjeqhc/webcodex/blob/main/SECURITY.md>
- LICENSE：<https://github.com/yyjeqhc/webcodex/blob/main/LICENSE>
