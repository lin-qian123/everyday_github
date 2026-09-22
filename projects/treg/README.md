<!-- markdownlint-disable MD013 -->

# treg（superdesigndev/treg）

- GitHub：<https://github.com/superdesigndev/treg>
- 抓取快照：2026-09-23，2,186 stars、217 forks、81 open issues
- 热度信号：GitHub Python Trending 抓取时约 +197 当日 stars
- 版本与许可：无 GitHub Release / tag，`pyproject.toml` 为 `0.21.0`；API 为 `NOASSERTION`，根 LICENSE 是 Apache-2.0 加托管服务限制

## 定位

treg 是面向 Agent 工具的 registry、credential relay、计费目录与 MCP / CLI 接入层。其托管目录宣称覆盖 60+ provider、3,000+ endpoint；团队也可注册自己的 HTTP endpoint、OAuth、供应商 CLI 和 `SKILL.md`，由服务端注入凭据，调用方只持有一个 treg token。

## 用法

托管路径通过安装脚本和 `treg login` 接入，可搜索 catalog、查看价格后调用 endpoint，或安装 Claude Code plugin / MCP。团队自有路径用 `treg scan` 预览，再以 `treg upload` 上传 `.env` 中识别出的 provider key、skills 和已安装 CLI；自托管则需要配置数据库、Fernet 密钥、session secret、OAuth client 等并备份密钥和数据。

## 原理

注册表按组织隔离 secret、tool、bundle 和 call record。请求到来后按“团队自有工具 → 团队 provider secret → 无需密钥的公开 route → treg 自有账号”选择凭据路径，服务端解密并注入 header、query、env、secret file 或 OAuth token，再把请求转发给上游。MCP v2 对 curated catalog 区分 read / write safety signal；旧 MCP 面仍可暴露团队工具与 imported skills。

## 价值

它把 Agent 的工具发现、价格可见性、共享凭据、OAuth 刷新、调用审计和 CLI 执行统一到一条入口，减少每个 Agent 独立保管几十个 provider key 的需求。对于偶发的昂贵数据 API，也提供按调用付费而非逐个订阅的工程选择。

## 风险边界

- treg 是高价值凭据与高后果工具的集中控制面；服务器、Fernet key、super-admin token 或组织隔离失效都会扩大影响半径。
- `treg upload` 会扫描 `.env`、skills 和已安装 CLI；预览、选择范围和脱敏必须先于上传，不能把便利当作最小权限。
- faithful relay 不理解上游业务语义；read / write 标签、价格和参数校验不能替代目标系统的权限、预算、幂等、回读和人工审批。
- 托管路径存在计费、第三方 provider 数据流与匿名命令遥测（可用 `TREG_TELEMETRY=0` / `DO_NOT_TRACK=1` 关闭）。
- 根许可证禁止未经授权把该软件作为面向第三方的 hosted / managed / embedded commercial service，不应简称为纯 Apache-2.0 开源。

## 补充建议

先在独立组织中只接入只读、低额度、可撤销凭据，固定 endpoint allowlist、单次 / 单日预算和审计保留期。对每个工具保存参数 schema、side-effect 等级、重试 / 幂等语义和回滚方式；自托管时定期做密钥轮换、恢复演练与跨租户对抗测试。

## 参考资料

- [GitHub 仓库](https://github.com/superdesigndev/treg)
- [GitHub REST API](https://api.github.com/repos/superdesigndev/treg)
- [README](https://github.com/superdesigndev/treg#readme)
- [MCP 与 OAuth 架构](https://github.com/superdesigndev/treg/blob/main/docs/context/architecture/mcp-oauth.md)
- [自托管运维说明](https://github.com/superdesigndev/treg/blob/main/docs/context/ops/deploy.md)
- [SECURITY](https://github.com/superdesigndev/treg/blob/main/SECURITY.md)
- [自定义 LICENSE](https://github.com/superdesigndev/treg/blob/main/LICENSE)
