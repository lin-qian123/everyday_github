<!-- markdownlint-disable MD013 -->

# Rakazo（elie222/rakazo）中文解读

> 上游仓库：<https://github.com/elie222/rakazo> · 归类：记忆层与个人 AI 基础设施 · 证据快照：2026-10-18（Asia/Shanghai）。认证 API：4,461 stars / 800 forks / 52 open issues；Release / tag `v0.2.0`；产品 beta；Apache-2.0。本页为上游材料及所列源码的静态整理，未安装运行、复测 benchmark 或完成全面安全审计。

## 定位

Rakazo 是可自托管的持久 AI 队友系统，把对话、记忆、日程与带浏览器 / 终端的 computer 连接起来，提供 Web、Electron 和移动端。适合希望自行管理服务、模型与执行环境的人；它仍是 beta，上游“替代某产品”的比较是产品定位，不代表功能、质量和隐私对等。

## 用法

README 的发布镜像安装器会下载 Compose、生成独立随机密钥并启动服务；先下载审阅脚本，以 `--prepare-only` 检查配置，再在专用测试环境启动。CLI 安装器默认镜像是跟随 main 的 `edge`；已打包桌面版按自身版本固定镜像，两者不能混作相同部署。打开 loopback UI、创建账号、连接模型，先用无登录信息的测试 computer。

## 原理

API / worker 中的 Pi 运行 Agent 会话，通过 SandboxProvider 将浏览器、桌面、shell 和文件操作交给 Docker / 远端 provider。Team Computer 默认共享 workspace，bot 子目录用于组织；Private Computer 另配完整工作区。PostgreSQL、worker、持久 home 和独立 screen capability 支持重启、历史与接管。

## 价值

把模型与 computer provider 分离，便于独立替换与测量；多前端共用状态，适合跨设备接续。实际价值应以长任务最终验收、恢复一致性、误操作、费用与接管延迟衡量，而不是只看 bot 一直在线。

## 风险边界

- **Team bot 目录不是互不信任的隔离边界**：运行时文档明确同一 computer 共享 OS 用户、workspace、浏览器资料和 shell / X11 能力；独立 Chrome profile 与租约不阻止同容器进程互访。需要隔离时分 computer。
- Docker supervisor 挂载 Docker socket，Compose 默认 computer egress 为 open；其 token、网络和宿主暴露面要单独收敛。可信本机 provider 也不是远端沙箱。
- 连接模型、语音、Composio / MCP 等会产生数据外发和真实读写；持续 browser profile 保留 cookie，关闭 viewer 不等于销毁 computer。
- `.env` 与数据卷要配套备份；重建随机 `ENCRYPTION_KEY` 会让旧凭证不可读，`docker compose down -v` 会删除数据库状态。自托管不自动解决授权或恢复。

## 补充建议

先用单 bot + 私有测试 computer，禁止真实外部写入并限制出站和预算；再验证两个 Team bot 的共享范围、control 撤销、停止 / 恢复与旧浏览器会话。固定镜像版本，演练携带原密钥和数据卷的恢复，再考虑长驻和生产集成。

## 参考资料

- 上游仓库：<https://github.com/elie222/rakazo>
- GitHub REST API：<https://api.github.com/repos/elie222/rakazo>
- README / 镜像与桌面安装：<https://github.com/elie222/rakazo/blob/main/README.md>
- computer 与隔离契约：<https://github.com/elie222/rakazo/blob/main/docs/computer-runtime.md>
- 自托管密钥和恢复：<https://github.com/elie222/rakazo/blob/main/docs/self-host-secrets.md>
- Compose 默认值：<https://github.com/elie222/rakazo/blob/main/infra/compose/docker-compose.yml>
- 安全范围：<https://github.com/elie222/rakazo/blob/main/SECURITY.md>
- Release：<https://github.com/elie222/rakazo/releases/tag/v0.2.0>
- 许可：<https://github.com/elie222/rakazo/blob/main/LICENSE>
