<!-- markdownlint-disable MD013 -->

# HA-MCP

## 定位

HA-MCP 是面向 Home Assistant 的社区 MCP 服务，让 AI 客户端查询设备、维护自动化、仪表盘和配置。它的管理面比只控制 Assist 已暴露实体的 HA 内置 MCP 更广，两者权限范围不同。

- 上游：[homeassistant-ai/ha-mcp](https://github.com/homeassistant-ai/ha-mcp)，仓库 ID `1056618941`。
- 2026-11-10：5,911 stars / 292 forks / 25 open issues（含 PR）；综合 daily +31。
- 稳定版 [v9.1.2](https://github.com/homeassistant-ai/ha-mcp/releases/tag/v9.1.2)，UTC 11-08；PyPI 同版，Python `>=3.13,<3.15`。另有 9.2.0.dev 预发行。本页按主线 `4d9d4315ad3a27e1ab5522e4e2739eb57327c451` 核读，新能力须核目标 tag。

## 用法

1. 当前文档推荐进程内 HA-MCP integration，要求 HA ≥2026.8；2026.8–10 用 HACS，2026.11+ 可用 Marketplace。安装后重启 HA 并添加 HA-MCP Server integration。
2. 为服务配置专用管理员账号或管理员长效 token，选择本地 / 远端连接；两类接入初始均关闭。复制配置页 URL 给客户端，保管 token 和 secret URL。
3. OS / Supervised 还可用 app（add-on）；Docker、PyPI / uvx、stdio 是独立入口。每个客户端只保留一种连接；文档因已知传输问题不推荐 stdio 用于真实部署。
4. 从测试 HA 与只读查询开始，再核工具策略、管理权限、备份和回滚。

本轮仅核文档与配置源码，未连接家庭网络、安装组件或调用设备。

## 原理

MCP 工具将请求映射到 HA REST / WebSocket 与组件服务；进程内组件还可提供普通 API 没有的文件 / YAML 能力。`ha_config_set_yaml` 已迁到 beta。工具发现、可见性、策略和 HA 身份分别作用于不同层。

主线支持 HTTP endpoint 后加 `/readonly`，隐藏写工具并阻止直接、缓存和搜索代理写调用；改 URL 后需重连。**这是连接模式**，同一凭据仍能访问普通 endpoint，不是独立的只读凭据。

## 价值

- 聚合状态、日志、自动化和配置检查，减少多界面切换。
- 为多客户端 MCP、工具发现和管理策略提供工程样本。
- 以正确修改、回滚和最终设备状态衡量效果，工具数量不代表可靠性。

## 风险边界

- **可信客户端**：安全文档不防恶意或已失陷的认证客户端；标准 secret-URL 模式单租户、共享权限。管理员 token 对应管理员操作，服务不会自动降权。
- **身份模式不同**：OAuth 路线可按 HA token 区分；OIDC 是访问门禁，用户共用服务端 HA token。共享 IdP 应核 `OIDC_AUDIENCE`，文档注明默认不验 audience 的条件。
- **网络入口**：外部 HTTP 入口默认绑定 `0.0.0.0`，Host / Origin 校验默认关闭；OAuth / OIDC settings 路由有独立 secret-path 边界。
- **过滤并非隔离**：实体隐藏是尽力遮蔽；`python_transform` 的限制面向意外错误，不防恶意客户端；工具列表和提示词不能替代授权。
- **本地与外发**：隐私文档只覆盖 HA-MCP，保留“截至2026-06未采集匿名统计”的时间限定；客户端、云模型和主动 bug report 另有数据流，不能承诺全链路不外发。
- 根许可证 MIT；真实设备动作的后果需要独立确认。

## 补充建议

固定客户端、server 与 integration 版本，在测试实例核普通 / readonly / settings 三类入口与凭据撤销。逐项验证策略、备份恢复和配置引用，不用实体名称过滤承担安全隔离；门锁、报警、温控等动作要有明确的人类决策与状态复核。

## 参考资料

- [固定 SHA README：安装与 readonly](https://github.com/homeassistant-ai/ha-mcp/blob/4d9d4315ad3a27e1ab5522e4e2739eb57327c451/README.md)
- [安全威胁模型](https://github.com/homeassistant-ai/ha-mcp/blob/4d9d4315ad3a27e1ab5522e4e2739eb57327c451/SECURITY.md)
- [进程内服务配置](https://github.com/homeassistant-ai/ha-mcp/blob/4d9d4315ad3a27e1ab5522e4e2739eb57327c451/docs/in-process-server.md)
- [OIDC 配置](https://github.com/homeassistant-ai/ha-mcp/blob/4d9d4315ad3a27e1ab5522e4e2739eb57327c451/docs/oidc.md)
- [隐私政策及日期范围](https://github.com/homeassistant-ai/ha-mcp/blob/4d9d4315ad3a27e1ab5522e4e2739eb57327c451/PRIVACY.md)
- [Python 要求](https://github.com/homeassistant-ai/ha-mcp/blob/4d9d4315ad3a27e1ab5522e4e2739eb57327c451/pyproject.toml)、[PyPI 快照](https://pypi.org/pypi/ha-mcp/json)
