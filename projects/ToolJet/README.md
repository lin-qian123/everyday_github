<!-- markdownlint-disable MD013 -->

# ToolJet

## 定位

[`ToolJet/ToolJet`](https://github.com/ToolJet/ToolJet) 是构建内部工具、工作流和 AI agent 的低代码平台。社区版提供拖拽式页面、数据库/API/SaaS/对象存储连接器、内置数据库以及 JavaScript/Python 查询能力；上游同时提供含 AI 应用生成、查询生成和 agent builder 的商业产品。它适合将既有业务数据与受控操作拼装成内部界面，但不应把“低代码”理解为免除数据访问治理。

## 用法

上游提供托管服务和自托管路线；以下是其 README 的本地 Docker 快速体验命令。它会占用主机 80 端口并创建持久化卷，开始前应确认端口、镜像标签、数据保留和部署主机权限。

```bash
docker run \
  --name tooljet \
  --restart unless-stopped \
  -p 80:80 \
  --platform linux/amd64 \
  -v tooljet_data:/var/lib/postgresql/13/main \
  tooljet/try:ee-lts-latest
```

首次验证宜从只读数据源和测试租户开始：新建页面、添加组件、配置最小权限连接器，再为每个查询、脚本和工作流建立发布前审阅。生产自托管应采用上游 [Docker/Kubernetes 部署文档](https://docs.tooljet.com/docs/setup/) 与组织自身的身份、密钥和备份策略。

## 原理

- 平台把 UI 组件、数据源查询、脚本和页面/工作流配置组合为内部应用；连接器从平台侧代理访问数据库、API、云存储和 SaaS。
- 内置数据库、多人协作和访问控制降低搭建门槛，但具体的数据行、查询、服务账号和脚本仍是独立信任边界。
- AI 相关生成、调试和 agent 功能属于上游区分的产品能力；不可将社区版仓库的开源许可证或功能范围自动外推到所有托管/企业特性。

## 价值

- 对已有 SQL、REST、SaaS 和对象存储系统，能较快构建可操作的内部仪表板、审批页和工作台。
- 低代码界面与代码查询可并用，适合把原型、受控业务操作和后续工程化分层推进。
- GitHub API 于 2026-08-17 的快照约为 40.0k stars、5.3k forks，许可证为 AGPL-3.0；GitHub Trending 当日页面显示约 +446 stars。上述仅是公开关注度和代码许可证信息，不等同于其商业版合规性、安全能力或对特定数据源的适配结论。

## 风险边界

- 连接器凭据、查询结果、导出、错误日志和用户脚本可能接触生产数据；需做到每个数据源最小权限、密钥托管、传输/静态加密和审计留痕。
- `try:ee-lts-latest` 并非可复现的固定镜像引用；生产部署要锁定镜像 digest，并在升级前备份数据库、演练回滚。
- 浏览器端展示的角色控制不能替代数据库侧行列级授权。敏感查询和写操作应在后端/API/数据库层再次验证身份、范围和审批。
- AGPL-3.0 的网络交互条款及其与企业版、插件、托管服务和依赖的关系，应由组织法务按实际分发/修改方式评估。

## 补充建议

1. 用脱敏副本搭建第一版，仅授予只读连接器；对写操作增加双人审批、幂等键、额度/范围限制和审计记录。
2. 为每个页面建立数据流清单：用户角色、组件、查询、服务账号、返回字段、日志位置与保留期。
3. 把生成式 AI 输出视为草稿，限制它直接生成或执行 SQL、运维命令和业务动作，并要求人工复核差异。
4. 部署前进行 SSO/RBAC、CORS、webhook、备份恢复、镜像更新和越权访问测试；不以 stars 或产品宣传代替验证。

## 参考资料

- [GitHub 仓库](https://github.com/ToolJet/ToolJet)
- [上游 README / Quickstart](https://github.com/ToolJet/ToolJet#quickstart)
- [官方部署文档](https://docs.tooljet.com/docs/setup/)
- [数据源文档](https://docs.tooljet.com/docs/data-sources/airtable/)
- [GitHub REST API 元数据快照](https://api.github.com/repos/ToolJet/ToolJet)
