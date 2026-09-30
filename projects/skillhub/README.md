<!-- markdownlint-disable MD013 -->

# SkillHub（iflytek/skillhub）

> 上游仓库：<https://github.com/iflytek/skillhub> · 归类：Agent 框架与技能生态 · 本页基于 2026-10-01 的 GitHub API、中英文 README、架构、privacy / data governance、security scanning、Release 与 LICENSE 静态整理，未部署 registry、上传内部 skill 或验证租户隔离。

- 抓取快照：5,196 stars、846 forks、30 open issues。
- 热度信号：GitHub Java Trending 抓取时约 +10 当日 stars。
- 版本与许可：Apache-2.0；latest Release 与 tag 均为 `v0.2.21`。

## 定位

SkillHub 是面向组织的自托管 Agent Skill 注册与治理平台，用命名空间、版本、搜索、审核、RBAC、审计与 CLI 分发标准 `SKILL.md` 包。它是基础设施层而非技能内容集合，可接入 OpenClaw、Hermes Agent、DeepSeek Harness 等宿主，并提供 ClawHub 风格兼容读取路径。

## 用法

本地可用 Docker Compose / `make dev-all` 启动，生产支持 Compose、Kubernetes 与 Helm；CLI 通过 `npx @astron-team/skillhub` 登录、搜索、发布和安装。项目级或用户级 `--dir` 可把完整技能包写入指定宿主目录。生产部署必须配置外部 URL、真实认证、数据库、Redis、对象存储、TLS 与邮件 / 观察系统，不能沿用本地默认账户。

## 原理

后端维护技能、版本、namespace、review、promotion、rating、download 与 audit domain；包体放本地或 S3-compatible object storage，全文索引和事件流支撑搜索与治理。可选 scanner 将上传包放入 Redis task，经独立 `skill-scanner` 服务分析后写入 security audit，再进入人工 review；默认配置中 scanner 可关闭，且 `isSafe` 只表示没有高风险发现。

## 价值

它解决团队直接在 Git 仓库、聊天或用户目录复制 skill 时缺少版本与权限边界的问题。namespace policy、scope token、审核记录和固定版本能让技能分发更可追踪，也为内网团队保留私有 skill 和许可证元数据提供统一入口。

## 风险边界

- Skill 是可执行供应链资产；registry 上架、扫描或管理员批准都不能证明脚本、引用和后续网络行为安全。
- scanner 默认可禁用，连接失败最终会进入 `SCAN_FAILED` 但仍创建人工 review；“无高风险发现”也可能保留中低风险 findings。
- 开发 / release 模板可能启用默认管理员和普通账户；未更换凭据、关闭开发认证或正确配置公网 URL 时不可外部暴露。
- package、review、日志、trace、scanner findings 与对象存储都可能含个人数据、内部代码或 secret；自托管不自动满足合规。
- namespace RBAC、对象存储隔离、删除、备份和外部 OAuth / SMTP / monitoring / LLM scanner 数据流须由部署者独立验证。
- Apache-2.0 只覆盖平台代码；每个 skill、脚本、模型、素材和依赖都有自己的许可证与用途限制。

## 补充建议

用两个测试 namespace、不同角色和恶意样例做越权、路径穿越、软链接、压缩炸弹、提示注入和 scanner-failure 演练；发布必须固定 digest，安装前展示 diff / permission manifest。生产中删除默认账户，启用 TLS、最小 scope token、对象存储隔离、备份恢复与可导出审计；外部 scanner 前先做数据分类和脱敏。

## 参考资料

- [GitHub 仓库](https://github.com/iflytek/skillhub)
- [GitHub REST API](https://api.github.com/repos/iflytek/skillhub)
- [中文 README](https://github.com/iflytek/skillhub/blob/main/README_zh.md)
- [系统架构](https://github.com/iflytek/skillhub/blob/main/docs/01-system-architecture.md)
- [Privacy and Data Governance](https://github.com/iflytek/skillhub/blob/main/docs/PRIVACY_AND_DATA_GOVERNANCE.md)
- [Security Scanning](https://github.com/iflytek/skillhub/blob/main/docs/security-scanning.md)
- [v0.2.21 Release](https://github.com/iflytek/skillhub/releases/tag/v0.2.21)
- [LICENSE](https://github.com/iflytek/skillhub/blob/main/LICENSE)
