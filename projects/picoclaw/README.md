<!-- markdownlint-disable MD013 -->

# PicoClaw（sipeed/picoclaw）中文解读

> 上游仓库：<https://github.com/sipeed/picoclaw> · 归类：记忆层与个人 AI 基础设施 · 证据快照：2026-10-17（Asia/Shanghai）。API：30,077 stars / 4,470 forks / 44 open issues；GitHub Release / tag `v0.3.1`；README news 最新条目仍为 `v0.2.9`；MIT。本页为上游资料与相关代码的静态整理，未安装运行、复测性能或完成全面安全审计。

## 定位

PicoClaw 是 Sipeed 发起、用 Go 重写的轻量个人 AI 助手，支持多架构、小型 Linux 板、桌面和 Android 等部署。它是工具 / 会话 / 通道编排程序，常连接外部模型 provider；“小内存”描述助手进程，不是让完整大模型权重装进同样内存。

## 用法

从 README 指定的官方域名或 GitHub Release 选匹配系统架构的制品，先核对版本。最小 CLI 路径是 `picoclaw onboard`、配置模型、再运行 `picoclaw agent -m "What is 2+2?"`。Web launcher 默认 localhost:18800，`-public` 会扩大监听；先不开外部通道、exec、cron 与 MCP，以测试模型和专用 workspace 验证基础对话。源码构建另有 Go、Node 和 pnpm 依赖。

## 原理

- Go 单进程组织模型适配、工具、会话 / 记忆、路由和消息通道；模型可走云 API 或本地兼容 endpoint。
- Gateway 把聊天平台接入 Agent；MCP / skills 可继续扩展工具面，cron 支撑周期任务。
- workspace 限制与危险命令 guard 收敛文件 / shell；`.security.yml` 可分离敏感配置，凭据加密是另一个需主动配置的机制。

## 价值

轻量运行时和多架构制品方便在既有小设备上部署受监督助手。工程验收应测实际 RSS、启动时间、任务稳定性和 API 费用；README 已提醒近期构建可能用 10–20MB，不能沿用标题的 <10MB 为保证。

## 风险边界

- README 明确 pre-1.0 快速开发、未解决安全问题，建议 v1.0 前不生产部署；其硬件成本与性能倍率是作者对比，本次未复测。
- **远程 exec 默认值有冲突**：配置文档表格写 `tools.exec.allow_remote=false`；本次 main 的 `pkg/config/defaults.go` 却设 `AllowRemote: true`，同时 exec / cron enabled、cron AllowCommand 为 true。不能声称默认禁用远程命令；必须核对固定版本的实际配置及通道行为。
- 文档说明 exec guard 只检查顶层命令，不递归审查 make / npm / go 等生成的子进程；workspace guard 不能等同 VM 级隔离。
- `.security.yml` 分离不自动等于加密；云模型、消息通道、插件与本机 secrets 仍构成数据出口。项目另声明没有官方代币，仅信任其指定域名。

## 补充建议

显式设置并核验 `tools.exec.allow_remote=false`、不需要的 exec / cron 禁用、workspace 限制开启；独立限制通道身份。用专用 OS 用户或容器测试，核对密钥文件权限 / 加密和 provider 出站，按真实设备复测资源占用；不要仅依赖默认值。

## 参考资料

- 上游仓库：<https://github.com/sipeed/picoclaw>
- GitHub REST API：<https://api.github.com/repos/sipeed/picoclaw>
- README / 状态 / 官方域名：<https://github.com/sipeed/picoclaw/blob/main/README.md>
- 配置与 child-process 限制：<https://github.com/sipeed/picoclaw/blob/main/docs/guides/configuration.md>
- main 实际默认值：<https://github.com/sipeed/picoclaw/blob/main/pkg/config/defaults.go>
- 敏感配置：<https://github.com/sipeed/picoclaw/blob/main/docs/security/security_configuration.md>
- 独立凭据加密机制：<https://github.com/sipeed/picoclaw/blob/main/docs/security/credential_encryption.md>
- Go manifest：<https://github.com/sipeed/picoclaw/blob/main/go.mod>
- 许可：<https://github.com/sipeed/picoclaw/blob/main/LICENSE>
- Releases：<https://github.com/sipeed/picoclaw/releases>
