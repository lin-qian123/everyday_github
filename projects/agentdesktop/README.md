<!-- markdownlint-disable MD013 -->

# agentdesktop（agentdesktop-dev/agentdesktop）

> 记录日期：2026-09-05（Asia/Shanghai）。本页依据 2026-09-03 官方发布、上游 README、文档、release 与 GitHub API 做静态整理；它不是 2026-09-05 GitHub Trending 入选项，本页也未部署 daemon、controller、OIDC 或 LLM gateway。

## 定位

`agentdesktop` 是 Solo.io 发布的桌面 AI 工具治理层，面向组织发现并管理 Claude Code、Codex、OpenCode、VS Code 等工具及其 MCP、skills、模型配置、sandbox 意图和 gateway 凭据。它定位在 MDM 之上：MDM 管设备与 OS posture，agentdesktop 管 agent harness 的配置、身份与可观测性。

项目于 2026-09-03 正式公布并发布 `v0.1.0`。2026-09-05 的 GitHub REST API 快照为 `78 stars / 9 forks / 17 open issues`，许可证为 Apache-2.0。这里的收录依据是官方新发布和仓库可核验性，不是 Trending 排名或跨平台热度结论。

## 用法

上游提供从 release 下载 binary 或从源码构建的方式，并建议先用 standalone 模式：

```bash
git clone https://github.com/agentdesktop-dev/agentdesktop.git
cd agentdesktop
corepack enable
make install

agentdesktop daemon \
  --config examples/standalone/config.yaml \
  --user \
  --dry-run
```

`--dry-run` 用于预览拟写入的工具配置；移除后 daemon 会执行 reconcile。正式评估应使用专用测试用户、测试 IdP、测试 gateway 和无生产密钥的设备，先审查 diff 再允许写入。

## 原理

- **端点发现**：daemon 检测本机支持的 AI 工具和版本，清点 MCP、skills 与模型配置。
- **原生配置转换**：把组织层 sandbox / gateway / tool policy 翻译为各 harness 自己的 JSON、JSONC、TOML 或其他配置。
- **独立与托管模式**：standalone 从本地 YAML 读取策略；controller-managed 模式集中管理版本、设备注册、身份和状态回报。
- **设备与用户身份**：设备本地生成私钥和 CSR，经 OIDC 注册后用证书与用户 token 访问 controller。
- **短时凭据**：controller 可签发带 user、device、client label、audience 和 expiry 的 JWT，provider key 留在 gateway。
- **可选遥测**：组织可选择收集 session 与 tool-use 事件，并与用户、设备和 gateway 使用关联。

## 价值

- 把分散在多种 coding-agent 配置中的 MCP、skills、模型和 sandbox 意图集中到可盘点、可版本化的治理表面。
- 短时 gateway 凭据有助于减少长效 provider key 直接散落在工作站。
- `dry-run`、reconcile status 和 managed configuration 为组织审查配置漂移提供基础。
- 明确与 MDM、PKI、IdP 和 LLM gateway 分层，便于接入已有企业控制面。

## 风险边界

- agentdesktop 翻译 harness 的原生 sandbox 配置，不等于自己提供独立 OS sandbox；底层工具不支持的限制无法凭声明补足。
- 上游明确指出 `client_id` 是本地 helper 声明的 label，不是调用进程的密码学证明；同一用户边界内的其他进程可能请求允许的 label。
- MCP connection 会被清点，但不会自动经过 agentgateway；工具调用的数据面和权限仍需独立治理。
- 集中 controller、PKI、IdP、gateway 与配置写入形成高价值控制面，需要高可用、最小权限、审计和恢复设计。
- inventory / telemetry 即使宣称不收 secrets 或 skill body，也应通过包捕获、日志和失败路径实测数据最小化。
- `v0.1.0` 是早期版本，支持矩阵会随 harness 配置 schema 变化，需要持续兼容测试。

## 补充建议

- 先在专用设备以 `--dry-run` 保存 before / after diff，覆盖 Codex、Claude Code、OpenCode 与 VS Code 的不同配置格式。
- 用恶意同用户进程测试 client label 冒用，并把 gateway policy 建在可验证的 user / device / audience 上。
- 分别测试 daemon 停止、controller 不可达、证书过期、SSO 撤销、配置冲突、版本回退和 MDM 强制策略。
- 对 inventory 与 telemetry 建字段 allowlist、保留期、用户告知、导出 / 删除与管理员访问审计。
- 将“配置已写入”“harness 已读取”“sandbox 真正生效”“gateway 拒绝绕过”设为四个独立验收点。

## 参考资料

- [GitHub 仓库](https://github.com/agentdesktop-dev/agentdesktop)
- [GitHub REST API](https://api.github.com/repos/agentdesktop-dev/agentdesktop)
- [Solo.io 官方发布](https://www.solo.io/blog/introducing-agentdesktop)
- [项目公告](https://agentdesktop.dev/blog/2026/09/introducing-agentdesktop/)
- [Standalone Quickstart](https://agentdesktop.dev/docs/getting-started/standalone/)
- [v0.1.0 Release](https://github.com/agentdesktop-dev/agentdesktop/releases/tag/v0.1.0)
