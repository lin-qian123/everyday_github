# twenty

## 项目定位
Twenty 是一个面向 AI 场景的开源 CRM，目标是替代传统 Salesforce 式系统，并把 CRM 对象、字段、视图和自动化能力以“可代码化”方式交付。

- GitHub: https://github.com/twentyhq/twenty
- 官网: https://www.twenty.com/
- 文档: https://docs.twenty.com/

## 用法

### 1. 云端快速体验
- 在官网创建工作区，适合先验证流程与数据模型。

### 2. 通过 CLI 构建应用
- 官方示例命令：

```bash
npx create-twenty-app my-app
npx twenty app:publish --private
```

### 3. 自托管
- 官方提供 Docker Compose 与本地开发指南，适合私有化部署与深度定制。

## 原理
- 采用“业务对象 + 字段 + 视图 + 工作流/代理”组合，把 CRM 从封闭 SaaS 转成可版本化工程资产。
- 开发团队可用代码定义销售流程和数据结构，再发布到工作区，形成“产品配置即代码”的闭环。

## 价值
- 对技术团队：更易接入既有工程体系（代码评审、版本管理、CI/CD）。
- 对业务团队：在保留 CRM 能力的同时，缩短需求到上线链路。
- 对 AI 工作流：可将 Agent 能力绑定到 CRM 数据与动作层。

## 风险边界
- 迁移成本：从旧 CRM 迁移历史数据与流程规则可能较重。
- 治理复杂度：可定制能力越强，权限、审计、变更管理要求越高。
- 生态成熟度：与成熟 CRM 生态相比，插件与行业模板可能仍在建设中。

## 补充建议
- 先用单一业务线（如线索管理）做 MVP，再逐步扩展到全量流程。
- 提前定义“对象模型命名规范 + 字段变更策略 + 权限分层”。
- 在生产前补齐备份、审计日志和变更回滚机制。

## 参考资料
- GitHub Trending（2026-05-29）: https://github.com/trending
- 仓库 README: https://github.com/twentyhq/twenty
