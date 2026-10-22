<!-- markdownlint-disable MD013 -->

# onyx

- 主上游：[onyx-dot-app/onyx](https://github.com/onyx-dot-app/onyx)
- 分类：RAG、检索与知识处理。
- 核验日期：2026-10-23（Asia/Shanghai）；主线快照 `5bfd6e0b5592`。
- [API](https://api.github.com/repos/onyx-dot-app/onyx) 快照：32,859 stars / 4,616 forks / 595 open issues；发行列表首项 [v4.9.4](https://github.com/onyx-dot-app/onyx/releases/tag/v4.9.4)（UTC 2026-10-22，正式）。累计值不代表今日增量。

## 定位

Onyx 面向团队知识检索与 AI Agent，将应用连接器、文档索引、混合检索和生成式回答整合为平台，并提供聊天、MCP、网页搜索、外部动作等入口。适合有多来源知识、运维能力和权限治理需求的团队。[README](https://github.com/onyx-dot-app/onyx/blob/5bfd6e0b55922466e45e2ff822910c609508a74c/README.md)

## 用法

先选部署模式：Standard 含索引、同步 worker、模型服务与缓存 / 对象存储；Lite 是更轻的聊天 / Agent UI，**不支持文档索引**。跟随官方 Docker 或 Kubernetes 部署文档，在公开测试文档与两个不同权限账号上验证后再接内部资料。

Docker 环境模板默认 `IMAGE_TAG=latest`，注释说明它是 main nightly；建议固定已核版本。本轮发行列表首项为 v4.9.4，同时有 v4.8.8、v4.7.14 维护线，首项不表示所有维护线中最晚的发布时间。[模板](https://github.com/onyx-dot-app/onyx/blob/5bfd6e0b55922466e45e2ff822910c609508a74c/deployment/docker_compose/env.template)

## 原理

连接器拉取文档及元数据，经后台索引构建关键词 / 向量表示，检索后由模型生成有来源的回答；Agent 可进一步调用网页搜索、MCP 与外部动作。权限同步的文档权限与外部组成员同步分别运行，再供查询时 ACL 使用，权限变化并非天然即时生效。[权限组件说明](https://github.com/onyx-dot-app/onyx/blob/5bfd6e0b55922466e45e2ff822910c609508a74c/.agents/feature-map/components/permission-sync.md)

## 价值

为经常重复搜索多个业务系统的团队提供统一知识入口；回答引用方便回到原文核对。接入价值取决于连接器覆盖、索引新鲜度、权限一致性与检索质量，而不是仅看可连接应用数量。

## 风险边界

- 根许可将主体列为 MIT Expat，所有 `ee` 目录另用企业许可；README 的 MIT 徽标不能涵盖整个仓库。[LICENSE](https://github.com/onyx-dot-app/onyx/blob/5bfd6e0b55922466e45e2ff822910c609508a74c/LICENSE)
- 仓库 feature map 明确把源系统权限同步列为 EE-only，当前实现也位于 `backend/ee/`。CE 的手动共享范围与源 ACL 自动同步不可混写；该 feature map 自带较早核验 commit，本轮只交叉核其实现位置，未跑完整权限链。[实现](https://github.com/onyx-dot-app/onyx/blob/5bfd6e0b55922466e45e2ff822910c609508a74c/backend/ee/onyx/external_permissions/sync_params.py)
- 自托管允许把索引、数据库和处理部署在本环境，但模型、embedding、网页搜索、外部动作与具体遥测配置仍需逐项核，不能据部署位置声称全栈断网。
- 检索文本和网页可能包含提示注入；有来源的回答仍可能误引、漏引或超出原文。启用外部动作后，风险从读资料扩展到写业务系统。

## 补充建议

验收至少包括：两个角色的检索隔离、源权限撤销后的生效延迟、删除文档后的残留、连接器失败重试及引用准确率。先验证 Standard 读权限，再独立接入 Actions；将 main 模板与正式发行差异写入部署记录。本轮未部署、同步组织资料或授权第三方应用。

## 参考资料

- [README.md](https://github.com/onyx-dot-app/onyx/blob/5bfd6e0b55922466e45e2ff822910c609508a74c/README.md)（固定 commit）。
- [LICENSE](https://github.com/onyx-dot-app/onyx/blob/5bfd6e0b55922466e45e2ff822910c609508a74c/LICENSE)（固定 commit）。
- [deployment/docker_compose/env.template](https://github.com/onyx-dot-app/onyx/blob/5bfd6e0b55922466e45e2ff822910c609508a74c/deployment/docker_compose/env.template)（固定 commit）。
- [.agents/feature-map/components/permission-sync.md](https://github.com/onyx-dot-app/onyx/blob/5bfd6e0b55922466e45e2ff822910c609508a74c/.agents/feature-map/components/permission-sync.md)（固定 commit）。
- [backend/ee/onyx/external_permissions/sync_params.py](https://github.com/onyx-dot-app/onyx/blob/5bfd6e0b55922466e45e2ff822910c609508a74c/backend/ee/onyx/external_permissions/sync_params.py)（固定 commit）。
- [正式发行列表](https://github.com/onyx-dot-app/onyx/releases)、[仓库 API](https://api.github.com/repos/onyx-dot-app/onyx)（动态状态）。
