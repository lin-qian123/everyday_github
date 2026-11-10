<!-- markdownlint-disable MD013 -->

# Sure

> 更新：2026-11-11（Asia/Shanghai）。分类：办公、商业与行业应用。上游 `we-promise/sure`，仓库 ID `1024661423`；固定源码 `79e8a26895f7ca326b15caae1a662144d4e1822d`。本文为官方榜单、API、文档与指定源码的静态核读，未部署、连接账户或调用模型。

## 定位

Sure 是已归档 Maybe Finance 的社区延续，用于汇总账户、交易、预算、贷款与资产。AI 助手是可选层，另有后台分类与商户识别；不是一个专为交易或收益预测训练的模型。[项目说明](https://github.com/we-promise/sure/blob/79e8a26895f7ca326b15caae1a662144d4e1822d/README.md)

官方综合 daily 为 +184 stars；API 快照为 11,878 stars / 886 forks / 891 open issues（含 PR）。稳定发行 [v0.7.6](https://github.com/we-promise/sure/releases/tag/v0.7.6) 发布于 UTC 10-31；UTC 11-10 的 [v2026.11.10-alpha](https://github.com/we-promise/sure/releases/tag/v2026.11.10-alpha) 是预发行，兼容别名为 0.7.7-alpha.5。下文主线文档中的新能力不可全部归入稳定包。[API](https://api.github.com/repos/we-promise/sure)

## 用法

自托管优先按 [Docker 指南](https://github.com/we-promise/sure/blob/79e8a26895f7ca326b15caae1a662144d4e1822d/docs/hosting/docker.md)准备 Compose 和 `.env`，生成独立 `SECRET_KEY_BASE`，确认镜像渠道、端口及存储后再启动。`stable` 对应稳定渠道，`latest` 对应 alpha；可复现实验应记录实际镜像 digest。

```bash
# 已审阅并配置 compose.yml 和 .env 后，在专用部署目录执行
docker compose up -d
docker compose ls
```

先用虚构交易或 CSV 样例核币种、时间和分类，再接数据提供方。仅需账本可不配 AI；内置助手、外部助手及 `mcp_only` 是不同入口，后台分类另有独立 provider 配置。修改环境后使用 `docker compose up -d` 重建相关容器，单纯 restart 不更新容器环境。[AI 配置](https://github.com/we-promise/sure/blob/79e8a26895f7ca326b15caae1a662144d4e1822d/docs/hosting/ai.md)

## 原理

应用以 Rails、PostgreSQL、Redis / Sidekiq 管理持久账本和后台任务。内置助手调用模型，再执行账户、交易、预算等结构化函数；外部助手把整段对话委托远端 Agent，由其通过 MCP 回读或修改 Sure。分类和商户识别是另一条后台流水线，切换聊天入口不会自动切换这条数据流。[AI 架构](https://github.com/we-promise/sure/blob/79e8a26895f7ca326b15caae1a662144d4e1822d/docs/hosting/ai.md)

核读的函数调度器解析 JSON 后调用对应函数，错误作为工具结果返回；这里没有通用的逐次人工批准流程。各工具的账户权限、预览和 dry-run 要单独核对，不能从聊天界面推断全局只读。[调度实现](https://github.com/we-promise/sure/blob/79e8a26895f7ca326b15caae1a662144d4e1822d/app/models/assistant/function_tool_caller.rb)

## 价值

适合把碎片化财务资料汇总为可查询、可追溯的个人账本，并比较确定性规则、Bayes 分类与 LLM 分类的成本和误差。稳定发行的支出变化、贷款计划与备份改进有实际管理价值；是否分类正确、能否恢复数据仍需自己的样本验证。[稳定发行说明](https://github.com/we-promise/sure/releases/tag/v0.7.6)

## 风险边界

- **自托管不等于数据全在本机**：云模型、银行 / 市场数据源及外部 Agent 各有出口。启用 Langfuse 后文档列明会发送 prompts、responses、session ID 等；用户 ID 哈希不等于提示词中的交易内容已匿名化。[AI 与观测说明](https://github.com/we-promise/sure/blob/79e8a26895f7ca326b15caae1a662144d4e1822d/docs/hosting/ai.md)
- **MCP 有写能力**：OAuth 动态注册获得 `read_write` scope；静态 token 绑定配置用户，工具包括交易、预算和账单修改。共享账户只读限制、工具 dry-run 与调用者身份需分别核验。[MCP](https://github.com/we-promise/sure/blob/79e8a26895f7ca326b15caae1a662144d4e1822d/docs/hosting/mcp.md)
- **示例部署需实际配置**：Compose 有固定的 secret fallback，端口映射没有限定 loopback；请设置独立 secret 并按目标限制绑定。开发服务器默认 localhost 不能代表 Compose 的暴露范围。[Compose](https://github.com/we-promise/sure/blob/79e8a26895f7ca326b15caae1a662144d4e1822d/compose.example.yml)
- **备份包含敏感配置**：备份含 `.env` 和加密所需 secret；外部对象存储中的上传文件不包含在本地备份中。数据库 dump 工具版本、恢复版本与迁移要匹配。[备份指南](https://github.com/we-promise/sure/blob/79e8a26895f7ca326b15caae1a662144d4e1822d/docs/hosting/docker.md)
- 根代码为 AGPL-3.0；Maybe 商标与第三方服务另有边界。账本分析和 AI 解释不能证明财务数据完整或任何投资收益。[许可](https://github.com/we-promise/sure/blob/79e8a26895f7ca326b15caae1a662144d4e1822d/LICENSE)

## 补充建议

以一组可手算的多币种、转账、退款和贷款数据建立基线，分别检查账本与 AI 解释；记录分类误差、重试和 token 成本。上线前做一次“备份 → 同版本恢复 → 对账”，再验证 MCP 读写、撤权及多用户账户范围。先确定稳定版需求，再决定是否采用 alpha 的新入口。

## 参考资料

1. [固定 SHA 项目说明](https://github.com/we-promise/sure/blob/79e8a26895f7ca326b15caae1a662144d4e1822d/README.md)
2. [Docker、升级与备份](https://github.com/we-promise/sure/blob/79e8a26895f7ca326b15caae1a662144d4e1822d/docs/hosting/docker.md)
3. [AI 配置与数据流](https://github.com/we-promise/sure/blob/79e8a26895f7ca326b15caae1a662144d4e1822d/docs/hosting/ai.md)
4. [MCP 身份与工具](https://github.com/we-promise/sure/blob/79e8a26895f7ca326b15caae1a662144d4e1822d/docs/hosting/mcp.md)
5. [官方综合 Trending](https://github.com/trending?since=daily)
