<!-- markdownlint-disable MD013 -->

# appwrite：为应用与 Agent 提供统一后端

- 上游：[appwrite/appwrite](https://github.com/appwrite/appwrite)，repository ID `180190854`；2026-11-28 新建档案。
- 快照：58,696 stars / 5,918 forks / 628 open issues（累计，含 PR）；TypeScript daily +50。
- 默认 SHA `958036ffcb239156fdbda28291192259839a9dd6`，2026-11-27；最新所见发行 2.7.4（11-19），tag 提交 `16b1118058ca65b4d0428a17a53ca7dba94f8de9`。主线 README 的安装示例仍为 2.7.2，不能据此选定最新维护版本。
- 范围：固定 README、manifest、安装入口、2.7.4 Compose / 发行说明，以及当前官网 MCP / 权限文档；大递归 tree 获取失败后只查根目录与指定文件，未完整审计、安装、授权或部署。

## 定位

Appwrite 是集成身份、数据库、文件、函数、消息、实时事件与站点托管的后端平台。现有 README 强调 MCP 和 coding agents：让 Agent 查询或修改真实项目，而非只生成接入代码。它也能通过 SDK 服务普通应用，不是模型本身或通用自主 Agent。

托管 Appwrite Cloud 与自托管服务器是不同交付范围。官网近期的项目 environments beta 和托管 PostgreSQL 19 属于 Cloud 功能，不能由主仓库源码、BSD 许可或 2.7.4 发行号推定自托管具有相同能力。

## 用法

1. 先选择 Cloud 或自托管，并建立测试项目。Cloud 的远程 MCP 地址为 `https://mcp.appwrite.io/`，客户端通过 OAuth 登录授权；无需为这个入口手工创建 API key。
2. 先用文档搜索、列出项目和读取测试资源检查项目 / environment 身份，再考虑创建或删除。当前远程工具集通过搜索发现具体操作；写调用须有 `confirm_write: true` 和原因。
3. 自托管应跟随官网的 self-hosted MCP 文档，使用本地 stdio 与实例 API key；Cloud OAuth 入口不会自动连接任意本地实例。该本地入口默认启用数据库工具，可按需增加工具，且不支持远程入口的 Events。按用途限制 key scopes，避免把 server key 放进前端。
4. 自托管安装需要 Docker。所查主线 README 将安装向导端口映射到 `127.0.0.1:20080`，并要求一次性 secret；安装命令同时挂载 Docker socket 和可写目录，需在专用测试主机先验收。
5. 选择确定的发行 / 镜像身份并备份。2.7.4 发行说明要求运行升级后的 migration，称已在 2.7 的实例无需改动数据；这不替代实际备份恢复验证。

这里没有执行任何安装命令或 MCP 登录。普通应用可从 Auth + 一张测试表 / 一个 bucket 起步，分别验证客户端身份、资源权限和服务端操作。

## 原理

应用 SDK 将操作交给统一 API，后端协调身份、数据、存储、执行器和事件等组件。固定 2.7.4 Compose 中包含多个服务及 OpenRuntimes executor；主线 `composer.json` 要求 PHP ≥8.5，因此 API 标记的主要语言不足以说明完整运行栈。

当前官网远程 MCP 先暴露上下文、工具搜索、读调用、写调用和文档搜索，再按需找到完整目录中的操作。写原因会进入项目 Activity。订阅事件还会创建项目 webhook，并使用 OAuth 权限；官方说明断线期间的事件不重放，重连后应重新读取状态。

资源权限和服务端权限有不同作用：官网说明，合适 scopes 的 Server SDK API key 可绕过用户的资源权限。应用端一行记录的 ACL 不能单独约束持有高权限 server key 的 Agent。

## 价值

它减少了从原型到带身份、数据、文件和函数的应用所需接线，适合评估 Agent 对真实业务后端的操作方式。可查询操作原因、区分环境与工具类型，有助于检查一次变更由谁、在何处、为何发起。

自托管使部署和数据治理有更多自主权，但仍需自己承担更新、镜像、执行器、密钥、备份与网络维护。官网产品功能与作者维护声明不等于本轮完成了性能或安全测试。

## 风险边界

| 议题 | 已核事实与边界 |
| --- | --- |
| 版本差异 | README 安装 2.7.2、最新所见发行 2.7.4、主线持续开发；当前 Cloud 文档也不是 2.7.4 的固定功能契约。 |
| 人工批准 | `confirm_write` 和原因由模型提交；MCP annotations 供客户端处理。工程判断：字段存在不证明用户实际确认，须验证目标客户端的审批行为。 |
| 服务端权限 | Server SDK + 合适 scopes 能绕过资源 ACL；项目、key scope、OAuth 授权及可执行工具需共同限制。 |
| 主机权限 | README 安装和 2.7.4 Compose 使用 Docker socket；向导的 localhost / secret 只控制该入口，不能当成整套执行栈的权限隔离。 |
| 事件可靠性 | 官方明确断线期间事件不重放；订阅使用项目 webhook 和额度，不能仅依赖推送实现业务账本。 |
| 云端升级 | PostgreSQL 19 官方公告说明升级单向、切换会关闭连接；“online / minimal downtime”不等于零中断、可降级或自托管同等支持。 |
| 许可与补丁 | 根 LICENSE / API 为 BSD-3-Clause；模型、第三方镜像和云服务条款另核。2.7.2–2.7.4 安全 / 稳定修复为发行者说明，本轮未做漏洞或镜像扫描验证。 |

## 补充建议

1. 为 Agent 使用专用测试项目及最小 scopes，验证越权读、写拒绝、审批和撤销，保存实际工具名与 Activity 记录。
2. 把 Cloud / 自托管、应用用户 / Server SDK、读取 / 写入、event / 对账分别测试，避免以一个成功示例替代全链路验收。
3. 固定镜像 digest 与配置，保管备份和加密密钥；在副本中做升级、恢复、连接中断与重试实验。
4. 有事件驱动任务时另做状态回查和幂等处理；用目标并发、数据规模、账单和恢复时间评价价值。

## 参考资料

- [仓库 API](https://api.github.com/repos/appwrite/appwrite)、[固定 README](https://raw.githubusercontent.com/appwrite/appwrite/958036ffcb239156fdbda28291192259839a9dd6/README.md)、[composer.json](https://raw.githubusercontent.com/appwrite/appwrite/958036ffcb239156fdbda28291192259839a9dd6/composer.json)、[主线安装入口](https://raw.githubusercontent.com/appwrite/appwrite/958036ffcb239156fdbda28291192259839a9dd6/src/Appwrite/Platform/Installer/Server.php)。
- [2.7.4 发行](https://github.com/appwrite/appwrite/releases/tag/2.7.4)、[该 tag 的 Compose](https://raw.githubusercontent.com/appwrite/appwrite/16b1118058ca65b4d0428a17a53ca7dba94f8de9/docker-compose.yml)、[LICENSE](https://raw.githubusercontent.com/appwrite/appwrite/958036ffcb239156fdbda28291192259839a9dd6/LICENSE)。
- 当前官网：[MCP](https://appwrite.io/docs/tooling/ai/mcp-servers)、[自托管 MCP](https://appwrite.io/docs/advanced/self-hosting/mcp)、[权限](https://appwrite.io/docs/advanced/security/permissions)、[Cloud PostgreSQL 19 公告](https://appwrite.io/blog/post/announcing-postgresql-19)。原 README 的 MCP `/api` 文档链接已转向上述通用页。
